# UNDERGROUND — Level Design Document

**Authored by GRID, Level Designer**
**Version 1.0 — Spatial Foundation**
**Date**: 2026-02-07

*"Where does the player LOOK? Where does the player MOVE? That's the entire game."*

---

## I. CORE SPATIAL PHILOSOPHY

### The Underground Is a Stage, Not a World

This isn't GTA. We're not building sprawl. We're building density. Every street, every alley, every arena exists to teach the player something about movement, about flow, about where they stand in the hierarchy. The city is a navigation puzzle disguised as an open world. Where you CAN go tells you who you ARE.

The player's journey through the Underground is measured in sightlines. At hour zero, they can't see past the next corner. At hour five, they can read a district from the underglow glow on wet pavement three blocks away. At hour twenty, they know which rooftop to watch from, which alley shortcut connects Southside to Old Town, where the crowds gather before an event even starts. **Level design IS the progression curve.**

### Movement Is Identity

The four disciplines aren't just mechanics. They're languages of space.

- **Racing** teaches the player to read speed: approach angles, drift zones, nitrous windows. Racing spaces are corridors with rhythm — straightaway, corner, straightaway, hairpin. The best racing levels are songs you drive through.
- **Fighting** teaches the player to read distance: engagement range, retreat paths, crowd pressure. Fighting spaces are circles with texture — walls that block escape, elevation that creates drama, lights that make shadows you can use.
- **Street Sports** teaches the player to read geometry: court dimensions, passing lanes, dunk approach vectors. Sports spaces are grids with asymmetry — one hoop is backlit, one defender always plays too tight, the crowd spills onto the court at Midtown.
- **Freestyle Tricks** teaches the player to read structure: grindable edges, launch ramps, linkable surfaces. Trick spaces are playgrounds where every object is a verb.

When a player moves from racing to fighting to streetball to tricks in a single session, they're not switching genres. They're code-switching languages of spatial cognition. The level design must make this feel natural. The shared grammar is momentum and risk.

### The City Teaches Without Teaching

No tutorials delivered through text boxes. The environment is the teacher. A drift race through tight alleys with neon guides teaches drift control. A fight in a narrow container stack teaches spacing and retreat. A streetball court lit unevenly teaches shot timing by making one side harder. A trick line through the Heights that requires three linked grinds teaches combo thinking.

The player should never feel lectured. They should feel like they figured it out. That's level design doing its job silently.

---

## II. DISTRICT DESIGN FRAMEWORK

Each district is a spatial lesson. A player who masters a district has learned a movement vocabulary they'll use forever.

### District 01: Southside (The Drag)

**PURPOSE**: Teach racing. Teach speed. Teach the foundational loop. Southside is the tutorial district for most players — even if they choose a different discipline to start, Southside is visually the entry point.

**EMOTIONAL BEAT**: Hunger. Southside makes you feel small and fast. The streets are wider than you, the cars around you are better than yours, but the road doesn't care. The road is the great equalizer. You can win here even when you're nobody.

#### Spatial Structure

```
                      [KING'S GARAGE]
                            |
        +-------------------+-------------------+
        |                                       |
   [RAIL YARDS]                          [INDUSTRIAL ROW]
   (Early Races)                         (Drift Focus)
        |                                       |
        +-------------------+-------------------+
                            |
                    [THE STRIP - Main Drag]
                            |
                    [OLD TOWN - Hub]
```

**The Strip** is Southside's spinal column. A two-mile straightaway lined with shuttered storefronts and graffiti-tagged loading docks. At night, underglow turns it into a neon river. This is where you LOOK first when you arrive in Southside. The Strip is always visible from elevated positions in the district — it's the landmark, the compass rose.

**Rail Yards** are the entry-level racing circuit. Wide lanes, gentle turns, minimal traffic. Forgiving. The lesson here is "stay on the gas, learn the corner timing." Three-lap circuit, 90 seconds per lap. The first time the player drifts successfully, it should be here, on Turn 4, where the rail crossing forces a wide approach. The drift tutorial is environmental: you MUST slide to maintain speed through this turn, so the player discovers drifting organically.

**Industrial Row** is the mid-tier challenge. Tighter streets, sharper turns, 90-degree intersections. The lesson: "drift to maintain speed through technical sections." This is where the player graduates from competent to stylish. Industrial Row has the highest near-miss opportunities — parked trucks, light poles, container corners. Risk is rewarded. Safe racing plateaus here.

**King's Garage** sits at the district's northern edge, elevated slightly so you look DOWN on the Strip when you're there. Visual hierarchy: King is above you until you're not below him anymore. His garage is the spatial goal. When you can access it freely, you've conquered Southside.

#### Flow Diagram: The Strip (Main Event Space)

```
START (South End)
    |
    v
[==========LONG STRAIGHTAWAY (0.8 mi)==========]
    |  Underglow reflections on wet asphalt
    |  Widest section - room for 4-wide racing
    |  Speed zone - nitrous is earned here
    |
    v
[OVERPASS SECTION - Slight elevation, tighter]
    |  Lighting shifts: overhead fluorescents
    |  2-wide only - positioning matters
    |
    v
[THE HAIRPIN - 180-degree turn around old factory]
    |  DRIFT REQUIRED or massive speed loss
    |  Crowd gathers here - highest Style Meter gain
    |  Inner line vs outer line tradeoff
    |
    v
[RETURN STRAIGHTAWAY (1.2 mi) - Slight downhill]
    |  Fastest section of any track in the game
    |  Traffic spawns here - near-miss opportunities
    |
    v
FINISH (Back to start)
```

**Pacing Curve (The Strip race)**:

