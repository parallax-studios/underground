# UNDERGROUND -- Game Design Document

**Author**: REED (Game Designer)
**Status**: First Pass -- Ready for Internal Review
**Version**: 1.0
**Date**: 2026-02-07

---

## 1. Player Fantasy

### Fantasy Statement

**"You are nobody. The city doesn't know your name. But tonight, on this street, in this race, this fight, this game -- you will make them remember."**

The player fantasy is *becoming legendary through self-expression*. Not just winning, but winning with style. Not just climbing, but defining the climb on your own terms. The emotional throughline is the transformation from invisible to undeniable -- and the dangerous question of what you sacrifice to stay there.

This is not a power fantasy in the traditional sense. The player does not start weak and become a god. They start *unseen* and become *unmissable*. The difference matters. A god controls the world. A legend controls the room. UNDERGROUND is about controlling the room.

### The Feeling at Each Stage

| Hour | The Player Feels |
|------|-----------------|
| 0-1 | Hungry. Small. The city is alive and doesn't care about you. Your car rattles. Your punches lack weight. But there's a spark -- one good drift, one clean cross-up -- and you taste it. |
| 5-10 | Competent. Dangerous in one discipline. NPCs start using your name. Your car sounds right. You've found a combo you like. The hunger shifts from survival to ambition. |
| 10-20 | Known. You own a district. Rivals seek you out. Your build has a thesis -- speed, flash, brutality, finesse. The systems start talking to each other. |
| 20-40 | Feared or respected. The city bends around your reputation. The underground-vs-mainstream tension forces real choices. Your crew is a reflection of who you've been. |
| 40+ | Legendary. You're not playing the game -- you're composing it. Cross-discipline chains feel like jazz. The question stops being "can I win?" and becomes "how do I want to be remembered?" |

What's the loop? At every stage, the answer is: **read, react, express, earn, build, escalate.** The verbs don't change. The stakes do.

---

## 2. Core Loop Architecture

### 2.1 The 30-Second Loop (Moment-to-Moment)

The atomic unit of gameplay. Regardless of discipline, the 30-second loop follows the same cognitive pattern:

```
  +------------------+
  |  READ THE FIELD  |  <-- Observe: What's the situation? Where's the opening?
  +--------+---------+
           |
           v
  +------------------+
  | CHOOSE YOUR MOVE |  <-- Decide: Safe play or risky style move?
  +--------+---------+
           |
           v
  +------------------+
  |  EXECUTE + FLAIR |  <-- Act: Timing, precision, expression
  +--------+---------+
           |
           v
  +------------------+
  | FEEDBACK + SCORE |  <-- Feel: Style points, crowd noise, meter fill,
  +--------+---------+       screen effects, controller rumble
           |
           v
  +------------------+
  | RISK/REWARD CALC |  <-- Loop: Did I gain enough style to justify the risk?
  +--------+---------+       Can I chain this into the next action?
           |
           +----------> [BACK TO READ THE FIELD]
```

**Discipline-specific expression of the 30-second loop:**

- **Racing**: Read the corner approach --> Choose drift angle vs. clean racing line --> Execute the drift/pass --> Feedback: drift score, near-miss bonus, underglow flare, tire smoke --> Assess: Did I gain position AND style?
- **Fighting**: Read opponent's stance/tell --> Choose counter, combo, or taunt --> Execute with timing window --> Feedback: hit impact, style meter spike, crowd roar, knockback distance --> Assess: Am I building toward a finisher or overextending?
- **Street Sports (Basketball)**: Read defender's position --> Choose crossover, pass, or drive --> Execute with rhythm timing --> Feedback: ankle-breaker slow-mo, swish sound, crowd eruption --> Assess: Do I keep the ball or pass for an assist chain?
- **Freestyle Tricks**: Read the environment geometry --> Choose trick type and link --> Execute with rotation/timing --> Feedback: trick name pop-up, combo counter, grind sparks --> Assess: Do I land clean or push for one more link?

The critical design principle: **every discipline must ask the same core question -- "Do I play safe or play stylish?" -- and reward style disproportionately.** Safe play keeps you alive. Style makes you legendary.

### 2.2 The 5-Minute Loop (Event Level)

```
  +---------------------+
  |  ENTER STREET EVENT  |  <-- Choose or stumble into an event on the map
  +---------+-----------+
            |
            v
  +---------------------+
  |   PERFORM + STYLE   |  <-- 2-4 minutes of active gameplay (the 30s loop repeating)
  +---------+-----------+
            |
            v
  +---------------------+
  |   RESULTS SCREEN    |  <-- Win/Loss + Style Rating (D through S rank)
  +---------+-----------+       REP earned, CASH earned, Rival reaction
            |
            v
  +---------------------+
  |   SPEND / EQUIP     |  <-- Quick garage/locker room: upgrade, equip, tune
  +---------+-----------+
            |
            v
  +---------------------+
  |    WORLD REACTS     |  <-- Rival mood shifts, new events unlock,
  +---------+-----------+       phone rings with crew intel, district REP updates
            |
            v
  +---------------------+
  | CHOOSE NEXT ACTION  |  <-- Roam to next event, respond to rival challenge,
  +---------------------+       pursue crew mission, or free-roam
```

Each event takes 2-4 minutes of active play. The results screen, spending, and world reaction take 30-90 seconds. Total 5-minute loop target: 3-5 minutes. The player should always be within one minute of the next meaningful decision.

