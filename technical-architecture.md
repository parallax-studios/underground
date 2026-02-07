# UNDERGROUND -- Technical Architecture Document

**Author**: BYTE (Lead Programmer)
**Status**: First Pass - Ready for Implementation
**Version**: 1.0
**Date**: 2026-02-07

---

## 1. Executive Summary

UNDERGROUND is a multi-genre street culture sim combining racing, fighting, basketball, and freestyle tricks in a single reputation-driven career. The technical challenge is clear: build four different game genres that feel like one cohesive experience, ship it, and keep it running at 60fps on Steam Deck.

This is not the place for novel tech. We use proven tools, battle-tested patterns, and ruthlessly scope to what ships. The complexity budget goes into gameplay systems, not rendering tech. The architecture prioritizes iteration speed over theoretical purity. Every decision in this document has one goal: ship a playable build every two weeks.

**Core Technical Thesis**: Unity as foundation. ECS for hot-path gameplay. State machines for game modes. ScriptableObjects for data. Addressables for content. CI/CD from day one. Profile before optimizing. Ship it, then improve it.

Target specs:
- 60fps on Steam Deck (800p)
- 120fps on mid-tier PC (1080p)
- 4GB RAM footprint max
- Sub-10-second load times district-to-district
- Zero loading screens during gameplay

---

## 2. Engine & Framework Selection

### 2.1 Core Engine: Unity 2022.3 LTS

**Why Unity**:
- Proven for multi-genre games (Yakuza-like scope)
- ECS + DOTS for hot-path performance where needed
- Mature asset pipeline for rapid iteration
- Strong tooling ecosystem (Odin Inspector, DOTween, etc.)
- Decent console porting path if we need it later
- I've shipped games on it. I know where the bodies are buried.