```
TENSION
  ^
  |                        ___
  |                   ____/   \___
  |              ____/            \___
  |         ____/                     \______
  |    ____/
  |___/
  +----------------------------------------> TIME (seconds)
  0   15   30   45   60   75   90   105

  0-15s:   Setup. You're positioning, testing the car.
  15-30s:  First straight. Speed builds. Confidence builds.
  30-45s:  Overpass. Tight. You're threading the needle.
  45-60s:  THE HAIRPIN. Peak tension. Make the drift or lose.
  60-75s:  Relief straight. You made it. Now maximize speed.
  75-90s:  Traffic spawns. Second tension spike. Near-misses.
  90-105s: Final push to finish. Style Meter should be near UNDERGROUND MODE.
```

The curve is never flat. Flat is boring. Flat is death.

#### Key Design Metrics (Southside Racing)

- **Average race duration**: 90-120 seconds (3 laps)
- **Track width (straight sections)**: 4-car widths (enough for passing, not enough to ignore positioning)
- **Track width (technical sections)**: 2-car widths (forces decisions)
- **Drift scoring zones**: 6-8 per lap (corners that reward style over pure racing line)
- **Traffic density**: 3-5 moving vehicles per lap on higher difficulty
- **Underglow visibility range**: 2-3 city blocks (you can SEE events before you reach them — visual breadcrumbing)

#### Breadcrumbing Strategy

- **Neon as Navigation**: Underglow, storefront signs, and street art create visual trails to event start points. The brightest light is always significant — either an event, a shop, or a rival.
- **Sound Layering**: Bass increases in volume as you approach active events. The soundscape is directional. Close your eyes and you can still find the race.
- **NPC Density**: Crowds cluster at event locations. Follow the people, find the action.
- **King's Gaze**: From King's Garage, you have a panoramic view of Southside's active events marked by distant light columns (like The Division's flares). The spatial hierarchy is literal: the boss sees everything.

---

### District 02: The Docks (The Cage)

**PURPOSE**: Teach fighting. Teach spacing. Teach consequence. The Docks are where the player learns that position matters more than speed.

**EMOTIONAL BEAT**: Weight. The Docks feel heavy — concrete, rust, standing water. Your footsteps echo. The camera is lower, tighter. This is where you learn to measure distance in arm's reach, not blocks.

#### Spatial Structure

```
            [BISHOP'S CONTAINER FORTRESS]
                        |
        +---------------+---------------+
        |                               |
   [DRY DOCKS]                    [WAREHOUSE ROW]
   (Small Rings)                  (Large Arena)
        |                               |
        +---------------+---------------+
                        |
                [THE FREIGHTER - Main Venue]
                        |
                [OLD TOWN - Hub]
```

**The Freighter** is a derelict cargo ship permanently docked at the center of the district. Its hold has been converted into a fighting pit. Descending into the ship is a spatial threshold: you enter at street level, walk down two flights of rusted stairs, and emerge in a circular space lit by work lights strung from the ceiling. The descent is narrative — you're going DOWN into the Underground literally.

The hold is 30 feet in diameter. Three tiers of spectators ring the space on scaffolding bolted to the walls. The floor is painted concrete with a spray-painted circle. There are no ropes, no barriers. The crowd IS the cage. If you get pushed into the crowd, they shove you back. Hard.

**Elevation creates drama**: Fighters on the bottom, crowd above. When you win, you look UP at them cheering. When you lose, you stare at the floor while they jeer.

#### Flow Diagram: The Freighter (Main Fighting Venue)

```
STREET LEVEL
    |
    v
[Entry Door - Red light above it]
    |
    v
[Hallway - Narrow, claustrophobic]
  | Graffiti: fighter names, records, threats
  | Sound muffled until you reach the stairs
  |
  v
[Stairwell - Descending, sound SWELLS]
  | This is the entrance music moment
  | You hear the crowd before you see the ring
  |
  v
[THE HOLD - Fighting Pit]
  | 30-foot diameter circle
  | Concrete floor, slight texture (affects footwork)
  | Crowd on three levels (scaffolding)
  | Single overhead light (creates harsh shadows)
  | No escape route - fight or lose
```

**Sightlines in Fighting Spaces**: The Freighter's hold has NO long sightlines. Everywhere you look, there's a wall, scaffolding, or crowd. This spatial compression intensifies the fight. You can't escape visually or physically. Compare this to Midtown's open-air courts — the Docks teach PRESSURE.

#### Pacing Curve (The Freighter fight)

```
TENSION
  ^
  |     __        __              ___
  |    /  \      /  \            /   \
  |   /    \    /    \          /     \___
  |  /      \__/      \___  ___/
  | /
  |/
  +----------------------------------------> TIME (seconds)
  0   15   30   45   60   75   90

  0-15s:   Feeling out. You're reading the opponent's stance.
  15-30s:  First exchange. Someone lands a clean combo. Tension spikes.
  30-45s:  Reset. Both fighters retreat, circle. Crowd louder.
  45-60s:  Second exchange. This one's bigger. Finisher territory if one fighter dominates.
  60-75s:  If still going, desperation phase. Both health pools low. Crowd DEAFENING.
  75-90s:  Final exchange. Someone goes down.
```

Fights should NEVER go past 90 seconds at calibrated difficulty. If a fight hits 2 minutes, someone made a mistake (the designer or the player).

#### Key Design Metrics (Docks Fighting)

- **Arena diameter**: 30 feet (10 meters) — far enough to retreat, close enough that you're never safe
- **Crowd pressure depth**: 3 feet before shove-back mechanic activates (teaches players to control space)
- **Lighting**: Single-source overhead creates harsh shadows — fighter silhouettes are as important as models
- **Audio occlusion**: Sound is muffled outside the arena, deafening inside (spatial audio is critical to immersion)
- **Camera distance**: 15% closer than racing or sports (intimacy and violence)
- **Floor texture**: Slight grip variation — center is smooth, edges near the crowd are grittier (subtly punishes being pushed to the edge)

#### Encounter Breakdown: Bishop (Final Boss Fight)