### 2.3 The Session Loop (30-60 Minutes)

```
  +---------------------------+
  |    CHOOSE A DISTRICT      |  <-- Each district has a dominant discipline,
  +------------+--------------+       a boss, and a reputation threshold
               |
               v
  +---------------------------+
  |  WORK THE STREETS (x5-8)  |  <-- Complete 5-8 events (5-min loops)
  +------------+--------------+       Mix of discipline types, rival encounters
               |
               v
  +---------------------------+
  |  DISTRICT BOSS UNLOCKS    |  <-- Hit REP threshold --> Boss issues challenge
  +------------+--------------+
               |
               v
  +---------------------------+
  |   BOSS EVENT (SHOWDOWN)   |  <-- High-stakes multi-phase event
  +------------+--------------+       (e.g., race then fight, or ball then tricks)
               |
               v
  +---------------------------+
  |   DISTRICT CLAIMED OR     |  <-- Win: Claim turf, unlock rewards, crew grows
  |   DEFEAT + REGROUP        |  <-- Lose: Rival gloats, new path to retry,
  +------------+--------------+         but the world remembers you lost
               |
               v
  +---------------------------+
  |  NARRATIVE BEAT / CHOICE  |  <-- Story progression, crew drama,
  +---------------------------+       underground-vs-mainstream tension escalates
```

A full session should feel like one "episode" of the player's legend. They arrive in a district as an outsider, work the streets, attract attention, face the boss, and emerge changed. Every session should end with the player knowing exactly what they want to do next.

---

## 3. Core Mechanics -- Detailed Design

### 3.1 STYLE METER (Universal System)

**Player verb**: Play with flair.
**System description**: A universal meter (0-1000 points) that fills from stylish actions across all four disciplines. The meter has four tiers:

| Tier | Points | Name | Effect |
|------|--------|------|--------|
| 0 | 0-249 | COLD | No bonus. You're performing, nobody's watching. |
| 1 | 250-499 | WARM | +10% REP gain. Crowd starts reacting. Subtle visual glow on character. |
| 2 | 500-749 | HOT | +25% REP gain. Crowd is loud. Rival AI becomes more aggressive or more cautious. Visual: underglow intensifies, camera pulls back slightly to show the spectacle. |
| 3 | 750-999 | ON FIRE | +50% REP gain. Time-window for inputs becomes slightly more forgiving (+80ms). Crowd is deafening. Visual: full screen color saturation, film grain shifts, beat drops. |
| MAX | 1000 | UNDERGROUND MODE | Triggered manually when meter is full. 12-second window: +100% REP, slowed time perception (15% slow-mo), enhanced move properties (wider drift angle, longer stun on hits, guaranteed ankle-breakers, higher trick multiplier). Meter drains completely after use. |

**Meter gain rates (base values, before modifiers)**:
- Clean drift (per second): +15
- Near-miss (traffic/obstacle): +40
- Fight combo (3+ hits): +20 per hit after 2nd
- Taunt (during fight, leaves you vulnerable for 1.2s): +60
- Crossover/ankle-breaker: +35
- Alley-oop/assist play: +45
- Trick link (per additional trick in combo): +25
- Discipline switch bonus (performing in a different discipline than your last event within 10 minutes): +100 flat

**Meter decay**: The meter decays at -8 points/second when no stylish action has occurred for 4 seconds. This means the player must maintain a flow state to reach UNDERGROUND MODE. Passive play bleeds your meter dry. The system rewards momentum and punishes hesitation.

**Feedback**: The meter is displayed as a vertical bar on screen-left, styled like a neon tube sign that literally "heats up" through blue -> yellow -> orange -> red -> white. At UNDERGROUND MODE, the entire HUD flickers like a CRT overloading. Sound design shifts: bass intensifies, high-hats sharpen, the soundtrack's mix changes to emphasize the beat.