**Why not Unreal**:
- Blueprint spaghetti is a maintenance nightmare for multi-genre complexity
- C++ compile times kill iteration speed
- Overkill for PS2-aesthetic target (we're not chasing photorealism)
- Team would need to ramp up on a new toolchain

**Why not Godot**:
- Immature 3D performance for dense city + four game genres
- Small middleware ecosystem
- GDScript is fine for small projects; this isn't small
- High risk for a commercial ship

**Version specifics**: Unity 2022.3 LTS (not 2023.x - we don't beta-test on Unity's experimental branch). LTS means two years of stable patches. We lock the version on day one and only upgrade if a critical bug forces it.

### 2.2 Language & Architecture Pattern

**Primary Language**: C# (Unity standard)

**Architecture Pattern**: Hybrid ECS + MonoBehaviour
- **ECS (Unity DOTS)** for:
  - Racing physics (hundreds of physics ticks per frame)
  - Crowd simulation (hundreds of NPCs reacting to player)
  - Particle systems (underglow, tire smoke, impact effects)
- **MonoBehaviour** for:
  - Game state management
  - UI systems
  - AI behavior trees (readability over micro-optimization)
  - Audio management

Why hybrid? Full ECS is fast but painful to debug and iterate. MonoBehaviour is slow but readable. Use ECS where profiling proves we need it. Use MonoBehaviour everywhere else. The performance budget is "60fps on Steam Deck," not "maximum theoretical throughput."

### 2.3 Target Platforms

**Primary**: PC (Steam)
- Windows 10/11 x64
- SteamInput API for controller support
- Steam Cloud for save sync
- Steam Achievements for milestone tracking

**Secondary**: Steam Deck (validated target)
- Linux/Proton compatibility (Unity 2022.3 handles this)
- 800p rendering resolution
- 60fps minimum (this is the performance floor for all tuning)

**Tertiary** (post-launch consideration): Console (PS5/Xbox Series)
- Unity has mature console pipelines
- Input system designed console-first (controller is primary, KB+M is secondary)
- Not committed until post-launch based on sales

**Platform abstraction layer**: Unity's Input System package. Controller is the assumed input. Keyboard/mouse is a fallback. No motion controls, no touch, no VR.

### 2.4 Rendering Strategy

**Renderer**: Universal Render Pipeline (URP)
- Forward rendering (no deferred - we don't have hundreds of lights)
- Single-pass instanced for VR-readiness (even though we're not doing VR, it's free perf)
- Post-processing stack: CRT shader, bloom, film grain, chromatic aberration
- Target: PS2-era aesthetic with modern anti-aliasing

**Visual target**: "PS2 game rendered in 2026"
- Low-poly models (5k-15k tris per car, 3k-8k per character)
- Stylized textures (hand-painted look, not PBR photorealism)
- Heavy post-processing to sell the CRT aesthetic
- Neon/underglow as primary light sources (simple point lights, no real-time GI)

**Camera**: Dynamic third-person with discipline-specific modes
- Racing: behind-car cam with drift tilt
- Fighting: side-view with dynamic zoom based on distance
- Basketball: over-shoulder with court awareness
- Tricks: free-following with trick highlighting

Camera transitions between disciplines: 2-second cinematic blend using Cinemachine state-driven cameras. No hard cuts. The camera system is what makes this feel like one game instead of four.

---

## 3. System Architecture Overview

### 3.1 High-Level Component Diagram

```
+----------------------------------------------------------+
|                    GAME DIRECTOR                         |
|  (State Machine: MainMenu -> DistrictRoam -> Event ->    |
|   Results -> Garage -> Repeat)                           |
+------------------------+---------------------------------+
                         |
         +---------------+----------------+
         |                                |
+--------v-----------+        +-----------v-----------+
|  WORLD MANAGER     |        |  EVENT MANAGER        |
|  - District state  |<------>|  - Event spawning     |
|  - NPC population  |        |  - Discipline router  |
|  - Time/weather    |        |  - Results calc       |
+--------+-----------+        +-----------+-----------+
         |                                |
         |                    +-----------v-----------+
         |                    | DISCIPLINE MODULES    |
         |                    | - Racing System       |
         |                    | - Fighting System     |
         |                    | - Basketball System   |
         |                    | - Tricks System       |
         |                    +-----------+-----------+
         |                                |
+--------v-----------+        +-----------v-----------+
|  PROGRESSION       |        |  INPUT MANAGER        |
|  - REP/CASH        |<------>|  - Controller binding |
|  - Style Meter     |        |  - Context switching  |
|  - Rival AI State  |        +-----------+-----------+
+--------+-----------+                    |
         |                    +-----------v-----------+
+--------v-----------+        |  AUDIO MANAGER        |
|  PERSISTENCE       |        |  - Music system       |
|  - Save/Load       |        |  - SFX pooling        |
|  - Steam Cloud     |        |  - Beat sync          |
+--------------------+        +-----------------------+
```

### 3.2 Data Flow: Event Loop

```
Player approaches event marker on map
    |
    v
WorldManager detects proximity -> triggers EventManager
    |
    v
EventManager determines discipline type -> loads Event ScriptableObject
    |
    v
Event ScriptableObject contains:
    - Discipline enum (Racing/Fighting/Basketball/Tricks)
    - Difficulty tier
    - Rival lineup
    - Environment config
    - Victory conditions
    |
    v
EventManager routes to appropriate Discipline Module
    |
    v
Discipline Module:
    - Spawns necessary entities (opponents, props, UI)
    - Initializes physics context (racing uses vehicle physics, fighting uses character physics)
    - Binds input context
    - Starts event timer
    |
    v
Player performs -> Input -> Discipline-specific logic -> Style Meter update
    |
    v
Event ends (timer expires or victory condition met)
    |
    v
EventManager calculates results:
    - Style rank (D-S based on Style Meter performance)
    - REP earned (base + style multiplier + bonuses)
    - CASH earned
    - Rival AI reaction (update Respect/Grudge/Confidence)
    |
    v
Results screen -> Player returns to WorldManager roaming state
    |
    v
WorldManager updates district state (new events may unlock, rival phone call may trigger)
```

### 3.3 Memory Architecture

**Memory budget breakdown** (4GB total target):

| System | Budget | Notes |
|--------|--------|-------|
| District geometry + textures | 1.2 GB | One district loaded at a time. Addressables for streaming. |
| Vehicle/Character models | 400 MB | Player + 8 rivals + 20 ambient NPCs in view |
| Audio (music + SFX) | 600 MB | Compressed Vorbis. One music track + SFX pool. |
| Gameplay systems (ECS) | 300 MB | Physics state, AI state, particle systems |
| UI + HUD | 150 MB | Atlas-based UI, minimal draw calls |
| Scripting overhead | 250 MB | Mono runtime + game code |
| OS + Unity engine | 1.1 GB | Unity's fixed cost on Steam Deck |
| **Total** | **4.0 GB** | Tight but achievable with streaming and pooling |

**Streaming strategy**: One district loaded at a time. District transitions trigger an Addressables async load of the next district while showing a "driving through tunnel" transition (2-3 seconds, not a loading screen per se, but enough time to swap memory). Old district unloads once new district is fully loaded. No two districts in memory simultaneously.

**Object pooling**: Aggressive pooling for:
- Particle effects (tire smoke, sparks, underglow trails)
- Audio sources (100+ simultaneous sounds during races)
- UI elements (pop-up text for style points)

Use Unity's `ObjectPool<T>` API. Pre-warm pools at district load time.

---

## 4. Core Systems Design

### 4.1 Racing System

**Physics Engine**: Unity's built-in PhysX with custom vehicle controller

**Why custom controller**: Unity's Wheel Collider is decent for sims but we need arcade handling with exaggerated drift. Building on top of Rigidbody with custom forces for:
- Drift angle (steering input + velocity direction mismatch triggers drift state)
- Nitrous (impulse force along velocity vector)
- Near-miss detection (SphereCast for proximity to traffic/walls)

**Implementation**:
```
VehicleController (MonoBehaviour on player car)
    - Rigidbody reference
    - Drift state machine (Grip -> Initiating -> Drifting -> Exiting)
    - Input: steering axis, throttle, brake, nitrous button
    - Per-frame: Apply forces based on state, calculate drift angle, emit particles

RacingEventManager (MonoBehaviour, spawned during race events)
    - Opponent AI (8 max)
    - Waypoint-based pathfinding with rubber-banding
    - Lap counter, position tracker
    - Near-miss detector (reports to Style Meter system)

StyleScorer (System, listens to racing events)
    - Drift seconds accumulated -> +15 points/sec
    - Near-miss triggers -> +40 points each
    - Position gains -> +20 points per place
```

**AI opponents**: Waypoint-based navigation. Each opponent has a "skill level" (0-100) that affects:
- Pathing accuracy (low skill = wider turns, more mistakes)
- Speed multiplier (scales with difficulty tier)
- Rubber-banding strength (if player is far ahead, opponents speed up; if far behind, slow down)

Rubber-banding is controversial but necessary for this genre. We're not simulating F1. We're creating drama. The player should feel fast, not untouchable.

**Performance target**: 60fps with 8 opponents + player at 800p. Vehicle physics runs at 50hz (physics timestep = 0.02s). Rendering at 60hz. Physics is the bottleneck. Use Unity Jobs System for opponent AI pathfinding (parallel job per opponent).

**Data-driven config**: Each car is a ScriptableObject:
```csharp
[CreateAssetMenu(menuName = "UNDERGROUND/CarData")]
public class CarData : ScriptableObject {
    public float mass;               // kg (800-1400 range)
    public float enginePower;        // 0-100 scale
    public float grip;               // 0-100 scale (low = drifty)
    public float nitrousCapacity;    // seconds of boost
    public float visualFlash;        // 0-100 (affects Style Meter gain rate)
    public Mesh bodyMesh;
    public Material[] materials;
    // etc.
}
```

Designers can tweak car stats without touching code. This is critical for balance iteration.

### 4.2 Fighting System

**Combat Engine**: Custom frame-data-driven system (think simplified fighting game frame data)

**Why not a physics engine**: Fighting game feel comes from frame-perfect timing and hit/hurtbox precision, not realistic physics. We need:
- Defined startup/active/recovery frames for every move
- Hitbox/hurtbox detection (not collision, but overlap checks)
- Combo system with hitstun and cancel windows

**Implementation**:
```
FighterController (MonoBehaviour on player and rival fighters)
    - Animator (drives visual animation)
    - MoveDatabase (ScriptableObject with frame data for all moves)
    - State: Idle, Attacking, Hitstun, Blocking, Taunting
    - Input buffer (stores last 10 frames of input for combo detection)

FightingEventManager (MonoBehaviour, spawned during fight events)
    - Two fighters (player + opponent)
    - Health tracking
    - Round timer
    - Crowd reaction system (feeds Style Meter)

HitboxManager (System, runs per-frame during fights)
    - Reads active move's hitbox data from frame data
    - Checks overlap with opponent's hurtbox
    - On hit: apply damage, trigger hitstun, check for combo continuation

MoveData (ScriptableObject):
    - Startup frames (before hitbox is active)
    - Active frames (hitbox is live)
    - Recovery frames (post-hit cooldown)
    - Damage value
    - Hitstun value (opponent's freeze time)
    - Style value (points awarded to Style Meter on hit)
    - Cancel windows (which frames allow canceling into another move)
```

**Combo system**: Input buffer stores last 10 frames. On move execution, check buffer for valid cancel patterns (e.g., Light -> Light -> Heavy is a valid 3-hit combo if frame data allows Light to cancel into Light within N frames).

**AI opponents**: Behavior tree with personality modifiers:
- Aggressive: higher chance to attack, lower block rate
- Defensive: higher block rate, counter-attack preference
- Showboat: uses taunts (high risk/high reward AI behavior)

Each rival has a personality profile (defined in Rival ScriptableObject) that modulates these weights.

**Performance target**: Fighting is the cheapest discipline performance-wise. Two characters, minimal geometry, locked camera. Should run at 120fps on mid-tier PC easily. The bottleneck is animation blending, which Unity's Animator handles well.

**Frame data balance**: This is fighting game design 101. Every move must feel good to execute and fair to counter. We target:
- Light attacks: 4-6 startup frames, 2-3 active, 8-10 recovery
- Medium attacks: 8-10 startup, 3-4 active, 12-15 recovery
- Heavy attacks: 12-16 startup, 4-6 active, 20-25 recovery
- Taunts: 0 startup, 0 active, 72 recovery (1.2 seconds at 60fps)

All frame counts assume 60fps. If framerate drops, input buffer and cancel windows must account for it. Use `Time.deltaTime` for timing, not frame counts directly.

### 4.3 Basketball System

**Core Mechanic**: 2v2 streetball, first to 11 points (1s and 2s)

**Physics**: Mixture of physics-based ball (Rigidbody + SphereCollider) and scripted events (dunks, alley-oops)

**Implementation**:
```
BasketballController (MonoBehaviour on player)
    - Ball possession state (HasBall, NoBall)
    - Dribble state machine (Dribbling, Shooting, Passing)
    - Input: movement, shoot button, pass button, crossover button
    - Animation-driven (Animator with IK for ball handling)

BasketballEventManager (MonoBehaviour, spawned during ball games)
    - Four players (player + AI partner + 2 opponents)
    - Score tracking
    - Shot detection (ball enters hoop trigger -> score)
    - Court boundaries (out-of-bounds detection)

BasketballAI (Component on AI players)
    - Role: Offense or Defense
    - Behavior: On offense, position for pass or drive. On defense, guard assigned opponent.
    - Skill level modulates success rates (e.g., AI shooting accuracy)

CrossoverSystem (detects player input timing vs. defender proximity)
    - Successful crossover: defender enters brief stun animation, player gains +35 style
    - Failed crossover: turnover, ball goes to defense
```

**Ball physics**: The ball is a Rigidbody. Shooting applies an impulse toward the hoop with arc calculation (simple projectile math). On successful shot entry (ball passes through hoop trigger collider), award points.

**Ankle-breaker mechanic**: When player uses crossover move within 2m of a defender, check timing window (200ms). If defender is moving in the wrong direction during window, trigger ankle-breaker (defender falls, slow-mo camera, +35 style points, crowd erupts).

**AI teammates**: The player's AI partner must be competent enough that losing doesn't feel like the AI's fault. Partner AI uses same behavior tree as opponents but with "Help Player" priority. If player has ball, partner positions for pass. If player doesn't have ball, partner attempts to get open or screen.

**Performance target**: Four characters + ball physics + crowd. Should run at 60fps on Steam Deck. The ball physics at 50hz (same as racing). Characters use Unity's NavMesh for court positioning (baked NavMesh per court, cheap lookups).

### 4.4 Tricks System

**Core Mechanic**: Tony Hawk-style trick linking with score attack

**Physics**: Character controller (not Rigidbody) for precise air control, with gravity applied manually

**Implementation**:
```
TrickController (MonoBehaviour on player)
    - State machine: Grounded, Airborne, Grinding, Manual
    - Input buffer (for trick combinations)
    - Rotation tracker (for spin tricks)
    - Trick queue (linked tricks in current combo)

TrickEventManager (MonoBehaviour, spawned during trick events)
    - Score accumulator
    - Combo multiplier (increases per linked trick)
    - Bail detection (failed landing = lose combo)
    - Environment: ramps, rails, halfpipes

TrickDatabase (ScriptableObject)
    - Trick definitions (input combination -> trick name + base score)
    - Animation clips per trick
    - Timing windows for links
```

**Trick system**: Each trick is defined by an input combination (e.g., Grab + Up = Indy Grab). Tricks have base scores. Linking tricks multiplies score (x1, x2, x3, x4, etc.). Landing cleanly locks in the score. Bailing (landing at too steep an angle or too much speed) resets combo to zero.

**Grinding**: Rails have spline paths. When player touches rail trigger, enter grind state and lock movement to spline. Player can balance with left stick (balance meter). Falling off = bail.

**Manual mode**: On landing, player can enter manual (wheelie/nose manual) to extend combo without trick. This allows chaining across flat ground. Manual has balance meter. Lose balance = bail.

**AI**: Not applicable. Tricks are solo score attack. Optional: AI opponents for head-to-head trick battles, but not MVP for launch.

**Performance target**: One character + environment. Cheapest discipline. Should run at 120fps easily.

### 4.5 Career/Reputation System

**Data model**: Player save file contains:
```csharp
[System.Serializable]
public class PlayerSaveData {
    public int totalREP;
    public int currentCash;
    public float styleMeterCurrent;        // Carries between events for 10 min
    public Dictionary<string, int> districtREP;  // Per-district progress
    public List<RivalState> rivals;        // All rival relationships
    public InventoryData inventory;        // Owned cars, moves, gear
    public Dictionary<string, int> disciplineProficiency;  // Racing: 5, Fighting: 3, etc.
    public List<string> completedEvents;   // For diminishing returns tracking
    public float lastEventTimestamp;       // For cross-discipline chain detection
    public string lastEventDiscipline;     // For chain bonuses
}

[System.Serializable]
public class RivalState {
    public string rivalID;
    public int respect;       // -100 to +100
    public int grudge;        // 0 to 100
    public int confidence;    // 0 to 100
    public int pride;         // 0 to 100 (static personality trait)
    public bool isRecruited;  // Is this rival in player's crew?
    public int timesDefeated; // Player wins against this rival
    public int timesLost;     // Player losses to this rival
}
```

**Progression Manager** (Singleton MonoBehaviour):
```csharp
public class ProgressionManager : MonoBehaviour {
    public PlayerSaveData saveData;

    public void AwardREP(int baseREP, float styleMultiplier) {
        int finalREP = Mathf.RoundToInt(baseREP * styleMultiplier);
        saveData.totalREP += finalREP;
        CheckREPTierProgression();
    }

    public void UpdateRival(string rivalID, bool playerWon, int styleRank) {
        RivalState rival = GetRival(rivalID);
        if (playerWon) {
            rival.confidence -= 10;
            rival.respect += (styleRank >= 3 ? 10 : 5);  // A or S rank = +10
            rival.grudge += (styleRank == 4 ? 25 : 15);  // S rank humiliation = +25
            rival.timesDefeated++;
        } else {
            rival.confidence += 15;
            rival.respect -= 5;
            rival.timesLost++;
        }

        CheckRivalThresholds(rival);
    }

    private void CheckRivalThresholds(RivalState rival) {
        if (rival.grudge >= 70) {
            // Rival enters "Obsessed" state - start appearing randomly
            EventManager.Instance.MarkRivalAsObsessed(rival.rivalID);
        }
        if (rival.respect >= 60 && !rival.isRecruited) {
            // Trigger recruitment dialogue
            DialogueManager.Instance.TriggerRecruitmentOffer(rival.rivalID);
        }
        if (rival.confidence <= 0 && rival.grudge > 50) {
            // Rival breaks - permanent story change
            StoryManager.Instance.TriggerRivalBreak(rival.rivalID);
        }
    }
}
```

**Persistence**: Save file is JSON serialized. Unity's `JsonUtility` works but has limitations (no dictionaries). Use Newtonsoft Json.NET for flexibility:
```csharp
public void SaveGame() {
    string json = JsonConvert.SerializeObject(saveData, Formatting.Indented);
    File.WriteAllText(GetSavePath(), json);
    // Also push to Steam Cloud if on Steam
    if (SteamManager.Initialized) {
        SteamRemoteStorage.FileWrite("save.json", Encoding.UTF8.GetBytes(json));
    }
}
```

Save triggers:
- After every event completion (auto-save)
- On district transition
- On game exit
- Manual save option in menus

**REP tier unlocks**: Check `totalREP` against tier thresholds. When threshold crossed, unlock new districts, trigger story beats, update NPC dialogue.

### 4.6 District Map & World

**Map structure**: Four districts, each roughly 1km x 1km. Dense Yakuza-style cities, not GTA sprawl.

**Technical approach**: Single scene per district. Addressables for async loading during transitions.

**District components**:
```
District_Southside (Scene)
    - Terrain mesh (roads, buildings, props)
    - Event markers (prefabs placed in-world, contain Event ScriptableObject reference)
    - NPC spawn points (ambient population)
    - District boss location (locked until REP threshold)
    - Lighting (baked lightmaps for static geo, real-time for cars/characters)
```

**Event markers**: Empty GameObjects with `EventTrigger` component. When player enters trigger collider, UI prompt appears ("Press X to start event"). On input, EventManager takes over.

**NPC population**: Ambient NPCs for atmosphere (crowds on sidewalks, traffic on roads). Not full AI - simple patrols on NavMesh. Use ECS for population density (DOTS Entities for hundreds of NPCs with minimal logic).

**Time/Weather system**: Simple TOD (Time of Day) shader with day/night cycle. Weather is per-district config (e.g., always raining in the Docks district for visual identity). No dynamic weather - scope killer.

**Performance**: District geometry is the heaviest memory cost. Use aggressive LODs:
- LOD0: 0-50m (full detail)
- LOD1: 50-150m (half poly count)
- LOD2: 150m+ (billboards/impostors)

Bake lightmaps for all static geo. Use Light Probes for dynamic objects (cars, characters). No real-time shadows from street lights (baked shadows only). Player car casts real-time shadow (only one shadow-casting light: directional sun/moon).

### 4.7 NPC/Rival AI

**Two AI systems**:
1. **Named Rival AI** (25-30 rivals, behavior trees + personality attributes)
2. **Ambient NPC AI** (hundreds of background characters, minimal logic)

**Rival AI Architecture**:
```
RivalAI (MonoBehaviour on rival character)
    - Personality: RivalData ScriptableObject (Pride, initial Confidence, Style Affinity)
    - Current state: RivalState (from save data - Respect, Grudge, Confidence)
    - Behavior tree: Decides when to challenge player, which discipline to use

RivalData (ScriptableObject):
    public string rivalName;
    public Sprite portrait;
    public int basePride;           // 0-100, affects behavior
    public StyleAffinity affinity;  // enum: DriftRacer, Brawler, etc.
    public CarData preferredCar;    // For racing events
    public FighterData fighterData; // For fighting events
    // etc.
```

**Rival behavior logic**:
- Rivals "patrol" their home district (not literally moving, but logically present)
- When player enters district, RivalManager checks which rivals are present and likely to engage
- Engagement chance based on: player's REP, rival's current Grudge/Respect, random roll
- If rival engages, they appear at next event marker player approaches (or interrupt current event if Obsessed)

**Rival obsession mechanic**: When rival hits 70+ Grudge, they enter Obsessed state. This means:
- 40% chance to interrupt any player event in their district (crash a race, invade a fight)
- Will call player's phone (UI notification) demanding a challenge
- Will adapt their build to counter player's dominant strategy

Adaptation logic:
```csharp
public CarData CounterPlayerCar(PlayerSaveData player) {
    // Simple heuristic: check player's most-used car stats
    CarData playerCar = GetMostUsedCar(player);

    if (playerCar.grip > 70) {
        // Player uses grip racing, rival uses drift car to score more style
        return GetRandomCarWithStats(grip: 30-40, power: 80-90);
    } else {
        // Player drifts, rival uses grip car to win on racing line
        return GetRandomCarWithStats(grip: 80-90, power: 60-70);
    }
}
```

This is simple heuristic AI, not machine learning. It doesn't need to be smart. It needs to feel personal.

**Ambient NPC AI**: Use Unity DOTS Entities + Jobs. Each NPC is an Entity with:
- Position
- Patrol waypoints
- Animation state (walking, idle, cheering)

Jobs process NPC updates in parallel. Update rate: 10hz for ambient NPCs (they don't need frame-perfect updates). This keeps hundreds of NPCs cheap.

### 4.8 Crew Management System

**Crew concept**: Recruited rivals become crew members. Crew provides passive bonuses + active assist moves.

**Implementation**:
```
CrewManager (Singleton MonoBehaviour)
    - List<RivalState> crewMembers (references to recruited rivals)

    public void AddCrewMember(string rivalID) {
        RivalState rival = ProgressionManager.Instance.GetRival(rivalID);
        rival.isRecruited = true;
        crewMembers.Add(rival);
        ApplyCrewBonus(rival.affinity);
    }

    private void ApplyCrewBonus(StyleAffinity affinity) {
        // Example: Having a DriftRacer in crew gives +5% Style Meter gain in racing
        switch (affinity) {
            case StyleAffinity.DriftRacer:
                StyleMeterManager.Instance.racingMultiplier += 0.05f;
                break;
            case StyleAffinity.Brawler:
                StyleMeterManager.Instance.fightingMultiplier += 0.05f;
                break;
            // etc.
        }
    }
```

**Crew assists** (optional, stretch goal): During events, player can call in crew member for assist move:
- Racing: Crew member "blocks" an opponent for 5 seconds
- Fighting: Crew member throws in a distraction (opponent flinches, opening for player)
- Basketball: Crew member sets a screen

This is low priority. Core crew functionality is passive bonuses. Assists are polish if time allows.

### 4.9 Customization System

**Data model**: All customization items are ScriptableObjects

```
CarPartData (ScriptableObject)
    public string partName;
    public int cashCost;
    public CarPartType type;  // Engine, Tires, Body, Underglow, etc.
    public StatModifiers mods; // struct with mass, power, grip, etc. deltas
    public Mesh visualMesh;   // For body kits
    public Material[] materials;

FightingMoveData (ScriptableObject)
    public string moveName;
    public int cashCost;
    public MoveType type;  // Combo, Counter, Finisher, Taunt
    public FrameData frameData;  // Startup, active, recovery, damage, style
    public AnimationClip anim;

// Similar for basketball skills, trick moves, fashion items
```

**Garage/Locker Room UI**: Simple menu-driven interface:
- Display owned items
- Display available items for purchase (filtered by CASH)
- Equip/unequip items
- Preview visual changes (for cars, show 3D model; for characters, show character with new gear)

**Stat preview**: When hovering over a new part, show stat comparison:
```
Current Car:
  Mass: 1000kg
  Power: 75
  Grip: 40

With New Engine:
  Mass: 1000kg
  Power: 85 (+10)
  Grip: 40
```

**Synergy detection** (hidden system): After equipping items, run synergy check:
```csharp
public void CheckSynergies(PlayerSaveData player) {
    // Example: DriftKing + AnkleBreaker synergy
    bool hasDriftCar = player.inventory.equippedCar.grip < 50;
    bool hasFlashyCrossover = player.inventory.equippedBasketballSkills.Contains("FlashyCrossover");

    if (hasDriftCar && hasFlashyCrossover) {
        // Don't tell the player explicitly, just apply bonus
        StyleMeterManager.Instance.crossDisciplineMultiplier += 0.25f;
        // Maybe a subtle UI hint: "You feel a flow between your driving and your handles..."
    }
}
```

Synergies are discovered through play, not explained upfront. Community will datamine and share on wikis. This is intentional.

---

## 5. Data Architecture

### 5.1 ScriptableObject Structure

ScriptableObjects are Unity's killer feature for data-driven design. Use them for everything:

```
Assets/
  Data/
    Cars/
      CivicEG_Starter.asset
      S2000_MidTier.asset
      (etc. - 30-40 cars)
    Fighters/
      Player_BaseMoves.asset
      Rival_Brawler.asset
      (etc. - 20-30 move sets)
    Events/
      Southside_Race01.asset
      Docks_Fight02.asset
      (etc. - 100+ events)
    Rivals/
      Rival_Marcus.asset
      Rival_Keisha.asset
      (etc. - 25-30 rivals)
    Districts/
      District_Southside.asset
      (etc. - 4 districts)
```

**Why ScriptableObjects**:
- Designers can edit without touching code
- Version control friendly (text-based YAML in Unity)
- Fast lookup at runtime (asset references, not string lookups)
- Memory efficient (single instance shared across references)

**Example: Event ScriptableObject**:
```csharp
[CreateAssetMenu(menuName = "UNDERGROUND/Event")]
public class EventData : ScriptableObject {
    public string eventName;
    public DisciplineType discipline;
    public int difficultyTier;        // 1-5
    public int baseREP;               // REP awarded on completion
    public int baseCash;              // CASH awarded
    public List<RivalData> rivals;    // Which rivals appear
    public SceneReference scene;      // Addressable scene for this event
    public VictoryCondition victory;  // enum: FirstPlace, KO, Score, etc.
    public AudioClip musicTrack;      // Music for this event
}
```

### 5.2 Save Data Schema

**Single save file per player**: `save.json` in persistent data path

**Schema** (JSON structure):
```json
{
  "totalREP": 12500,
  "currentCash": 3400,
  "styleMeterCurrent": 450.5,
  "districtREP": {
    "Southside": 5000,
    "Docks": 3500,
    "Midtown": 4000,
    "Heights": 0
  },
  "disciplineProficiency": {
    "Racing": 6,
    "Fighting": 4,
    "Basketball": 5,
    "Tricks": 3
  },
  "rivals": [
    {
      "rivalID": "Marcus",
      "respect": 40,
      "grudge": 55,
      "confidence": 60,
      "isRecruited": false,
      "timesDefeated": 3,
      "timesLost": 1
    }
  ],
  "inventory": {
    "ownedCars": ["CivicEG_Starter", "S2000_MidTier"],
    "equippedCar": "S2000_MidTier",
    "ownedMoves": ["ComboA", "CounterB", "Taunt1"],
    "equippedMoves": ["ComboA", "CounterB"]
  },
  "completedEvents": ["Southside_Race01", "Southside_Fight01"],
  "lastEventTimestamp": 1675890123.456,
  "lastEventDiscipline": "Racing"
}
```

**Save frequency**: Auto-save after every event. Manual save in menus. Corrupted save fallback: If JSON parse fails, create new save and log error (don't crash).

**Steam Cloud**: If on Steam, sync save file to Steam Cloud on every save. Use Steam's file API:
```csharp
if (SteamRemoteStorage.IsCloudEnabledForAccount() && SteamRemoteStorage.IsCloudEnabledForApp()) {
    byte[] data = File.ReadAllBytes(GetSavePath());
    SteamRemoteStorage.FileWrite("save.json", data);
}
```

On game start, check Steam Cloud for save. If newer than local, download and use that.

### 5.3 Content Addressables

Unity Addressables for content streaming:

**Addressable Groups**:
- **Districts** (one group per district): Southside, Docks, Midtown, Heights
- **Cars** (one group for all car assets)
- **Characters** (one group for all character models + anims)
- **Audio** (one group per district's music + SFX)

**Loading pattern**:
```csharp
public async void LoadDistrict(string districtName) {
    // Unload previous district
    if (currentDistrictHandle.IsValid()) {
        Addressables.Release(currentDistrictHandle);
    }

    // Load new district
    currentDistrictHandle = Addressables.LoadSceneAsync($"District_{districtName}", LoadSceneMode.Single);
    await currentDistrictHandle.Task;

    // District is now loaded and active
}
```

**Build size impact**: Addressables allow splitting content into bundles. This means:
- Base game download: Engine + UI + one starting district (~2GB)
- Additional districts: Streamed on first access (~500MB each)

Not critical for PC (players will download full game), but useful if we port to console (reduces initial download size).

---

## 6. Performance Considerations

### 6.1 Target Framerate & Profiling Strategy

**Targets**:
- Steam Deck (800p): 60fps minimum, 120fps stretch
- Mid-tier PC (1080p): 120fps minimum
- High-end PC (1440p+): Uncapped (let it run as fast as hardware allows)

**Profiling approach**: Unity Profiler + custom markers

**Critical paths** (what runs every frame):
1. **Player input processing**: ~0.1ms (negligible)
2. **Physics tick** (50hz, so every 1.2 frames at 60fps): ~2ms budget
3. **AI updates** (rival AI + ambient NPCs): ~1ms budget
4. **Rendering** (draw calls, shaders, post-processing): ~10ms budget at 60fps (16.67ms total frame time - 6.67ms headroom)
5. **Style Meter updates**: ~0.1ms (simple math)
6. **Audio mixing**: ~0.5ms (Unity's audio engine overhead)

**Total per-frame budget**: 14ms (leaves 2.67ms headroom at 60fps)

**Where performance tanks**:
- **Too many draw calls**: Unity is CPU-bound on draw calls. Target: <500 draw calls per frame.
  - Mitigation: Aggressive batching (static batching for districts, dynamic batching for characters), atlased UI, GPU instancing for repeated objects.
- **Physics overhead**: 8 cars with complex colliders can kill framerate.
  - Mitigation: Simplified colliders (box/capsule for cars, not mesh colliders). PhysX runs on separate thread (Unity Job System).
- **Post-processing**: CRT shader is expensive (full-screen effect).
  - Mitigation: Write optimized shader. Render at lower resolution (e.g., 720p internal, upscale to 800p with post). Use URP's built-in upscaling.
- **Ambient NPCs**: Hundreds of NPCs with full Animators will destroy CPU.
  - Mitigation: ECS for NPCs. Simplified animation (no IK, no ragdoll, just walk cycles). Update at 10hz, not 60hz.

**Profiling workflow**:
1. Play test session for 10 minutes
2. Capture Unity Profiler deep profile
3. Identify top 5 CPU spikes
4. Optimize worst offender first
5. Repeat

Never optimize without data. Profiling before optimizing is law.

### 6.2 Multi-Genre Rendering

**Challenge**: Four different game genres with different camera angles, lighting needs, and visual priorities.

**Approach**: Unified rendering pipeline (URP) with per-discipline overrides

**Racing**:
- Camera: Wide FOV (80 degrees), motion blur enabled
- Lighting: Dynamic car headlights, underglow (real-time point lights)
- Post-processing: Heavy bloom, chromatic aberration on edges
- LOD bias: 1.0 (normal)

**Fighting**:
- Camera: Narrow FOV (60 degrees), locked angle
- Lighting: Dramatic overhead light, rim lights on characters
- Post-processing: Film grain, vignette
- LOD bias: 0.5 (higher detail - fewer objects in view)

**Basketball**:
- Camera: Medium FOV (70 degrees), dynamic zoom
- Lighting: Court lights (baked), character lights (real-time)
- Post-processing: Color grading (warm tones)
- LOD bias: 0.75 (detailed characters, simplified crowd)

**Tricks**:
- Camera: Wide FOV (85 degrees), follows player rotation
- Lighting: Environment-dependent (ramp lights, etc.)
- Post-processing: Light bloom, speed lines (custom shader)
- LOD bias: 1.0 (normal)

**Implementation**: Use URP's Volume system with per-discipline profiles. On discipline switch, lerp between Volume profiles over 2 seconds (during camera transition).

### 6.3 Physics Optimization

**Racing physics** (most expensive):
- Use simplified vehicle colliders (box for body, spheres for wheels)
- PhysX runs at 50hz (0.02s timestep). Don't increase - diminishing returns.
- Opponents use cheaper physics (no wheel colliders, just Rigidbody with forces)
- Track surfaces are static mesh colliders (expensive but unavoidable)

**Fighting physics** (cheap):
- No physics. Characters are kinematic (Animation-driven movement, manual collision checks for hitboxes)

**Basketball physics** (medium):
- Ball is only physics object (Rigidbody + SphereCollider)
- Characters are NavMesh agents (not physics-driven)
- Court boundaries are simple box colliders

**Tricks physics** (cheap):
- Character controller (not Rigidbody). Manual gravity application.
- Rails are spline paths (no collision, just trigger detection)

**PhysX threading**: Unity's PhysX runs on job threads (not main thread). Ensure physics work is job-ified using Unity's C# Job System where possible.

### 6.4 Memory Optimization

**Texture compression**:
- All textures: BC7 on PC (high quality, good compression)
- Albedo maps: 1024x1024 max (downscale from source 2k textures)
- Normal maps: 512x512 (normals compress poorly, keep resolution low)
- UI atlases: Single 2048x2048 atlas per UI screen (use Unity's Sprite Atlas)

**Mesh LODs**:
- LOD0: Full detail (5k-15k tris)
- LOD1: 50% tris
- LOD2: Impostor billboard (single quad with baked texture)

**Audio compression**:
- Music: Vorbis, 128kbps (high quality, good compression)
- SFX: Vorbis, 96kbps (lower quality acceptable for short sounds)
- Voice (if any): Vorbis, 64kbps (voice compresses well)

**Addressables memory management**:
- Load one district at a time
- Unload previous district explicitly (don't rely on GC)
- Use weak references for cached assets (allow GC to collect if memory pressure)

**GC (Garbage Collector) pressure**:
- Avoid per-frame allocations (no `new` in Update loops)
- Use object pools for frequently spawned objects
- Use `StringBuilder` for string concatenation
- Cache component references (don't call `GetComponent<T>()` every frame)

Target: <10ms GC spikes. If GC takes >10ms, it causes frame hitches. Profile and eliminate allocations.

---

## 7. Technical Risks

### 7.1 Primary Risks

**RISK 1: Four game genres = four times the complexity**

**Severity**: Critical
**Likelihood**: Certain
**Impact**: Each discipline is a mini-game with its own systems. If any one fails, the whole game suffers.

**Mitigation**:
- Build one discipline at a time to vertical slice quality
- Prototype each discipline independently (racing first, it's most legible)
- Validate fun before integration
- If a discipline doesn't hit quality bar by month 6, cut it or massively simplify
- Fallback: Ship with 3 disciplines (racing, fighting, basketball). Tricks become post-launch DLC.

**RISK 2: Cross-discipline balance is a nightmare**

**Severity**: High
**Likelihood**: High
**Impact**: Players optimize one discipline and ignore others. Game becomes single-genre in practice.

**Mitigation**:
- REP diminishing returns system forces variety (implemented in ProgressionManager)
- Cross-discipline style chains reward switching (testable via playtests)
- Synergy bonuses require multi-discipline builds (data-driven, tunable)
- Balance via playtesting: If 80%+ of players stick to one discipline, increase penalties for repetition.

**RISK 3: Rival AI feels dumb or scripted**

**Severity**: High
**Likelihood**: Medium
**Impact**: The Nemesis System clone falls flat. Rivals become forgettable.

**Mitigation**:
- Heavy investment in personality variance (25-30 rivals, each unique)
- QA focus: "Tell me about your most memorable rival." If answers are generic, system needs work.
- Iterate on attribute weights (Pride, Grudge, Confidence) until emergent stories happen
- Fallback: If emergent AI doesn't work, hand-script 5-6 key rivalries (narrative beats) and let the rest be procedural flavor.

**RISK 4: Performance doesn't hit 60fps on Steam Deck**

**Severity**: High
**Likelihood**: Medium
**Impact**: Steam Deck is primary validation target. Miss this, game feels bad on portable.

**Mitigation**:
- Profile on Steam Deck hardware monthly (borrow/buy devkit)
- Use Steam Deck as minimum spec for all performance tuning
- LOD system, texture compression, draw call reduction all target Steam Deck first
- Resolution scaling: If 800p doesn't hit 60fps, drop internal res to 720p and upscale (URP supports this)
- Worst case: Lock to 30fps on Steam Deck and optimize later. 30fps is playable for these genres (not ideal, but not a killer).

**RISK 5: Scope creep kills the project**

**Severity**: Critical
**Likelihood**: High (multi-genre games always scope creep)
**Impact**: Never ship.

**Mitigation**:
- Locked feature list (this doc defines MVP)
- Monthly scope reviews: "What can we cut to ship sooner?"
- Every feature has a "must-have" or "nice-to-have" tag
- Nice-to-haves get cut at month 9 if schedule slips
- Hard deadline: 18-month dev cycle. Ship whatever we have at month 18, even if incomplete.

### 7.2 Secondary Risks

**RISK 6: Unity version bugs**

**Mitigation**: Use LTS version (2022.3). Don't upgrade mid-dev. Test on target platforms monthly.

**RISK 7: Third-party dependencies break**

**Mitigation**: Vet all dependencies before integration. Avoid experimental packages. Have fallback plans (e.g., if DOTween breaks, write simple lerp system).

**RISK 8: Save data corruption**

**Mitigation**: JSON is human-readable and version-controllable. Implement save file versioning (schema version number). On load, check version and migrate if needed. Always keep backup save.

**RISK 9: Multiplayer requests from community**

**Mitigation**: Ship single-player first. Explicitly communicate "multiplayer not planned for 1.0" to avoid expectations. If game succeeds, consider async multiplayer (rival sharing) as DLC.

**RISK 10: Balancing economy is impossible**

**Mitigation**: Data-driven design (all costs/earnings in ScriptableObjects). Playtest with spending logs. Iterate costs/earnings until median playtime-to-purchase ratio hits target (45-75 min per meaningful purchase).

---

## 8. Development Pipeline

### 8.1 Version Control

**System**: Git + GitHub

**Branch strategy**: Trunk-based development
- `main` branch: Always shippable (or close to it)
- Feature branches: Short-lived (1-2 weeks max)
- No long-lived dev branches (they rot)

**Unity-specific Git setup**:
- `.gitignore`: Exclude `Library/`, `Temp/`, `Logs/`, `obj/`, `Builds/`
- LFS for large files: `.fbx`, `.png`, `.psd`, `.wav`, `.ogg`, `.mp3`
- Text-based scene serialization (Unity's YAML mode for scenes/prefabs)
- Smart Merge tool for `.unity` and `.prefab` files

**Commit discipline**:
- Commit every working feature (not every line of code)
- Commit message format: `[System] What changed` (e.g., `[Racing] Added drift state machine`)
- No broken builds on `main`. If build breaks, revert immediately.

### 8.2 Build System

**Build targets**:
- Windows x64 (primary)
- Linux x64 (for Steam Deck validation)
- (Later: macOS if easy, console if successful)

**Build automation**: GitHub Actions for CI/CD

**Build pipeline**:
1. On push to `main`: Trigger build job
2. Unity Cloud Build or local Jenkins server runs build
3. Build outputs to artifact storage (AWS S3 or similar)
4. Smoke test: Launch build, load first district, check for crashes
5. If smoke test passes, deploy to internal testing (Steam private branch)
6. If smoke test fails, alert team (Slack/Discord webhook)

**Daily builds**: Automated build every night at 2am. Morning standup: team tests yesterday's build.

**Build versioning**: Semantic versioning (e.g., 0.5.12)
- Major: Big milestones (0 = alpha, 1 = shipped)
- Minor: Feature complete (each discipline = +0.1)
- Patch: Bug fixes / iterations

### 8.3 Testing Strategy

**Testing pyramid**:
1. **Unit tests** (bottom layer): Core systems (ProgressionManager, StyleMeterManager)
   - Unity Test Framework (NUnit)
   - Target: 80% coverage of logic code (not MonoBehaviours, just C# logic)
2. **Integration tests** (middle layer): Discipline systems (does racing event start and end correctly?)
   - Play-mode Unity tests
   - Target: One test per discipline per major feature
3. **Manual playtests** (top layer): Full gameplay sessions
   - Internal team: Daily
   - External testers: Weekly (once vertical slice exists)

**Continuous testing**: Run unit tests on every commit (GitHub Actions). If tests fail, build fails.

**Playtesting protocol**:
- Weekly playtest: 1 hour session, structured feedback form
- Questions: "What was fun? What was frustrating? What was confusing?"
- Metrics: Record REP/CASH earned, disciplines played, rivals encountered
- Iterate based on feedback (prioritize "confusing" fixes first - confusion kills retention)

### 8.4 Asset Pipeline

**Art assets**:
- Models: FBX from Blender/Maya
- Textures: PNG source, Unity auto-compresses to BC7
- Animations: FBX with embedded anims (Unity imports as AnimationClips)

**Audio assets**:
- Source: WAV (44.1kHz, 16-bit)
- Unity imports and compresses to Vorbis on build

**Pipeline tools**:
- Blender for modeling (free, scriptable)
- Substance Painter for texturing (if budget allows; else Photoshop/GIMP)
- Audacity for audio editing (free)
- FMOD or Wwise for advanced audio (if needed; else Unity's built-in audio)

**Asset naming convention**:
```
Cars/
  CivicEG_Body.fbx
  CivicEG_Albedo.png
  CivicEG_Normal.png

Characters/
  PlayerMale_Rig.fbx
  PlayerMale_Idle.anim
  PlayerMale_Punch.anim
```

Consistent naming prevents chaos. Enforce in code reviews.

### 8.5 Documentation

**Internal docs**:
- This tech architecture doc (living document, update as decisions change)
- System-specific docs (e.g., "Racing Physics Implementation Notes")
- Code comments for non-obvious logic (not every line, just tricky parts)

**Player-facing docs**:
- In-game tutorial (interactive, not text walls)
- Steam store page (screenshots, GIFs, feature list)
- (Optional) Wiki for community (let players document synergies and builds)

**Doc format**: Markdown files in repo (`/docs` folder). Easy to version-control, easy to read.

---

## 9. Third-Party Dependencies

### 9.1 Critical Dependencies

**1. Unity Engine 2022.3 LTS**
- License: Pro license ($2k/year per seat) - necessary for dark theme and profiler features
- Risk: Unity's pricing changes (2023 fiasco). Mitigation: Lock to LTS, avoid Unity's runtime fee (under install threshold for indie game).

**2. Steamworks.NET**
- Purpose: Steam integration (achievements, cloud saves, input)
- License: Open source (MIT)
- Risk: Steam API changes. Mitigation: Use stable Steamworks SDK, don't rely on experimental features.

**3. Newtonsoft Json.NET**
- Purpose: Save data serialization (better than Unity's JsonUtility)
- License: MIT
- Risk: Low. Stable library.

**4. DOTween (or LeanTween)**
- Purpose: UI animations, camera transitions
- License: Free version available (paid for pro features)
- Risk: Low. Widely used, stable.
- Fallback: Write simple lerp/easing system if dependency breaks.

**5. Cinemachine**
- Purpose: Camera system (discipline-specific cameras, transitions)
- License: Unity package (free)
- Risk: Low. Maintained by Unity.

**6. Unity Input System**
- Purpose: Controller input handling
- License: Unity package (free)
- Risk: Low. Replaces old Input Manager.

### 9.2 Nice-to-Have Dependencies

**7. Odin Inspector** (optional)
- Purpose: Better inspector for ScriptableObjects (designer QOL)
- License: Paid ($55)
- Risk: Budget. Can live without it but slows designer iteration.

**8. Post-Processing Stack v2** (or URP's built-in post)
- Purpose: CRT shader, bloom, film grain
- License: Unity package (free)
- Risk: Low. Use URP's built-in if PPS v2 has issues.

**9. TextMesh Pro**
- Purpose: UI text rendering (sharper than Unity's legacy Text)
- License: Unity package (free, integrated into Unity)
- Risk: None. TMPro is standard.

**10. FMOD or Wwise** (optional)
- Purpose: Advanced audio (beat-synced music, dynamic mixing)
- License: Free for indie (under revenue threshold)
- Risk: Integration complexity. Only use if Unity's audio can't handle beat-sync requirements.
- Fallback: Unity's audio with custom beat detection (FFT analysis).

### 9.3 Dependency Management

**Policy**: Minimize dependencies. Every dependency is a liability.

**Vetting process**:
1. Is this dependency solving a problem we can't solve in 1-2 days?
2. Is the dependency actively maintained?
3. Is the license compatible (MIT, Apache, Unity's license)?
4. What's the fallback if this dependency breaks?

If answers are yes/yes/yes/concrete-plan, proceed. Otherwise, write it ourselves or cut the feature.

**Dependency updates**: Lock dependency versions. Don't auto-update. Update only if:
- Critical bug fix
- Feature we need
- Security patch

Test thoroughly after updating.

---

## 10. Implementation Roadmap

### 10.1 Phase 1: Prototype (Months 0-3)

**Goal**: Prove one discipline is fun.

**Deliverables**:
- Racing system vertical slice
  - One district (simplified geometry)
  - Player car + 3 AI opponents
  - Basic drift physics
  - Style Meter prototype
  - 60fps on target hardware
- Tech foundation
  - Unity project setup
  - Git repo + CI pipeline
  - Core architecture (GameDirector, EventManager state machines)
  - ScriptableObject pipeline for cars/events

**Team focus**: Programmer + designer working tight loop on racing feel.

**Milestone**: Playable racing demo that passes "one more race" test.

### 10.2 Phase 2: Multi-Discipline Integration (Months 4-6)

**Goal**: Prove genre-switching works.

**Deliverables**:
- Fighting system vertical slice
  - Frame-data-driven combat
  - Basic combo system
  - One rival fight
- Basketball system prototype
  - 2v2 pickup game
  - Crossover mechanic
- Cross-discipline Style Meter carry-over
- Garage/customization UI (basic version)
- One full district with all three disciplines represented

**Team focus**: Expand to 2 programmers (one on disciplines, one on systems).

**Milestone**: Demo with race -> fight -> ball sequence, Style Meter persistent across all three.

### 10.3 Phase 3: Core Loop (Months 7-12)

**Goal**: Full progression loop works.

**Deliverables**:
- Full progression system (REP, CASH, tier unlocks)
- Rival AI system (personality attributes, grudge/respect)
- Four districts (geometry + events)
- Tricks system (fourth discipline)
- Crew management (basic version)
- Full customization (cars, moves, skills, fashion)
- Save/load system + Steam Cloud

**Team focus**: Full team (2-3 programmers, 1-2 artists, 1 designer).

**Milestone**: Playable from start to first district boss, full loop intact.

### 10.4 Phase 4: Content & Polish (Months 13-16)

**Goal**: Fill the world, smooth the edges.

**Deliverables**:
- All 25-30 rivals implemented with unique personalities
- All 100+ events placed in districts
- Narrative beats (underground-vs-mainstream tension)
- Audio implementation (music, SFX)
- CRT shader + post-processing polish
- UI/UX polish (menus, results screens, garage)
- Performance optimization (hit 60fps on Steam Deck consistently)

**Team focus**: Content creation (artists) + bug fixing (programmers).

**Milestone**: Feature-complete build, ready for beta testing.

### 10.5 Phase 5: Beta & Launch Prep (Months 17-18)

**Goal**: Ship it.

**Deliverables**:
- External beta test (50-100 players)
- Bug fixes from beta feedback
- Balance tuning (economy, difficulty)
- Steam store page (screenshots, trailer, description)
- Launch build
- Day-one patch plan (assume we'll find bugs post-launch)

**Team focus**: Everyone on QA and launch prep.

**Milestone**: 1.0 ships on Steam.

---

## 11. Post-Launch Considerations

**Support plan**:
- Monitor Steam forums, Discord, Reddit for major bugs
- Patch critical bugs within 1 week (game-breaking issues)
- Patch balance issues within 1 month (economy, difficulty tuning)
- Content updates (new rivals, districts, disciplines) as paid DLC if game succeeds

**Metrics to track**:
- Steam CCU (concurrent users)
- Average session length (target: 60-90 minutes)
- Discipline usage rates (are all four disciplines played equally?)
- Completion rate (what % of players reach credits?)
- REP distribution (where do players plateau?)

**Success criteria**:
- 10k units sold in first month = break even
- 50k units in first year = profitable
- 100k+ units = greenlight for sequel or major DLC

**Failure criteria**:
- <5k units in first month = flop. Learn lessons, move on.
- <50% positive reviews = fundamental design issue. Post-mortem and fix or abandon.

---

## 12. Conclusion

UNDERGROUND is ambitious. Four game genres, unified progression, emergent AI rivalries, PS2 aesthetic with 2026 tech. The complexity is the point - no one has done this before.

But complexity kills projects. So we scope ruthlessly, prototype relentlessly, and profile constantly. Unity + ECS + ScriptableObjects + CI/CD. Build one discipline at a time. Validate fun before integration. Ship something playable every two weeks. Profile before optimizing. Trust the data, not our instincts.

The architecture is designed for iteration. State machines for game flow. ScriptableObjects for data. Addressables for content streaming. ECS for hot paths. MonoBehaviour for everything else. It's not the fanciest stack. It's the stack that ships.

What's the simplest version? Racing + fighting in one district with basic progression. That's the three-month milestone. If that's fun, we build out. If it's not, we pivot or cut. We don't bet the farm on a vision. We bet on iteration speed and tight loops.

Risks are real. Four genres is scope creep incarnate. But the mitigation is clear: cut features before cutting quality. If tricks don't hit the bar, they become DLC. If basketball feels like a minigame, we cut it. Three tight disciplines beats four loose ones.

Performance is non-negotiable. 60fps on Steam Deck. That's the floor. LODs, batching, texture compression, object pooling - all the boring optimizations that make games run. We profile monthly on target hardware. If we're not hitting 60fps by month 9, we cut visual features until we do.

This doc is a living document. Decisions will change. Systems will be cut. But the philosophy doesn't change: ship working software, make it right, then make it fast. In that order.

Let's build the 2000s street culture game that never got made. One discipline at a time. One commit at a time. One build at a time.

Ship it.

---

**Next steps**:
1. Set up Unity project (2022.3 LTS)
2. Initialize Git repo with proper `.gitignore` + LFS
3. Build racing physics prototype (week 1-2)
4. Playtest racing loop (week 3)
5. Iterate until "one more race" test passes
6. Repeat for each discipline

**Document version**: 1.0
**Next review**: After racing vertical slice completion (month 3)
**Owner**: BYTE (Lead Programmer)

---

*Code speaks louder than words. Now let's write some code.*