**WHERE**: The Freighter's hold, but modified. Bishop's fight is at night during a rainstorm. Water drips through the ceiling. The floor is slick. Footing is unstable — not mechanically punishing, but visually/aurally different. The crowd is silent for the first 30 seconds. They've seen Bishop do this too many times.

**WHY HERE**: The Freighter is where Bishop has never lost. Fighting him here is symbolic. The space is his. You're taking it.

**WHAT CHANGES**: The crowd's scaffolding is packed tighter than any other fight. There are 200 people in a space meant for 100. The camera is slightly wider to capture the scale. When Bishop enters, the crowd parts. He doesn't walk down the stairs. He's already in the ring. He lives there.

**PHASE STRUCTURE**:
- **Phase 1 (60 seconds)**: Bishop fights defensively. He's testing you. The lesson: patience. You cannot rush him. The crowd is silent, judging both of you.
- **Phase 2 (60 seconds)**: Bishop shifts to aggression. He stops testing and starts finishing. The crowd starts chanting his name. This is the difficulty spike. The lesson: adaptation. Your Phase 1 strategy won't work here.
- **Phase 3 (conditional)**: If the fight goes past 2 minutes, Bishop gets SLOWER but hits HARDER. His age is showing. The crowd's chant falters. This is the narrative beat — Bishop is human. The lesson: endurance. Outlast him.

**VICTORY CONDITION**: Bishop goes down. But the spatial storytelling is in what happens next. The crowd doesn't cheer. They go quiet. Then one person claps. Then another. They're applauding both fighters. You didn't just beat Bishop. You EARNED the Docks. The space is yours now.

#### Breadcrumbing Strategy

- **Acoustic Wayfinding**: Fight sounds (impacts, crowd roars) carry across the Docks. Follow the noise.
- **Graffiti as Lore**: Every wall has fighter records spray-painted on it. Names, W-L records, dates of last fights. You read the district's history by walking through it.
- **Light as Invitation**: Active fighting rings are lit. Inactive rings are dark. Simple. Effective. Never confusing.
- **Bishop's Presence**: His container fortress is ALWAYS visible from any elevated position in the Docks — three stacked containers with his symbol (a chess piece) painted 20 feet tall. Spatial hierarchy. He is the king until you take the crown.

---

### District 03: Midtown (The Court)

**PURPOSE**: Teach street sports. Teach rhythm. Teach crowd dynamics. Midtown is where the player learns that an audience isn't just scenery — it's a game system.

**EMOTIONAL BEAT**: Electricity. Midtown feels ALIVE in a way the other districts don't. The crowds are bigger, louder, younger. The courts are outdoors, public-facing. This is the most vulnerable district to commercialization, and you feel it — camera flashes, phones recording, the line between underground and overground blurring in real-time.

#### Spatial Structure

```
            [THE PENTHOUSE - Visible in distance]
                        |
        +---------------+---------------+
        |                               |
   [WEST COURT]                   [EAST COURT]
   (Intro level)                  (Advanced)
        |                               |
        +---------------+---------------+
                        |
                [THE CAGE - Main Court]
                        |
            [TRICK'S TERRITORY - Crew HQ]
                        |
                [OLD TOWN - Hub]
```

**The Cage** is THE court. The legendary space. It's an outdoor basketball court surrounded by a 12-foot chain-link fence (hence "Cage"). Four public housing towers ring it on all sides, creating an amphitheater effect. People watch from their apartment windows, balconies, fire escapes. The court itself is standard dimensions (94 feet by 50 feet) but feels smaller because the fence compresses the space.

**The fence is participatory**: When a player drives to the basket, the crowd presses against the fence, making it rattle and bow. This isn't just visual — it's audio storytelling. The fence SOUNDS like a living thing. When the crowd goes quiet (rare, but it happens when a newcomer does something impossible), the absence of the fence-rattle is LOUD.

**Lighting is asymmetric**: One end of the court is lit by streetlights. The other end is lit by floodlights someone rigged to the tower's electrical panel. This creates a visibility gradient. Shooting from the dark end toward the lit end is harder (backlit hoop). This isn't a bug — it's teaching shot timing under varied conditions.

#### Flow Diagram: The Cage (Main Streetball Venue)

```
[ENTRY GATE - Single opening in fence]
    |
    v
[THE COURT - 94' x 50' outdoor court]
  | Painted concrete (faded three-point line)
  | Two hoops (standard height, but rims are bent from dunks)
  | Crowd presses against all four sides of fence
  |
  | SPATIAL ZONES:
  | - Paint (key area) - crowded, physical
  | - Three-point arc - space to shoot, but defender pressure
  | - Baseline corners - tight, high-risk passing lanes
  |
[BENCH AREA - Outside fence, player side]
  | Where you wait between games
  | Where Trick sits when he's watching
  | Social hub between events
```

**Sightlines in Sports Spaces**: The Cage's genius is that the audience is VISIBLE from court-level. You see their reactions in real-time. When you cross someone over and break their ankles, you don't just hear the crowd — you SEE a kid on a fire escape lose his mind. This visual feedback makes the Style Meter feel earned.

#### Pacing Curve (The Cage - 2v2 game to 11 points)

```
TENSION / LEAD CHANGES
  ^
  |  __    __      ____
  | /  \  /  \    /    \  __
  |/    \/    \__/      \/  \___
  +----------------------------------------> TIME (seconds)
  0   20   40   60   80   100   120

  0-20s:    Feeling out. Both teams testing defenses. 2-2 score.
  20-40s:   First run. One team pulls ahead 6-4. Tension rising.
  40-60s:   Momentum shift. Defensive adjustment. Now 7-7.
  60-80s:   Peak tension. Score is 9-9. Next basket is critical.
  80-100s:  Final possessions. 11-9 or 11-10 finish.
  100-120s: Game over. Crowd reaction. Immediate challenge or exit.
```