**Depth**: Mastery of the Style Meter is the skill ceiling of the entire game. Expert players will learn to:
- Time their UNDERGROUND MODE activation for maximum REP (triggering it during a boss event's climax)
- Chain style across disciplines using the switch bonus as a "style battery"
- Manage decay by routing through the city to minimize downtime between events
- Use taunts strategically (high risk/high reward, especially in fights)

Where's the depth? It's in understanding that the Style Meter is a resource management problem disguised as a spectacle system. The player who treats it as "cool stuff happens when I'm flashy" will enjoy the game. The player who treats it as "I need to optimize my style-per-second across a session to maximize REP throughput" will master it.

### 3.2 REP SYSTEM (Progression Currency)

**Player verb**: Build your name.
**System description**: REP is the unified progression metric. It functions as XP, gating currency, and NPC relationship modifier simultaneously.

**REP Sources:**

| Source | Base REP | Style Multiplier Applied? | Notes |
|--------|----------|--------------------------|-------|
| Event win | 100 | Yes | Scales with event difficulty tier |
| Event loss (style) | 20-50 | Yes | Partial REP if you lost with style (B rank or higher) |
| Rival defeat | 150-500 | Yes | Scales with rival's own REP rank |
| Boss defeat | 500-1000 | Yes | One-time large bonus per district |
| First-time event type | 75 | No | Bonus for trying a new discipline or event variant |
| Crew mission complete | 200 | Partial (50%) | Crew missions are story-gated |
| Style milestone | 50 | No | "First S-rank in racing", "First 10-hit combo", etc. |

**Diminishing Returns (Anti-Grind Mechanic)**:
Repeating the same event type in the same district within a session yields progressively less REP:
- 1st event: 100% REP
- 2nd same-type: 80% REP
- 3rd same-type: 50% REP
- 4th+ same-type: 25% REP

This resets per session and per district. The system actively pushes the player to diversify and explore. A player who only races will plateau. A player who races, then fights, then balls will accelerate. This is the core economic incentive for cross-discipline play.

**REP Tiers and World Reaction:**

| REP Total | Tier Name | World State |
|-----------|-----------|-------------|
| 0-999 | NOBODY | NPCs ignore you. Events are low-stakes. Rivals don't bother. |
| 1,000-4,999 | LOCAL | Named NPCs start recognizing you. One district's events are accessible. Tier-1 rivals engage. |
| 5,000-14,999 | KNOWN | Two districts open. Crew recruitment available. Rival AI actively seeks you out. The phone rings with opportunities. |
| 15,000-34,999 | FEARED | Three districts open. District bosses acknowledge you. Promoters approach (mainstream tension begins). Named rivals evolve behaviors. |
| 35,000-74,999 | LEGENDARY | All districts accessible. The underground-vs-mainstream choice point triggers. Boss events become multi-phase. |
| 75,000+ | KING / ICON | Endgame state. The city shapes itself around you. Legacy challenges unlock. |

**REP Loss**: You do not lose REP for losing events (losing should not feel punishing enough to discourage experimentation). However, declining a rival's direct challenge costs 200 REP -- the underground does not respect cowardice. Losing to a rival you challenged costs no REP but boosts the rival's confidence and aggression.

### 3.3 CASH ECONOMY (Short-Term Spending)

**Player verb**: Gear up.
**System description**: CASH is the short-loop spending currency. Earned alongside REP from events but on a separate track.

**Cash Sources**: Every event pays CASH (50-300 base, scaled by event difficulty). Side bets with rivals pay double or nothing. Selling old parts/gear at 40% value.

**Cash Sinks**:
- Car parts (engine, suspension, tires, nitrous, body kits, paint, underglow): 100-5000 per item
- Fighting movesets (new combos, counters, taunts, finishers): 200-3000 per move
- Street sports skills (crossover packages, dunk packages, shot styles): 200-2500 per skill
- Trick loadouts (new tricks, grind styles, grab variations): 150-2000 per trick
- Fashion (clothing, accessories -- purely cosmetic but affects crowd reaction by +5-15%): 50-1500 per item
- Car repairs (damage from races persists until repaired): 50-500

**Economic Balance Target**: The player should be able to afford one meaningful upgrade every 2-3 events. They should never have enough CASH to buy everything they want, forcing choices that shape their build identity. At any given time, a player should be choosing between 3-4 tempting purchases.

**Inflation Control**: Event payouts scale with district difficulty tier but costs also scale. A Tier-3 district event pays 3x a Tier-1 event, but Tier-3 gear costs 4x Tier-1 gear. This keeps the economic pressure consistent throughout the game.

### 3.4 BUILD SYSTEM (Customization-as-Mastery)

**Player verb**: Define your legend.
**System description**: Every purchasable item has stats that create real mechanical tradeoffs, not just cosmetic differences.

**Car Build Axes:**

| Axis | Low End | High End | Tradeoff |
|------|---------|----------|----------|
| Weight | Light (quick acceleration, fragile) | Heavy (slow start, better drift momentum) | Speed vs. drift style |
| Grip | Low (slidey, drift-oriented) | High (planted, racing-line oriented) | Style vs. consistency |
| Nitrous | Burst (one massive shot) | Sustained (slow burn) | Risk vs. reliability |
| Visual Flash | Subtle | Maximum underglow/body kit | +Style meter gain rate vs. rival attention/targeting |

**Fighter Build Axes:**

| Axis | Low End | High End | Tradeoff |
|------|---------|----------|----------|
| Speed | Slow (heavy hits, long recovery) | Fast (quick jabs, low damage) | Burst vs. sustain |
| Flash | Technical (efficient, low style gain) | Flashy (big openings, high style gain) | Safety vs. spectacle |
| Stance | Counter (reactive, bonus on reads) | Pressure (aggressive, bonus on initiative) | Defense vs. offense |

**Street Sports Build Axes:**

| Axis | Low End | High End | Tradeoff |
|------|---------|----------|----------|
| Handling | Tight control (safe plays) | Loose/flashy (trick moves, risk of turnover) | Consistency vs. highlight reel |
| Playmaking | Solo scorer (high personal output) | Team facilitator (assist bonuses, crew synergy) | Individual glory vs. crew REP |

**Trick Build Axes:**

| Axis | Low End | High End | Tradeoff |
|------|---------|----------|----------|
| Complexity | Simple (easy to land, low score) | Complex (hard timing, high score) | Reliability vs. ceiling |
| Chain Length | Short combos (consistent) | Long combos (exponential scoring, crash risk) | Safety vs. explosive payoff |

**Cross-Discipline Synergies (The Deep Layer)**:

This is where the build system becomes a strategy game. Specific combinations of equipment and skills across disciplines unlock **Synergy Bonuses**:

- *Drift King + Ankle Breaker*: If your car is drift-tuned AND you have the flashy crossover package, your Style Meter carries 25% more when switching between racing and basketball.
- *Counter Fighter + Technical Racer*: If your fighting stance is counter AND your car grip is high, you gain a "Patience" passive: +10% REP from events where you never dropped below second place or took fewer hits than your opponent.
- *Showboat Universal*: If your car visual flash is maxed, your fighting style is flashy, AND your trick complexity is high, your base Style Meter gain rate increases by 15% across all disciplines.

There are 15-20 of these synergies in the game. They are not surfaced in a menu -- players discover them through play and community knowledge-sharing. This is the layer that gives the game legs at hour 40 and beyond.

### 3.5 RIVAL AI SYSTEM (Emergent Antagonists)

**Player verb**: Make enemies. Earn respect.
**System description**: Every named NPC rival is driven by an AI personality model with the following attributes:

**Rival Attributes:**

| Attribute | Range | Effect |
|-----------|-------|--------|
| Pride | 0-100 | High pride: refuses to back down, escalates grudges. Low pride: pragmatic, will ally. |
| Respect (for player) | -100 to +100 | Negative: hostile, ambushes, trash-talks. Positive: offers alliance, shares intel. |
| Confidence | 0-100 | High: challenges you to their best discipline. Low: avoids you, or fights dirty. |
| Grudge | 0-100 | Accumulates from losses. At high grudge, rival becomes obsessed: appears more often, brings backup, targets your weaknesses. |
| Style Affinity | Archetype tag | Defines their preferred discipline and playstyle. "Drift purist," "Brawler," "Showboat," "Technician." |

**Rival Behavior Rules:**

1. **After player wins**: Rival's Respect +10 if player showed style (A rank or higher). Rival's Grudge +15 if player humiliated them (taunted, S rank, or won by massive margin). Rival's Confidence -10.
2. **After player loses**: Rival's Confidence +15. Rival's Respect -5 (they think less of you). If rival won with style, player's Grudge toward rival increases (narrative flavor text: "That one stung").
3. **Grudge threshold (70+)**: Rival enters "Obsessed" state. They will interrupt your events (crash your race, invade your fight). They study your build and counter it -- if you're drift-heavy, they bring a grip car. If you're a counter-fighter, they use pressure tactics. This is the Nemesis System's revenge mechanic.
4. **Respect threshold (60+)**: Rival offers an alliance. They can be recruited to your crew. As crew members, they provide passive bonuses aligned with their Style Affinity and can be called in for assist moves during events.
5. **Breaking point**: If a rival's Confidence hits 0 while their Grudge is above 50, they "break." They leave the district, appear later in a different context (maybe working for the mainstream antagonists), fundamentally changed. This is permanent and narrative.

**Rival Roster**: Each district has 4-6 named rivals plus 1 boss. Total named rival count: 25-30 across the game. Each has a unique visual design, voice lines, car/build identity, and personality attribute spread. No two rivals feel the same.

How does this feel at hour 20? By hour 20, the player has a web of relationships. A rival they humiliated early has become obsessed and is now a genuine threat. A rival they respected is now a loyal crew member. A rival they ignored has gotten stronger in another district. The game's social landscape is unique to each playthrough.

### 3.6 DISCIPLINE SWITCHING (Genre Fluidity)

**Player verb**: Be everything.
**System description**: The player can engage in any available event regardless of discipline. The map always displays events across all four types. There are no genre-locking mechanics.

**Cross-Discipline Style Chain**: When the player completes an event in one discipline and immediately (within 10 minutes of game-time) enters an event in a different discipline, they receive:
- +100 flat Style Meter points (starting the new event with momentum)
- A "Flow State" buff for the first 30 seconds of the new event: +20% Style Meter gain rate
- If they chain three different disciplines in a row (e.g., Race -> Fight -> Ball), the third event grants a "Triple Threat" bonus: +200 REP on completion regardless of performance

This system makes the optimal path through the city a varied one. The player who specializes deeply in one discipline can still progress, but the player who flows between all four is rewarded with faster REP growth and higher style ceilings.

**Discipline Proficiency**: Each discipline tracks an independent proficiency level (1-10). Higher proficiency unlocks:
- New move/part slots (proficiency 3, 5, 7)
- Advanced techniques within the discipline (proficiency 4, 6, 8)
- Discipline-specific legendary challenges (proficiency 9-10)

Proficiency levels by playing: roughly 1 proficiency level per 3-4 events completed in that discipline. A player who evenly splits time across all four disciplines will hit proficiency 5-6 in each by hour 20. A specialist might hit 8-9 in one but only 2-3 in others.

---

## 4. Systems Interaction Map

```
                         +------------------+
                         |   STYLE METER    |
                         | (Universal Fuel) |
                         +--------+---------+
                                  |
                   Feeds into     |     Feeds into
              +-------------------+-------------------+
              |                   |                   |
              v                   v                   v
     +--------+------+   +-------+-------+   +-------+--------+
     | REP EARNINGS  |   | UNDERGROUND   |   | CROWD REACTION |
     | (Multiplied)  |   | MODE TRIGGER  |   | (Audio/Visual) |
     +--------+------+   +-------+-------+   +-------+--------+
              |                   |                   |
              v                   |                   v
     +--------+------+           |           +-------+--------+
     | REP TIER      |           |           | RIVAL AI       |
     | PROGRESSION   |           |           | (Mood Shifts)  |
     +--------+------+           |           +-------+--------+
              |                   |                   |
              v                   v                   v
     +--------+------+   +-------+-------+   +-------+--------+
     | DISTRICT      |   | IN-EVENT      |   | GRUDGE /       |
     | UNLOCKS       |   | ADVANTAGE     |   | RESPECT        |
     +--------+------+   +-------+-------+   +-------+--------+
              |                                       |
              v                                       v
     +--------+------+                       +-------+--------+
     | BOSS ACCESS + |                       | CREW RECRUIT / |
     | STORY BEATS   |                       | RIVAL ESCALATE |
     +---------------+                       +----------------+

     +------------------+         +------------------+
     |   CASH ECONOMY   | <-----> |   BUILD SYSTEM   |
     | (Earned from     |         | (Spend to        |
     |  events)         |         |  customize)      |
     +--------+---------+         +--------+---------+
              |                            |
              v                            v
     +--------+---------+        +--------+---------+
     | ECONOMIC PRESSURE |        | STAT TRADEOFFS   |
     | (Can't buy all)   |        | (Define identity)|
     +--------+---------+        +--------+---------+
              |                            |
              +----------------------------+
              |
              v
     +--------+---------+
     | SYNERGY BONUSES  |
     | (Cross-discipline|
     |  build rewards)  |
     +------------------+
```

### Positive Feedback Loops (Snowball Potential)

1. **Style -> REP -> Access -> Higher-Tier Events -> More Style Opportunities**: Playing well accelerates progression, which unlocks harder content that rewards even more. Risk: The skilled player rockets ahead. Mitigation: Diminishing REP returns on repeated events and the discipline-variety incentive.

2. **Rival Grudge Escalation**: Beating a rival makes them come back harder, which means a harder fight, which means more REP if you win again. Risk: Spiral of difficulty. Mitigation: Broken rivals exit the loop. New, fresh rivals replace them at calibrated difficulty.

3. **Synergy Discovery -> Faster Style -> Faster REP**: A player who discovers a cross-discipline synergy earns style faster, which means more REP, which means faster access to gear that enables more synergies. Risk: Knowledge gap between informed and uninformed players. Mitigation: Synergies provide 10-25% bonuses, not 200%. They accelerate, not break.

### Negative Feedback Loops (Rubber Banding)

1. **Diminishing REP Returns**: The system actively discourages grinding one event type, forcing the player outward into less comfortable disciplines where they're less efficient.

2. **Rival Adaptation**: Rivals who lose to the player study the player's build and counter it. A player who never varies their approach will face increasingly hard-countered opponents.

3. **Economic Pressure**: Gear costs scale faster than earnings, preventing the player from ever feeling "done" with their build. There's always a next upgrade just out of reach.

4. **Style Meter Decay**: The meter punishes passivity. You can't bank style and coast. You must maintain momentum, which keeps the player in a state of active engagement rather than comfortable dominance.

---

## 5. Progression Curves

### 5.1 Difficulty Curve

The difficulty model is **stepped with controlled spikes**, not linear:

```
Difficulty
    ^
    |                                          ________
    |                                   ______/  BOSS 4
    |                            ______/
    |                     ______/  BOSS 3
    |              ______/
    |       ______/  BOSS 2
    |______/
    | BOSS 1
    |_______________________________________________> Time (hours)
    0     5     10    15    20    25    30    35
```

Each district represents a plateau of consistent difficulty with a spike at the boss event. Between districts, difficulty resets slightly (the new district's street-level events are easier than the previous boss) before climbing again. This creates breathing room.

**Boss events are the skill checks.** They are multi-phase encounters that test cross-discipline competence. The Southside boss (racing-dominant district) doesn't just race you -- he races you, then steps out and fights you if you win. The Docks boss doesn't just fight -- she fights, then challenges you to tricks on the warehouse structures. Players must be at least passable in multiple disciplines to clear a boss.

### 5.2 Content Introduction Pacing

| Hours | New Mechanics Introduced | New Content Unlocked |
|-------|-------------------------|---------------------|
| 0-1 | Primary discipline choice (tutorial in chosen discipline), basic Style Meter | Starting district, 4-6 starter events |
| 1-3 | Second discipline introduced (gentle tutorial), CASH spending, first garage/locker access | 2-3 new event variants, first named rival appears |
| 3-5 | Third discipline introduced, Rival system explained (first grudge forms), crew concept introduced | Second district partially accessible, 3 new rivals |
| 5-8 | Fourth discipline introduced, cross-discipline style chain explained, first synergy hint | Full second district, boss event accessible |
| 8-12 | Build system depth opens (advanced parts/moves), rival recruitment possible | Third district, crew missions begin |
| 12-18 | Underground Mode strategy deepens, rival obsession mechanic, side bet system | Fourth district, promoter approaches (story pivot) |
| 18-25 | Mainstream vs. underground choice, advanced synergies, legacy challenges | Full map, endgame events, all bosses accessible |
| 25+ | Mastery content: S-rank hunting, all-synergy builds, rival collection, legacy runs | Post-story freeplay, challenge modes |

The rule: **never introduce more than one major system per 2-3 hours of play.** Each new system gets a dedicated event that teaches it, then 3-5 events that test it, before the next system is layered on.

### 5.3 Discipline Proficiency Progression

```
Proficiency
    ^
  10|                                              *
   9|                                         *
   8|                                    *
   7|                              *
   6|                        *
   5|                  *
   4|            *
   3|       *
   2|    *
   1| *
    +-----------------------------------------> Events in Discipline
    0  3  6  9  12 15 18 21 24 27 30
```

Roughly linear with slight diminishing returns at higher levels. Proficiency 1-5 comes fast (3-4 events each). Proficiency 6-8 requires 5-6 events each. Proficiency 9-10 requires 8-10 events each and specific challenge completions. This means:

- A generalist hitting proficiency 5 in all four disciplines: approximately 48-64 events (roughly 16-20 hours)
- A specialist hitting proficiency 10 in one discipline: approximately 50-55 events in that discipline (roughly 17-18 hours of focused play)

Both paths reach the endgame at similar total playtimes, but with very different capability profiles.

---

## 6. Economy Design

### 6.1 Currency Flow Model

```
  EVENTS -----> CASH (80-300 per event, average 150)
    |                |
    |                v
    |          PARTS / MOVES / GEAR
    |           (100 - 5000 each)
    |                |
    |                v
    |          BUILD IDENTITY
    |           (Tradeoffs define playstyle)
    |
    +-------> REP (50-500 per event, average 120 before style multiplier)
                   |
                   v
              TIER PROGRESSION
               (Gates content and narrative)
```

### 6.2 Earning and Spending Targets by Game Phase

| Phase | Avg CASH/Hour | Key Purchase Target | Hours to Afford |
|-------|---------------|--------------------|-----------------|
| Early (0-5h) | 600-900 | Tier-1 car part (300-500) | 0.5-0.8h |
| Mid (5-15h) | 1200-1800 | Tier-2 part or new move (800-1500) | 0.7-1.0h |
| Late (15-25h) | 2000-3000 | Tier-3 part or advanced moveset (2000-3500) | 0.8-1.2h |
| Endgame (25h+) | 3000-4500 | Legendary items (4000-5000) | 1.0-1.5h |

The target: **one meaningful purchase every 45-75 minutes of play.** The player should never feel "rich" (nothing left to buy) or "starved" (hours between purchases). The ideal emotional state is "I can afford one of three things I want -- which one defines my build best?"

### 6.3 Sink Balance

Total CASH to buy everything in the game (estimated): 180,000-220,000
Total CASH earned in a full playthrough (40 hours): 80,000-100,000
**Completion ratio: 40-55%**

This means a single playthrough lets the player acquire roughly half of all available gear. This is intentional -- it forces build identity (you ARE your choices) and provides replay value (second playthrough explores different builds).

### 6.4 Side Bet System

Before certain rival events, the player can propose a side bet:

| Bet Level | Cost | Payout (Win) | Payout (Lose) |
|-----------|------|-------------|---------------|
| Low Stakes | 100 CASH | 200 CASH | 0 (lose bet) |
| High Stakes | 500 CASH | 1200 CASH | 0 (lose bet + rival Confidence boost) |
| Pink Slip | Your equipped item | Rival's equivalent item | Lose your item permanently |

Pink slip bets are the high-risk, high-reward end of the economy. Winning a rival's legendary part through a pink slip bet is one of the most memorable moments in the game. Losing your own is devastating -- but the underground remembers your courage, awarding a +50 REP "Gambler's Respect" consolation.

---

## 7. Difficulty and Balance Framework

### 7.1 Difficulty Philosophy

UNDERGROUND is not a hard game. It is a **deep** game. The difference: a hard game blocks progress behind skill walls. A deep game rewards investment with layers of mastery. Any player should be able to see credits. The question is how stylishly they did it.

### 7.2 Adaptive Difficulty (Hidden)

The game tracks a rolling performance score per discipline based on the player's last 5 events:

| Avg Style Rank | Difficulty Adjustment |
|----------------|---------------------|
| D-C average | -1 tier (events become easier: slower rivals, wider timing windows, less aggressive AI) |
| C-B average | Neutral (calibrated baseline) |
| B-A average | +0.5 tier (rivals sharpen up, timing windows tighten 10%) |
| A-S average | +1 tier (rivals at full aggression, optimal pathing, counter-build behavior) |

This adjustment is **invisible**. The player should never feel patronized or punished. They should feel that "tonight the streets are tougher" or "I'm really in the zone." The tuning is subtle -- a 10-15% swing in rival competence, not a genre shift.

### 7.3 Per-Discipline Balance Targets

**Racing:**
- Average race duration: 90-120 seconds (3 laps on a city circuit)
- Position spread: Player should finish top-3 at calibrated difficulty, top-1 with strong play
- Drift scoring should account for 30-50% of style gains in a race (pure position-focused racing should still earn style, but less)
- Nitrous usage: 2-3 uses per race, each giving 1.5-2 seconds of speed boost

**Fighting:**
- Average fight duration: 60-90 seconds
- Health pools: player and rival should trade 4-6 exchanges before a KO at calibrated difficulty
- Combo timing windows: 300ms (generous) for basic links, 150ms (precise) for advanced links, 80ms (frame-tight) for style links
- Taunt window: 1.2 seconds of vulnerability for +60 style -- this should feel genuinely risky against competent rivals

**Street Sports (Basketball):**
- Average game duration: 90-120 seconds (first to 11 points, 1s and 2s)
- AI team (2v2 format): AI partner competence scales with player's Style Rank
- Crossover success rate at calibrated difficulty: 60-70% base, 85-95% with correct timing input
- Turnover punishment: lose ball possession + 3-second recovery, enough to feel bad but not game-ending

**Freestyle Tricks:**
- Average session: 90-120 seconds (score attack format)
- Trick timing windows: 400ms (generous) for basic tricks, 200ms for advanced, 100ms for legendary
- Bail punishment: lose current combo multiplier + 2 seconds of recovery time
- Score target for A rank: top 75th percentile of possible score in the time limit
- Score target for S rank: top 95th percentile, requiring near-perfect chaining

### 7.4 Cross-Discipline Balance

The most critical balance question: **are all four disciplines equally viable paths to progression?**

Target: A player focused on any single discipline should be able to reach LEGENDARY REP tier in approximately the same number of hours, assuming equal skill. The diminishing returns system handles REP-per-hour parity. The discipline proficiency system ensures depth in every path.

However, the game explicitly rewards breadth. A player proficient in all four disciplines will reach LEGENDARY roughly 15-20% faster than a pure specialist, due to cross-discipline chain bonuses and variety REP multipliers. This is intentional -- the game's fantasy is being a complete street legend, not a narrow specialist. But the specialist path must remain viable and satisfying.

---

## 8. Risk Assessment

### High-Risk Items

| Risk | Severity | Likelihood | Mitigation |
|------|----------|------------|------------|
| **Jack of all trades, master of none**: Each discipline feels shallow compared to a dedicated genre game | Critical | High | Each discipline must have its own depth tree with proficiency 1-10 mastery curve. Target depth: each discipline should feel as tight as a mobile game's core loop -- not as deep as a full genre entry, but deeper than a minigame. If any discipline fails the "would I play 30 minutes of just this?" test, it needs redesign. |
| **Onboarding overwhelm**: Four genres + Style Meter + REP + CASH + Rivals + Builds is too many systems | High | High | Staggered introduction over 8-12 hours. Opening hour has ONE discipline, ONE meter, ONE currency. Each new system gets a dedicated teaching event. The player should never encounter a system they haven't been taught. |
| **Style-over-substance trap**: Players feel forced to be flashy and can't enjoy playing "their way" | High | Medium | Safe play must remain viable for progression. Style is a multiplier on REP, not a requirement. A C-rank player still earns REP. The incentive to be stylish is acceleration, not gating. No content should be locked behind style rank requirements. |
| **Rival AI feels scripted**: The "emergent" rivalry system feels predictable or repetitive | High | Medium | Invest heavily in personality variation. 25-30 named rivals with distinct attribute spreads. Randomize initial encounters. QA focus: after 20 hours, does the player have at least 3 rivalries that feel personal and distinct? If not, the attribute system needs more variance. |
| **Economic dead zones**: Player accumulates too much or too little CASH at certain phases | Medium | Medium | Playtest with spending logs. Track median CASH balance at each hour mark. If balance exceeds 2x the next purchase target, costs are too low or earnings too high. If balance stays below 0.3x, the player is resource-starved. Target: balance hovers at 0.6-1.2x next purchase. |
| **Cross-discipline switching friction**: Transitioning between genres feels jarring, not fluid | Medium | Medium | Shared control philosophy: all disciplines use the same "read-react-express" input cadence. Style Meter is the continuity thread. The camera and audio transitions must be polished -- 2-3 second cinematic handoff between disciplines, never a hard cut. |
| **Boss difficulty spikes**: Multi-phase boss events feel unfair because the player is strong in one phase and weak in another | Medium | High | Boss events telegraph their phases in advance ("He'll race you, then he'll want to scrap"). The player can prepare their build. If a player fails a boss 3 times, offer a "focus challenge" -- beat the boss in just their dominant discipline, but for reduced REP. This is the "accessibility door," not the "front door." |

### Medium-Risk Items

| Risk | Severity | Likelihood | Mitigation |
|------|----------|------------|------------|
| REP grind feels mandatory before fun content | Medium | Medium | Front-load interesting events. The first district boss should be accessible within 3-4 hours. No REP gate should require more than 2 hours of focused play to clear. |
| Style Meter decay feels punishing to explorers | Medium | Low | Decay only activates during events, not during free-roam. Players exploring the city are never punished. The meter pauses outside active event contexts. |
| Synergy system is too hidden | Low | Medium | Introduce the concept of synergies explicitly at hour 8-10 with a tutorial event that grants one synergy. Subsequent synergies remain discoverable but the player knows to look for them. |
| Fashion/cosmetic system feels irrelevant | Low | Medium | Cosmetics affect crowd reaction (+5-15% Style Meter gain from crowd). This gives fashion a mechanical edge without being mandatory. A naked car can still win -- but a fly car earns more doing it. |

---

## 9. Open Playtesting Questions

These are the questions I cannot answer at the desk. They require hands on controllers and eyes on players.

### Priority 1: Test Immediately (Prototype Phase)

1. **Does the 30-second loop feel good in EACH discipline independently?** Before anything else, each discipline needs to pass the "one more round" test in isolation. If racing isn't fun without the meta-game, it won't be fun with it. Build four standalone prototypes. Test them separately. If any one fails, stop and fix it before integration.

2. **Does the Style Meter reward feel proportional to the risk?** Taunting in a fight should feel dangerous AND rewarding. If the +60 style doesn't feel worth the 1.2-second vulnerability window, the numbers are wrong. Playtest the exact moment of taunt-into-punish vs. taunt-into-payoff. The ratio should be roughly 30% punish, 70% payoff for a well-timed taunt.

3. **Is the cross-discipline transition jarring or exciting?** Record player faces during the first race-to-fight transition. If they look confused, the camera work and control handoff need iteration. If they grin, ship it.

### Priority 2: Test Early (Vertical Slice Phase)

4. **Does the diminishing REP return system feel like guidance or punishment?** Players should feel "Oh, I should try something different" not "The game is punishing me for having fun." Watch for frustration signals when the 4th same-type event pays 25%. If players express anger rather than curiosity, soften to 40%.

5. **Do rival personalities feel distinct after 10 hours?** Give 10 testers 10 hours. Ask each to describe their most memorable rival. If they describe the same generic "tough enemy," the attribute system lacks variance. If they tell unique stories ("This guy kept showing up at my basketball games even though he's a racer -- he was desperate"), the system works.

6. **Is the economic pressure motivating or stressful?** Track when players check their CASH balance. If they check constantly and frown, the economy is too tight. If they never check because they always have enough, it's too loose. The ideal: they check when they see something they want, do mental math, and make a choice that feels meaningful.

### Priority 3: Test in Beta

7. **How does this feel at hour 20?** The critical question. Is the player still discovering new things? Have their rivalries evolved? Is their build meaningfully different from hour 10? Or has the game settled into a routine? Watch for the "autopilot" moment -- when the player stops making intentional choices and starts going through motions. That moment must be pushed past hour 25 at minimum.

8. **Does the underground-vs-mainstream choice feel genuine?** At the narrative fork, do players actually agonize? Or do they pick the "obviously correct" option? If 90% of players pick the same path, the other path lacks sufficient incentive. Target: 40/40/20 split (underground/mainstream/both).

9. **Are there dominant strategies that collapse build variety?** If every optimized player converges on the same car setup, the same fighting style, the same trick loadout, the tradeoff system has failed. Track build diversity across the top 20% of playtesters by performance. Target: no single build should account for more than 25% of high-performers.

10. **What do players do in freeplay after credits?** If they immediately start a new save to try a different build, the game has succeeded. If they put the controller down and never return, the endgame content loop needs work. If they keep playing the same save and hunting S-ranks, the mastery curve is working.

---

## 10. Design Pillars Summary

Every design decision in UNDERGROUND must be tested against these five pillars:

1. **Style IS substance.** How you do something matters as much as whether you did it. Every system must reward expression, not just execution.

2. **One identity, four languages.** The player is the same legend whether they're drifting, fighting, balling, or tricking. The Style Meter is the Rosetta Stone. No discipline should feel like a different game -- they should feel like different sentences in the same language.

3. **The city remembers.** Rivals evolve. REP accumulates. Choices matter. No action exists in a vacuum. The emergent narrative from the Rival AI and REP systems should make every player's story unique.

4. **Depth, not difficulty.** The game should be completable by a casual player in 30-40 hours. The mastery content should sustain an invested player for 80-100 hours. The difference is not harder walls -- it's deeper systems to explore.

5. **Never figure out the fun later.** If the 30-second loop in any discipline doesn't pass the "one more round" test as a standalone experience, no amount of meta-game, narrative, or progression will save it. Fun first. Everything else is amplification.

---

## Appendix A: Notation Reference

- **REP**: Reputation points (progression currency, earned not spent)
- **CASH**: Spending currency (earned and spent)
- **Style Meter**: Universal performance meter (0-1000, four tiers + UNDERGROUND MODE)
- **Proficiency**: Per-discipline mastery level (1-10)
- **Style Rank**: Per-event performance grade (D, C, B, A, S)
- **REP Tier**: Overall progression gate (NOBODY through KING/ICON)

## Appendix B: Comparable Design References

| System | Reference Game | What We Take | What We Change |
|--------|---------------|--------------|----------------|
| Style Meter | Tony Hawk's SPECIAL meter | Universal meter that enables power moves | Ours works across genres, decays actively, and multiplies progression |
| Rival AI | Shadow of Mordor's Nemesis System | AI personalities that remember and adapt | Ours tracks respect AND grudge separately, allows recruitment, and spans four game genres |
| Discipline Switching | Yakuza's minigame integration | Multiple activities in one open world | Ours treats every discipline as a first-class system with deep progression, not a minigame |
| Build Synergies | Balatro's joker combinations | Hidden synergies between build elements | Ours span across genres, rewarding cross-discipline investment |
| REP Diminishing Returns | Roguelike entropy mechanics | Discouraging repetition | Ours uses it to push genre variety rather than just difficulty |
| Economic Pressure | Darkest Dungeon's resource tension | Never enough to buy everything | Ours forces build identity rather than punishing failure |

---

*This document represents REED's first-pass design. Every number is a starting point. Every system is a hypothesis. The game will be found in playtesting -- but this is the map we carry into the fog.*

*What's the loop? Read, react, express. In every discipline, at every scale, from the 30-second drift to the 30-hour legend. That's UNDERGROUND.*

---

**Document version**: 1.0
**Next review**: After prototype of individual discipline loops
**First playtest target**: Single-discipline vertical slice (racing recommended as most immediately legible genre)