Games to 11 should last 90-120 seconds. If a game goes past 2 minutes, the skill gap is too large (someone is dominating or being dominated — both are design failures at calibrated difficulty).

#### Key Design Metrics (Midtown Streetball)

- **Court dimensions**: Standard 94' x 50' (feels authentic)
- **Fence proximity**: 2-3 feet from court boundary (crowd feels CLOSE)
- **Crowd density**: 80-120 NPCs visible (more than any other event type — Midtown's identity is VOLUME)
- **Audio dynamic range**: Crowd volume ranges from 60 dB (ambient) to 95 dB (peak ankle-breaker moment) — the widest audio range in the game
- **Lighting asymmetry**: 40% brightness difference between lit and dark ends (teaches adaptability)
- **Camera height**: Slightly elevated (8-10 feet) to capture both the player and the crowd in the same frame

#### Encounter Breakdown: Trick (Boss - 1v1 Game)

**WHERE**: The Cage, midday. This is the ONLY major event that happens during daylight. The symbolism: Trick is the most public figure in the Underground. He doesn't hide. The sunlight is harsh, unforgiving. No neon, no underglow, no shadow. Trick plays in full view.

**WHY HERE**: Trick owns Midtown by consensus. He's not a tyrant like King or a force of nature like Bishop. He's the best, and everyone knows it, and everyone is fine with it because he's FUN. Playing him here is a spectacle.

**WHAT CHANGES**: The crowd is 3x normal size. People are on rooftops. There are cameras (the first time cameras explicitly appear in gameplay). Trick enters to APPLAUSE. You enter to... curiosity. The crowd doesn't know you yet.

**PHASE STRUCTURE**:
- **Phase 1 (0-5 points)**: Trick is LOOSE. He's not trying to dominate. He's performing — behind-the-back passes, unnecessary trick shots, taunting. He's putting on a show. The lesson: style matters. If you play boring basketball, you'll lose the crowd even if you score.
- **Phase 2 (5-9 points)**: The game is close. Trick tightens up. He stops performing and starts executing. His shot percentage goes up. His defense gets sharper. This is when you realize he's GOOD, not just flashy. The lesson: fundamentals under pressure.
- **Phase 3 (9-11 points)**: Game point territory. Trick goes back to performing — but now it's EARNED. He's not showboating. He's expressing mastery. The crowd is deafening. This is the peak Style Meter moment in Midtown.

**VICTORY CONDITION**: You hit 11 first. But the spatial storytelling is in Trick's reaction. He doesn't rage. He LAUGHS. He daps you up. The crowd cheers for both of you. Trick says something like, "You're ready. Question is, ready for what?" He's the first boss who doesn't feel defeated — he feels like he was testing you, and you passed.

#### Breadcrumbing Strategy

- **Crowd as Compass**: Active games draw crowds like gravity. You don't need a map. You follow the density of people.
- **Sound as Signal**: The rattle of the fence carries two blocks. You hear The Cage before you see it.
- **Visual Verticality**: Midtown is the only district where you should regularly LOOK UP. The audience is above you, around you. The spatial awareness is three-dimensional.
- **Trick's Presence**: When he's at The Cage (which is often), there's a LINE of people waiting to challenge him. The line itself is a breadcrumb. It says: this is where the best player in Midtown lives.

---

### District 04: The Heights (The Edge)

**PURPOSE**: Teach freestyle tricks. Teach creative navigation. Teach flow state. The Heights are where the city stops being a container and starts being an instrument.

**EMOTIONAL BEAT**: Freedom. The Heights feel OPEN in a way no other district does. You're not racing through corridors or fighting in cages. You're moving through three-dimensional space, treating stairs as ramps, rails as grind paths, walls as launch pads. This is the least "Underground" district aesthetically — it's residential, hilly, sunlit (when it's day). But it's the most underground philosophically: totally uncommercializable, totally personal, totally about self-expression.

#### Spatial Structure

```
            [NIX'S LOFT - Highest point]
                        |
        +---------------+---------------+
        |                               |
   [RESIDENTIAL HILLS]           [CONSTRUCTION SITE]
   (Natural terrain)             (Built environment)
        |                               |
        +---------------+---------------+
                        |
                [THE STAIRCASE - Iconic spot]
                        |
                [SILK'S HIDEOUT - Discoverable]
                        |
                [OLD TOWN - Hub]
```

**The Staircase** is the Heights' signature landmark. It's a public staircase that descends 200 feet down a hillside in a series of landings, rails, and switchbacks. Someone (probably Nix) has added improvised ramps and grind rails at every landing. The Staircase is the Heights' equivalent of The Strip or The Cage — the space everyone knows, where reputations are made.

**Verticality is identity**: The Heights are the only district where elevation changes CONSTANTLY. You're always going up or down. Tricks are rewarded for using vertical space — wall rides, roof gaps, drop-ins from height. The camera has to work harder here to communicate spatial relationships. The player needs to develop a sense of "what can I use?" when scanning an environment.

#### Flow Diagram: The Staircase (Main Trick Venue)

```
TOP LANDING (Elevation: +200 feet)
    |
    v
[Section 1 - 40 feet of stairs, metal rail on right]
  | Manual or grind to build combo
  |
  v
[Landing 1 - Flat platform with bench obstacle]
  | Ollie the bench for style or go around (safe)
  |
  v
[Section 2 - 50 feet of stairs, double rails]
  | Choose left rail (easier) or right rail (longer grind, higher multiplier)
  |
  v
[Landing 2 - Curved wall section]
  | Wall ride possible (high risk, high reward)
  |
  v
[Section 3 - 60 feet of stairs, gap in the middle]
  | MUST air the gap or crash — no safe option
  |
  v
[Landing 3 - Bowl-shaped depression]
  | Vert opportunity — air and grab for bonus
  |
  v
[Section 4 - Final 50 feet, narrow single rail]
  | Commitment grind — if you start, you finish or bail
  |
  v
BOTTOM LANDING (Elevation: +0 feet)
  | Crowd gathers here to watch
  | Bail = shame. Land clean = legend.
```

**The lesson of The Staircase**: Commitment. Unlike racing (where you can brake) or fighting (where you can retreat), tricks require commitment. Once you're in the air, once you're on the rail, you're locked in. The Heights teach the player to read space and commit BEFORE acting, not during. This is a different cognitive skill than the other disciplines.

#### Pacing Curve (The Staircase - Trick Run)

```
COMBO MULTIPLIER / RISK
  ^
  |                      ______
  |                    _/      \
  |              _____/         \
  |         ____/                 \___
  |    ____/
  |___/
  +----------------------------------------> TIME (seconds)
  0   10   20   30   40   50   60   70

  0-10s:    Entry. You're building speed, setting up.
  10-20s:   First grind. Combo starts. Confidence builds.
  20-30s:   Second section. Link trick. Multiplier grows.
  30-40s:   Wall ride. RISK SPIKE. If you land it, you're godlike. If you bail, you lose everything.
  40-50s:   Gap jump. Second risk spike. No safe option.
  50-60s:   Final grind. This is the closer. Maximum style.
  60-70s:   Land clean or crash. Binary outcome. Maximum tension.
```

Trick runs should be 60-90 seconds. Shorter than races or fights because the DENSITY of decisions is higher. Every second in a trick run requires a decision. Every second is risk.

#### Key Design Metrics (Heights Freestyle)

- **Vertical range**: 200+ feet in key trick zones (more than any other district — height IS the gameplay)
- **Grindable surfaces**: 60-80 distinct grind rails/ledges/walls in The Staircase alone (density of opportunity)
- **Bail punishment**: 2-second recovery + full combo reset (harsh but necessary — tricks must have stakes)
- **Camera behavior**: More dynamic than other disciplines — anticipates player trajectory, smooths during aerial tricks, zooms slightly during peak moments
- **Crowd placement**: Always at the bottom, looking UP (reverses the spatial hierarchy of fighting — here, you're elevated, they're below)

#### Encounter Breakdown: Nix (Boss - Timed Trick Challenge)

**WHERE**: The entire Heights district becomes the venue. Nix doesn't challenge you to beat her on a single line. She challenges you to EXPRESS YOURSELF across the district. It's a 3-minute free-roam trick session. Highest score wins. She goes first. You go second. The pressure is watching her run and knowing you have to top it.

**WHY HERE**: The Heights are about creativity, not domination. Nix's challenge respects that. She's not testing whether you can do a specific trick. She's testing whether you understand the HEIGHT's language.

**WHAT CHANGES**: During Nix's run, you're a spectator. The camera follows her. You watch her choose a line, link tricks, use parts of the district you've never considered. This is TEACHING through observation. When your turn comes, you can try to replicate her line (safe, but lower ceiling) or find your own (risky, but potentially higher score).

**PHASE STRUCTURE**:
- **Nix's Run (90 seconds)**: She sets the bar. Her score is shown at the end. It's JUST above what you've been averaging. It's beatable, but not easily.
- **Your Run (90 seconds)**: Free roam. You choose the path. The Heights district's full trick infrastructure is available. The lesson: mastery is personal. There's no "correct" route. The game tracks your score in real-time. You KNOW if you're ahead or behind.
- **Final 30 Seconds**: If you're behind, the Style Meter gain rate increases slightly (rubber-banding — we want close finishes, not blowouts). If you're ahead, Nix's ghost appears doing a second run in parallel (visual pressure — she's RACING you in a discipline where racing shouldn't exist).

**VICTORY CONDITION**: You outscore her. But the spatial storytelling is that Nix SMILES. She doesn't care that she lost. She cares that you FOUND A NEW LINE. After the event, new grind rails and ramps appear in the Heights — she's building new obstacles based on what you showed her. The district evolves.

#### Breadcrumbing Strategy

- **Elevation as Information**: The higher you are, the more you can see. Nix's loft (highest point) offers a panoramic view of all active trick zones (marked by small clusters of people).
- **Environmental Scanning**: Unlike other districts, the Heights require the player to actively LOOK for opportunities. Grindable edges are marked by slight wear textures and scuff marks (subtle, but learnable).
- **Nix's Influence**: She tags new trick obstacles with spray paint — a small symbol (三 — three horizontal lines, her signature). Following her tags leads to the best lines.
- **Silk's Hideout**: Unlocking Silk requires exploration. Her hideout is in a residential building that doesn't look special. The breadcrumb: a PARKED CAR in an alley, under a tarp, that's TOO NICE for this neighborhood. Investigate the car, find the building.

---

### District 05: Old Town (The Market)

**PURPOSE**: Social hub. Gear progression. Crew management. Old Town is the only district WITHOUT a dominant discipline. It's the neutral ground, the bazaar, the space between spaces.

**EMOTIONAL BEAT**: Belonging. Old Town feels WARM. It's the only district that feels safe. No rivalries here. No boss. Just shops, crews, Moms on the radio, and the diner that never closes.

#### Spatial Structure

```
        [KING'S GARAGE (Southside border)]
                        |
        +---------------+---------------+
        |                               |
   [VINYL PROPHECY]                [MACK'S DINER]
   (Moms's Radio HQ)               (Social Hub)
        |                               |
        +---------------+---------------+
                        |
                [MAIN STREET - Strip Mall Row]
                        |
        +---------------+---------------+
        |               |               |
   [GARAGE #1]    [GEAR SHOPS]    [GARAGE #2]
   (Car Mods)     (Fashion/Moves) (Car Mods)
```

**Main Street** is a half-mile stretch of shuttered and semi-active storefronts. The active businesses are the Underground's economy: garages for car mods, clothing shops for fashion, a barbershop where you overhear rumors, a pawn shop that sells fighting moves and trick gear. Everything here costs CASH or REP. Old Town is where you FEEL your progression through spending.

**Mack's Diner** is the social center. Open 24/7. Cheap food. Booths where crews meet. This is where you recruit crew members, where you overhear district gossip, where Trick might be sitting in a corner booth after a game, where Bishop never goes but everyone talks about him. Mack's is the game's social stealth tutorial: information is AMBIENT. The player learns to LISTEN.

**Vinyl Prophecy** is Moms's record store and pirate radio station. The front is a store (actually selling vinyl — some NPCs browse, creating ambient life). The back is the studio where Moms broadcasts. You can visit her between events. She comments on your recent performances, offers side quests, and provides the game's ONLY explicit moral guidance. Vinyl Prophecy is the player's narrative compass.

#### Flow Diagram: Old Town Loop (Session Structure)

```
[Finish Event in Any District]
    |
    v
[Return to Old Town - Automatic fast travel option offered]
    |
    v
[DECISION POINT: Where first?]
    |
    +-- [Garage] --> Spend CASH on car parts --> Check build
    |
    +-- [Gear Shop] --> Spend CASH on moves/clothes --> Check build
    |
    +-- [Mack's Diner] --> Check crew status --> Accept missions
    |
    +-- [Vinyl Prophecy] --> Talk to Moms --> Get narrative context
    |
    v
[Phone Rings - New Event Unlocked in X District]
    |
    v
[Choose Next Event - Fast travel or drive there]
```

Old Town is the BREATH between action beats. The pacing structure of the entire game flows through Old Town. Event -> Old Town -> Event -> Old Town. This rhythm prevents fatigue.

#### Key Design Metrics (Old Town)

- **Walking speed**: 25% slower than other districts (intentional — we want the player to OBSERVE, not rush)
- **NPC density**: Highest in the game (60-80 visible NPCs on Main Street — this place feels ALIVE)
- **Audio mix**: Music from car radios, Moms's broadcast, diner ambience, shop audio — layered, warm, busy
- **Shop accessibility**: All shops are within 200 meters of each other (no wasted time — the hub is DENSE)
- **Lighting**: Warmest in the game — tungsten streetlights, neon shop signs, diner windows glowing orange (visual contrast to the cooler, harsher lighting of competition districts)

#### Breadcrumbing Strategy

- **Moms as Oracle**: Her radio show TELLS YOU what's happening. "I'm hearing Bishop's been in the ring every night this week — someone's got him rattled." That's a narrative breadcrumb AND a gameplay hint (Bishop's Grudge score is rising — challenge him soon).
- **Phone as Quest Log**: The player's flip phone receives texts from rivals, crew, and Moms. The phone IS the quest system. It buzzes, you check it, you get information. Diegetic UI.
- **Visual Progression Markers**: As your REP grows, Old Town REACTS. Your crew's colors appear as graffiti. Shops stock higher-tier gear. NPCs greet you by name. The environment is a mirror of your progression.

---

### District 06: The Penthouse (Endgame Zone)

**PURPOSE**: The final test. The mainstream. The space where the player confronts the consequences of their choices. The Penthouse is NOT a traditional district. It's a thematic space that activates in Act 3.

**EMOTIONAL BEAT**: Dislocation. The Penthouse feels WRONG. It's clean. It's corporate. The crowds are different — tourists, influencers, people with lanyards and cameras. The lighting is even, professional, sterile. The Style Meter still works here, but it feels hollow. This is the game's spatial argument: authenticity cannot be transplanted.

#### Spatial Structure

```
                    [MARCUS'S OFFICE - Top Floor]
                            |
        +-------------------+-------------------+
        |                                       |
   [SANCTIONED RACE TRACK]              [TELEVISED FIGHT VENUE]
   (Corporate Racing)                   (Broadcast Cage)
        |                                       |
        +-------------------+-------------------+
                            |
                    [SPONSORED STREETBALL COURT]
                            |
                    [LOBBY - Ground Level]
```

**The spatial language is reversed**: In the Underground, you descend (into The Freighter, down The Staircase). In the Penthouse, you ASCEND. You take an elevator UP to Marcus's office. The elevation is aspirational, but it feels like climbing away from something, not toward something.

**Sanctioned Race Track**: A closed-circuit track inside a parking garage. It's SAFE — barriers, runoff zones, no traffic. It's BORING. The track is technically perfect, but it has no SOUL. The lesson: polish kills spontaneity. This track will never produce the moments The Strip does.

**Televised Fight Venue**: A ring with ropes, a referee, cameras on cranes. It's a fight, but it's not a FIGHT. The lesson: rules sanitize violence. Bishop's cage had no rules. This cage has too many.

**Sponsored Streetball Court**: An indoor court with branded flooring, JumboTron screens, and seating for 500. The Cage held 200 people pressed against a fence. This holds 500 people sitting in chairs, watching. The lesson: comfort creates distance.

#### Pacing Curve (The Penthouse - Full District)

```
EMOTIONAL TENSION (Not Gameplay Tension)
  ^
  |                                    ____
  |                              _____/    \
  |                        _____/           \
  |                  _____/                  \
  | ___________     /                         \___
  |/           \___/
  +----------------------------------------> TIME (hours)
  0   1   2   3   4   5   6   7   8   9   10

  0-1h:   First visit. Curiosity. "This is different."
  1-2h:   Participation. "The money is real. The crowds are huge."
  2-4h:   Cognitive dissonance. "Why doesn't this feel good?"
  4-6h:   Realization. "I miss the Underground."
  6-8h:   The choice is forced. Marcus's contract or walk away.
  8-10h:  Resolution. Choose a path. The Penthouse either becomes your new home (hollow victory) or the place you burned down (symbolically).
```

The Penthouse is NOT about mechanical difficulty. It's about emotional difficulty. The events here are EASIER than Underground events. The rewards are HIGHER. But the FEELING is wrong. The level design is the argument.

#### Key Design Metrics (Penthouse)

- **Lighting**: 40% brighter than any Underground district (overlit, clinical)
- **Crowd behavior**: Passive. They clap politely. They don't ROAR. The audio dynamic range is 30% narrower than Midtown.
- **Style Meter behavior**: Gains normally, but the visual feedback is muted. The neon doesn't POP the same way. This is subtle but important — the game is SHOWING you that style feels different here.
- **Camera angles**: More static, more "broadcast" feeling — you're being FILMED, not EXPERIENCED.

#### Encounter Breakdown: Marcus (Final Choice - Not a Fight)

**WHERE**: Marcus's office. Top floor of the Penthouse tower. Floor-to-ceiling windows overlooking the entire city. You can SEE all five Underground districts from here. Southside's glow. The Docks' lights. Midtown's towers. The Heights' hills. Old Town's strip.

**WHY HERE**: The spatial symbolism is literal. Marcus is ABOVE the Underground. He looks down on it. The question the game asks: will you join him up here, or will you return down there?

**WHAT HAPPENS**: No fight. No race. A conversation. Marcus presents the contract. He makes his case. The player has three response options (simplified):

1. **"I'm in."** (Mainstream ending path)
2. **"I'm out."** (Underground ending path)
3. **"There's a third way."** (Only available if specific conditions met — high REP in all districts, crew intact, Zero questline discovered)

**THE THIRD WAY**: The player proposes a cooperative structure where the Underground controls its own representation, using Marcus's resources but not his ownership. This is the hardest ending to unlock and requires mastering all four disciplines, maintaining crew loyalty, and understanding Zero's original vision.

**SPATIAL STORYTELLING**: The player's choice is reflected IMMEDIATELY in the environment. Choose Mainstream: the office door locks behind you, symbolizing commitment. Choose Underground: you walk to the elevator, descend, and the Penthouse district becomes INACCESSIBLE (you burned that bridge). Choose Third Way: Marcus stands, looks out the window with you, and says, "Let's go down there and talk to them together."

---

## III. CROSS-DISTRICT SPATIAL DESIGN

### The City as a Flow Problem

The player doesn't just experience districts in isolation. They MOVE between them. The connective tissue matters as much as the organs.

#### Fast Travel Philosophy

Fast travel is AVAILABLE but not REQUIRED. The game should make driving between districts INTERESTING enough that the player chooses to do it sometimes. Fast travel is a quality-of-life feature for hour 20+, not a crutch for poor spatial design.

**When does the player fast travel?**
- When they've already driven that route five times.
- When they're in a shopping/optimization loop (event -> Old Town -> event).
- When they're focused on mechanical mastery and narrative is secondary.

**When does the player drive manually?**
- When they're new to a district connection and want to learn the route.
- When a rival or event is "on the way" (the game should spawn dynamic encounters during traversal).
- When they're in "flow state" and want to chain style across districts (driving between districts fills the Style Meter passively).

#### District Boundaries as Thresholds

The transition from one district to another should be FELT. Not a hard loading screen (there are none), but an environmental shift.

**Southside -> Old Town**: The streets widen. The industrial facades give way to commercial storefronts. The lighting warms from cool blues to warm oranges. The audio shifts from engine noise to ambient crowd chatter.

**Old Town -> Docks**: The streets narrow. You start seeing water, rust, shipping containers. The lighting cools. The bass in the music drops lower, heavier.

**Docks -> Midtown**: Elevation rises. You're climbing out of the waterfront into the housing projects. The crowds grow. The lighting becomes more uneven (streetlights + apartment windows).

**Midtown -> Heights**: The roads get steeper. Residential architecture replaces commercial/industrial. The crowds thin. The audio opens up — more space, less compression.

**Heights -> Old Town**: Descent. You're coming back to the valley where Old Town sits. The familiarity is intentional — Old Town is HOME BASE.

The player should be able to FEEL which district they're in with their eyes closed, based on audio alone.

#### Dynamic Event Spawning During Traversal

The drive between districts is NOT empty. The game spawns:

- **Ambient Races**: NPC cars with underglow pull up next to you at a red light. Rev engine. Impromptu race begins.
- **Rival Intercepts**: A rival with high Grudge intercepts you. "We got business. Pull over."
- **Crew Callouts**: A crewmate texts, "I'm at [location] — meet me." Dynamic micro-missions during traversal.
- **Style Opportunities**: Trick spots along routes (a rail you can grind while DRIVING — yes, this should exist in Heights transitions).

Traversal is PART OF THE LOOP, not dead time between loops.

---

## IV. METRICS TO TRACK IN PLAYTESTING

These are the questions I need answered by watching players, not by guessing at my desk.

### Priority 1: Core Loop Validation

1. **Does each discipline's 30-second loop pass the "one more round" test independently?**
   - Metric: Session length when given a single-discipline sandbox. Target: 15+ minutes before boredom.
   - Watch for: When does the player start looking at their phone? That's the boredom point.

2. **How long does it take a new player to understand each discipline's spatial language?**
   - Metric: Time from discipline introduction to first B-rank performance. Target: 3-5 events (10-15 minutes).
   - Watch for: Confusion signals — missed inputs, unclear pathing, failure to use the space correctly.

3. **Do players naturally discover breadcrumbs, or do they get lost?**
   - Metric: Time spent in "wander mode" (no objective engagement, no movement toward events). Target: Less than 2 minutes per session.
   - Watch for: Menu opens to check map (indicates failed environmental navigation).

### Priority 2: Pacing and Difficulty

4. **Do tension curves match intent?**
   - Metric: Player heart rate during key events (if biometric tracking available) OR player self-reported tension ratings post-event.
   - Watch for: Flat affect during intended peaks (design failure). Stress during intended valleys (pacing failure).

5. **Are boss events completable on the 3rd attempt?**
   - Metric: Boss defeat attempt count. Target median: 2-3 attempts.
   - Watch for: First-attempt victories (boss too easy). 5+ attempts (boss too hard or unclear).

6. **Does the Penthouse feel hollow?**
   - Metric: Player facial expressions and dialogue during Penthouse events. Target: Visible discomfort or stated dissatisfaction.
   - Watch for: If players PREFER the Penthouse, the spatial storytelling has failed.

### Priority 3: Spatial Clarity

7. **Can players navigate from any district to Old Town without a map?**
   - Metric: Navigation success rate (reach Old Town without opening map). Target: 80%+ by hour 5.
   - Watch for: Map opens. That's a failed breadcrumb.

8. **Do players understand elevation and sightlines in the Heights?**
   - Metric: Trick run scores compared to Nix's tutorial run. Target: 70%+ of players reach 80% of Nix's score by their 3rd attempt.
   - Watch for: Players ignoring vertical opportunities (failure to teach spatial scanning).

9. **Does the Style Meter gain feel EARNED in each discipline?**
   - Metric: Post-session interview — "Did you feel the Style Meter rewarded the right actions?" Target: 90%+ yes.
   - Watch for: Complaints about meter gain feeling random or disconnected from player intent.

### Priority 4: Emotional Resonance

10. **Do players form genuine rivalries with AI characters?**
    - Metric: Unsolicited mentions of specific rival names during playtesting. Target: 3+ rival names mentioned per 10-hour session.
    - Watch for: Generic descriptions ("that guy," "the fighter") instead of names (system failure).

11. **Does the player CARE about their crew by hour 10?**
    - Metric: Reaction to crew fracture event (Trick leaving). Target: Visible emotional response (frustration, sadness, anger).
    - Watch for: Indifference. If the player shrugs, the relationship building failed.

12. **Does Old Town feel like home?**
    - Metric: Voluntary return frequency (non-quest visits to Old Town). Target: 2+ voluntary visits per session.
    - Watch for: Players fast-traveling OUT of Old Town immediately after arriving (place has no pull).

---

## V. OPEN DESIGN QUESTIONS

These are the questions I CANNOT answer without build-test-iterate cycles.

1. **What's the right density of events per district?**
   - Hypothesis: 8-12 events per district feels full without overwhelming.
   - Test: Do players feel paralyzed by choice (too many) or starved for content (too few)?

2. **Should districts unlock sequentially or in player-chosen order?**
   - Hypothesis: Player choice increases engagement, but gating prevents overwhelm.
   - Test: Does freedom feel empowering or directionless?

3. **How much of the map should be drivable vs. walkable?**
   - Hypothesis: 70% drivable (racing focus), 30% walk-only (density focus in Old Town, Midtown, Docks).
   - Test: Do players feel frustrated by walk-only zones, or do they provide pacing relief?

4. **What's the optimal size differential between districts?**
   - Hypothesis: Southside (largest), Midtown (second), Docks (third), Heights (fourth), Old Town (smallest). Size correlates with primary movement mode (racing needs space, tricks need density).
   - Test: Does any district feel too large (empty) or too small (claustrophobic)?

5. **Should boss arenas be VISIBLE from a distance, or DISCOVERED through exploration?**
   - Hypothesis: Visible = goal clarity. Hidden = discovery reward. Split the difference: King's Garage and Bishop's Fortress visible. Trick's court and Nix's loft require finding.
   - Test: Do players feel rewarded by discovery, or frustrated by obscurity?

6. **How much environmental destruction/change should result from events?**
   - Hypothesis: Minimal destruction (this isn't Battlefield), but persistent marking (graffiti, tire marks, scuff marks on courts).
   - Test: Does the world feel LIVED IN, or does it feel static?

7. **What's the failure state for events?**
   - Hypothesis: Losing an event costs no REP but triggers rival/narrative consequences. Mechanical failure is not punished; narrative choices are.
   - Test: Does losing feel fair and interesting, or punishing and frustrating?

---

## VI. SPATIAL STORYTELLING PRINCIPLES (FINAL SUMMARY)

Every level design decision in UNDERGROUND must answer these questions:

### Where does the player LOOK?

The player's eye should always be GUIDED, never LOST. Light, color, density, elevation, sound — every sensory input is a breadcrumb. If the player opens a map, the environment failed.

### Where does the player MOVE?

Every space teaches a movement vocabulary. Racing spaces teach speed. Fighting spaces teach distance. Sports spaces teach rhythm. Trick spaces teach commitment. The player's body (via the controller) should LEARN the city.

### What does this space TEACH?

No space is neutral. The Rail Yards teach drift basics. Industrial Row teaches risk/reward. The Freighter teaches spacing under pressure. The Cage teaches crowd dynamics. The Staircase teaches commitment. Every space is a lesson the player doesn't know they're taking.

### What does this space FEEL?

Southside feels hungry. The Docks feel heavy. Midtown feels electric. The Heights feel free. Old Town feels warm. The Penthouse feels wrong. Emotion is spatial. The geometry, lighting, audio, and camera CREATE feeling. If a space doesn't have an emotion, it has no purpose.

### How does this space CHANGE?

The Underground is alive. Graffiti appears. Crowds grow. Rivals move through spaces. The player's legend is written on the walls. A district at hour 1 should LOOK different at hour 20, not because of scripted events, but because the player's presence has MARKED it.

---

*This document is a map, not a prison. The spaces will evolve through playtesting. But the questions stay the same: Where does the player LOOK? Where does the player MOVE? What are we teaching? What are we making them FEEL? Answer those, and the level designs itself.*

*The city is a stage. The player is the performer. The space is the script they don't know they're reading.*

*— GRID*
