# UNDERGROUND — Production Plan

**Producer**: CLOCK
**Status**: Production Roadmap — Ready for Execution
**Version**: 1.0
**Date**: 2026-02-07

---

## 1. Project Overview

### 1.1 What We're Building

UNDERGROUND is a multi-genre street culture career game combining racing, fighting, basketball, and freestyle tricks into a unified reputation-driven progression system. Target: Steam (PC primary, Steam Deck validated), 30-40 hours to credits, PS2 aesthetic with modern systems depth.

This is four games unified by one progression spine. The scope is large. The risk is real. The mitigation is ruthless prioritization and vertical-slice validation before full production.

### 1.2 Scope Summary

**Core Pillars** (non-negotiable):
1. Four disciplines (racing, fighting, basketball, tricks) with distinct gameplay
2. Unified Style Meter + REP progression across all disciplines
3. AI-driven rival system with emergent relationships (25-30 named rivals)
4. Dense open-world city (4 districts, Yakuza-style density)
5. Deep customization with cross-discipline synergies
6. 2000s aesthetic authenticity (CRT shader, neon underglow, era-accurate fashion/music)

**Stretch Goals** (cut if schedule slips):
- Crew vs. Crew multiplayer (async rivalry between player crews)
- Music rhythm integration (beat-synced Style Meter bonuses)
- Create-A-Legend mode (export your character as an AI rival for others)
- District editor (player-created content)
- Fifth discipline (skateboarding)

**Cut List** (not in 1.0):
- Real-time online multiplayer
- Multiple cities
- Licensed cars (all fictional/inspired designs)
- Photo mode
- New Game Plus

### 1.3 Team Structure

**Core Team** (minimum viable):
- 1 Producer (CLOCK - that's me, managing this whole operation)
- 1 Lead Designer (REED - owns gameplay systems, balance, loop design)
- 1 Lead Programmer (BYTE - technical architecture, engine integration)
- 1 Programmer (disciplines implementation, AI systems)
- 1 Narrative Designer (NOVA - story, characters, world-building)
- 1 Art Director (PIXEL - visual identity, art pipeline, asset review)
- 1 Environment Artist (districts, props, lighting)
- 1 Character/Vehicle Artist (player character, cars, rivals)
- 1 Sound Designer/Composer (ECHO - SFX, music, audio implementation)
- 1 QA Lead (CRASH - testing, bug tracking, balance validation)

**Extended Team** (contract/part-time):
- 2 Additional Environment Artists (months 7-16, content push)
- 1 UI/UX Designer (months 4-12, interface implementation)
- 1 Technical Artist (months 4-18, shader work, VFX, optimization)
- 1 Additional Programmer (months 10-16, if scope proves too large)
- Marketing Support (HYPE - months 14-18, Steam page, trailer, launch prep)

**Total headcount**: 10 core + 5 extended/contract = 15 people peak (months 10-16)

### 1.4 Timeline

**Total Duration**: 18 months (78 weeks)
- Prototype: Months 0-3
- Vertical Slice: Months 4-6
- Pre-Production: Months 7-9
- Production: Months 10-15
- Alpha: Month 16
- Beta: Month 17
- Launch Prep: Month 18

**Target Ship Date**: Month 18, Week 4 (1.0 launch on Steam)

**Key Dates**:
- Month 3, Week 4: Racing prototype must pass "one more race" test or we pivot
- Month 6, Week 4: Vertical slice with 3 disciplines playable or we cut scope
- Month 9, Week 4: Full loop (REP/progression/rivals) functional or we cut features
- Month 16, Week 4: Feature freeze, alpha testing begins
- Month 17, Week 4: Code freeze, beta to external testers
- Month 18, Week 4: 1.0 launch

### 1.5 Budget Assumptions

Not detailing exact budget here (that's finance's job), but production assumes:
- Unity Pro licenses for all programmers + lead designer ($2k/year/seat x 4 = $8k/year)
- Steam Direct fee ($100)
- Middleware licenses (FMOD if needed, Odin Inspector, DOTween Pro) (~$500 total)
- Contract labor at standard rates for extended team
- Marketing budget exists for trailer production, Steam featuring, press outreach (not produced, but needs to exist)
- No licensed music budget (all original composition, possibly 1-2 licensed tracks for trailer if budget allows)

This is a mid-tier indie production. Not AAA. Not hobbyist. Achievable with focused execution.

---

## 2. Milestone Definitions

Each milestone has clear entry/exit criteria. You don't move forward until exit criteria are met. No exceptions. This is how scope creep dies.

### Milestone 0: Pre-Production Kickoff (Weeks 0-2)

**Entry Criteria**: Team hired, contracts signed, tools installed.

**Deliverables**:
- Unity project initialized (2022.3 LTS)
- Git repo + CI pipeline active
- First daily build runs successfully
- Design documents reviewed by full team (everyone reads pitch, GDD, narrative bible, art direction, sound design, tech architecture)
- First discipline choice finalized (REED decides: racing is first, it's most legible to playtest)
- Sprint 0 backlog created (CLOCK owns backlog)

**Exit Criteria**:
- All team members have Unity running, can pull repo, can build to Windows executable
- First stand-up meeting held, team knows sprint cadence
- CLOCK has first 6 sprints planned in backlog

**Owner**: CLOCK (Producer)
**Duration**: 2 weeks
**Risk**: Low. Standard project setup. If Git or Unity causes issues, senior programmer handles.

---

### Milestone 1: Racing Prototype (Months 1-3, Weeks 3-14)

**Entry Criteria**: Milestone 0 complete.

**Goal**: Prove racing feels good enough to build a game around.

**Deliverables**:
- Playable racing system:
  - Player car with arcade drift physics (grip/drift state machine)
  - 3 AI opponent cars with waypoint-based racing
  - One 3-lap circuit (placeholder geometry)
  - Nitrous mechanic functional
  - Near-miss detection and scoring
- Style Meter prototype (fills during drifts/near-misses, decays when idle)
- Basic HUD (speed, position, Style Meter bar)
- Results screen (placement, REP/CASH earned, style rank D-S)
- 60fps on Steam Deck (800p) confirmed via profiling

**Exit Criteria** (ALL must be met):
1. **"One More Race" Test**: 8/10 internal playtesters say "yes" when asked "do you want to race again?" after finishing one race. If not, racing is not fun enough. Iterate or pivot.
2. **Drift Feel Validation**: Drifting must feel satisfying. REED and BYTE co-sign on physics feel. If drift sucks, the whole game is at risk (drifting is core to Style Meter scoring).
3. **Style Meter Legibility**: Playtesters can explain what the Style Meter does without being told. If they're confused, feedback is unclear.
4. **Performance Floor Met**: 60fps locked on Steam Deck test hardware. If not, visuals are too expensive; PIXEL cuts effects/detail.

**Owner**: BYTE (Lead Programmer) + REED (Design feedback loop)
**Duration**: 12 weeks (3 months)
**Risk Level**: HIGH
- **Risk**: Racing doesn't feel good. Arcade physics are hard to tune.
- **Mitigation**: Weekly playtest Fridays. REED + BYTE iterate based on feedback. Reference Need for Speed Underground 2 constantly. If physics still suck at Week 10, consider licensing a vehicle physics package (Edy's Vehicle Physics, ~$100) instead of custom.
- **Fallback**: If racing fails by Month 3, pivot entire project. UNDERGROUND without racing is not UNDERGROUND.

**Dependencies**: None (first milestone, no blockers).

---

### Milestone 2: Fighting System Prototype (Months 4-5, Weeks 15-22)

**Entry Criteria**: Milestone 1 complete (racing validated).

**Goal**: Prove fighting system works and integrates with Style Meter.

**Deliverables**:
- Playable fighting system:
  - Player character with 4 moves (light punch, heavy punch, kick, grab/throw)
  - Frame-data-driven hit detection (startup/active/recovery frames)
  - One rival opponent with basic AI (behavior tree: attack when close, block randomly)
  - Combo system (light -> light -> heavy chain possible)
  - Taunt mechanic (1.2s vulnerability, +60 style points)
- Style Meter integration (hits/combos fill meter, same visual as racing)
- Fight arena (simple cage, crowd background)
- Results screen (win/loss, style rank)

**Exit Criteria**:
1. **Combat Feel Check**: Hits must feel impactful. ECHO's impact SFX + PIXEL's screen shake + BYTE's hitstun timing all align. If hits feel floaty, iterate.
2. **Style Risk/Reward Balance**: Taunt must feel dangerous (you get punished ~30% of attempts) and rewarding (style gain is significant). If risk/reward is off, tune vulnerability window or style points.
3. **Cross-Discipline Style Meter Works**: Player can race (fill Style Meter to 500), then immediately fight, and Style Meter persists. The cross-discipline continuity is the core innovation. If this breaks, fix immediately.

**Owner**: BYTE (implementation) + REED (frame data design)
**Duration**: 8 weeks (2 months)
**Risk Level**: MEDIUM
- **Risk**: Frame data balancing is complex. Easy to make moves feel unresponsive or broken.
- **Mitigation**: REED references fighting game frame data charts (Street Fighter, Tekken). Start conservative (slow moves, long recovery) and speed up based on playtests.
- **Fallback**: If combo system proves too complex, simplify to single-hit attacks only. Combos become stretch goal.

**Dependencies**: Milestone 1 must be complete (Style Meter foundation exists).

---

### Milestone 3: Basketball System Prototype (Months 5-6, Weeks 23-26)

**Entry Criteria**: Milestone 2 complete (fighting validated).

**Goal**: Third discipline functional, cross-discipline chain mechanic proven.

**Deliverables**:
- Playable basketball system:
  - 2v2 streetball (player + AI partner vs. 2 AI opponents)
  - Dribbling, shooting, passing functional
  - Crossover/ankle-breaker mechanic (timing-based, stuns defender on success)
  - Shot detection (ball enters hoop trigger, awards points)
  - Court boundary detection (out-of-bounds turnover)
- AI teammates competent enough that losses don't feel like AI's fault
- Style Meter integration (crossovers, swishes, dunks fill meter)
- Cross-discipline chain bonus: Race -> Fight -> Ball within 10 minutes = +200 REP bonus on third event

**Exit Criteria**:
1. **Triple Threat Achievement**: Internal tester completes race, fight, ball game in sequence and receives Triple Threat bonus. This proves the meta-loop works.
2. **Basketball Fun Check**: Basketball must pass "would I play 5 minutes of just this?" test. If it feels like a minigame (not a real basketball experience), iterate or consider cutting.
3. **AI Partner Doesn't Suck**: Playtesters don't blame AI partner for losses. If they do, improve partner AI positioning/shooting.

**Owner**: Second Programmer (if hired by Month 5; else BYTE continues)
**Duration**: 4 weeks (1 month)
**Risk Level**: MEDIUM
- **Risk**: Basketball physics (ball trajectory) can feel wrong easily. Shooting arc math must feel intuitive.
- **Mitigation**: Reference NBA Street Vol. 2 shooting. Simple arc formula: parabola with gravity, fixed release angle. Don't overcomplicate.
- **Fallback**: If basketball can't hit quality bar, cut it from 1.0 launch. Ship with 3 disciplines (racing, fighting, tricks). Basketball becomes post-launch DLC.

**Dependencies**: Milestone 2 complete (Style Meter + event structure in place).

---

### Milestone 4: Vertical Slice Complete (Month 6, Week 26-27)

**Entry Criteria**: Milestones 1, 2, 3 complete (three disciplines playable).

**Goal**: Prove the game concept works end-to-end in a small slice.

**Deliverables**:
- One complete district (Southside):
  - Explorable environment (1km x 1km, placeholder geometry acceptable)
  - 3 racing events, 2 fighting events, 2 basketball events placed in world
  - Player can walk/drive between events (no discipline-locked zones)
- Basic progression:
  - REP/CASH awarded after events
  - REP total tracked (tier system placeholder UI)
  - One rival (Marcus, from narrative bible) appears in 2 events, relationship updates after player wins/loses
- Garage UI (can spend CASH on 2 car upgrades, see stat changes)
- Camera transitions between disciplines (Cinemachine setup, 2-second blends)
- Full game loop: Walk to event -> Enter -> Play -> Results -> Spend -> Repeat

**Exit Criteria**:
1. **External Playtest Validation**: Bring in 5 external testers (not team). They play for 90 minutes. Ask: "Would you keep playing if this was available?" If 4/5 say yes, vertical slice succeeds.
2. **Technical Validation**: Slice runs at 60fps on Steam Deck, loads district in under 10 seconds, no crashes during 90-min session.
3. **Scope Checkpoint**: CLOCK reviews actual time-to-build vs. estimated. If disciplines took 2x longer than estimated, cut scope NOW (likely cuts: tricks discipline becomes post-launch, or reduce district count from 4 to 3).

**Owner**: CLOCK (coordinates all departments)
**Duration**: 2 weeks (assembly + polish)
**Risk Level**: CRITICAL
- **Risk**: Vertical slice doesn't feel like "one game." Disciplines feel disconnected.
- **Mitigation**: PIXEL ensures visual consistency across disciplines. ECHO ensures audio language is unified. REED ensures Style Meter is the connective tissue players understand.
- **Fallback**: If slice fails external playtest, we have 12 months to fix it. But we must know what's broken. CLOCK conducts detailed debrief with testers: "What confused you? What excited you? What felt like a different game?"

**Dependencies**: Milestones 1, 2, 3 complete.

**Go/No-Go Decision**: At end of Week 27, CLOCK calls a production meeting. Either:
- **GO**: Slice validates concept. Proceed to full production with current scope.
- **SCOPE CUT**: Slice is good but took too long. Cut tricks discipline or reduce district count. Proceed with reduced scope.
- **NO-GO**: Slice fails validation. Major pivot required (unlikely if individual disciplines passed their tests, but possible).

---

### Milestone 5: Tricks System + Full District 1 (Months 7-9, Weeks 28-39)

**Entry Criteria**: Milestone 4 passed GO decision.

**Goal**: Fourth discipline added, first district reaches production quality.

**Deliverables**:
- Tricks system:
  - Skateboard/BMX trick gameplay (Tony Hawk-style)
  - Ollie, grab tricks, grinds, manuals functional
  - Combo system (link tricks for multiplier)
  - Bail system (failed landing = lose combo)
  - One trick course/environment in Southside
- Southside district (full production assets):
  - Final geometry (PIXEL-approved visual quality)
  - Baked lighting, optimized LODs
  - 8 events total (2 per discipline)
  - Ambient NPC population (traffic, pedestrians)
  - One district boss event (King Delgado, from narrative bible)
- Full progression system:
  - REP tier system (NOBODY -> LEGENDARY)
  - Diminishing returns on repeated events (25% REP after 4th same-type event)
  - District unlock gating (Docks unlocks at 5,000 REP)
- Rival AI system:
  - RivalState data structure (Respect, Grudge, Confidence tracking)
  - 5 rivals implemented (King + 4 regular rivals in Southside)
  - Rival mood reactions to player wins/losses
  - Obsession mechanic (70+ Grudge = rival interrupts events)

**Exit Criteria**:
1. **Tricks Validation**: Tricks pass "one more trick run" test (same as racing test). If not, iterate or cut tricks.
2. **District Production Quality**: Southside looks/sounds/feels final. No placeholder art remains. PIXEL + ECHO sign off.
3. **Rival AI Produces Stories**: Playtesters report at least one "memorable rival moment" (e.g., "Marcus kept showing up after I beat him, finally I broke him"). If no stories emerge, AI needs more variance or clearer feedback.

**Owner**:
- Tricks: Second Programmer (or BYTE if programmer #2 not hired)
- District: Environment Artist + Character/Vehicle Artist
- Rival AI: BYTE + NOVA (AI systems + personality data)

**Duration**: 12 weeks (3 months)
**Risk Level**: HIGH
- **Risk**: Four disciplines is too much. Team bandwidth is stretched. Tricks might not hit quality bar.
- **Mitigation**: If tricks slips past Week 35, cut it from 1.0. Ship with 3 disciplines. Tricks becomes DLC.
- **Risk**: Rival AI doesn't feel personal/emergent. Feels random or scripted.
- **Mitigation**: NOVA writes 25-30 rival personality profiles (Pride, Confidence, Style Affinity variations). BYTE implements but relies on NOVA's data. Playtest Weeks 36, 38 specifically for rival AI feel.

**Dependencies**: Milestone 4 complete.

---

### Milestone 6: Content Production (Months 10-15, Weeks 40-65)

**Entry Criteria**: Milestone 5 complete (all disciplines + one full district done).

**Goal**: Fill the world. Build remaining 3 districts, all events, all rivals.

**Deliverables**:
- Districts 2-4 (Docks, Midtown, Heights):
  - Full geometry, lighting, optimization (same quality as Southside)
  - 8-10 events per district (total 100+ events across all districts)
  - District-specific ambiance (rain in Docks, always)
  - District boss per district (Bishop, Trick, Nix from narrative bible)
- Rival roster:
  - 25-30 named rivals total
  - Each rival has personality data, preferred car, preferred discipline
  - Rival recruitment mechanic (60+ Respect = recruitment offer)
  - Rival breaking mechanic (Confidence hits 0 = permanent story change)
- Customization system (full):
  - 30-40 cars (across 3 archetypes: Import, Sport, Muscle)
  - 20-30 fighting movesets
  - 20-25 basketball skills
  - 20-25 trick loadouts
  - Fashion items (tops, bottoms, shoes, hats, accessories)
  - Garage/locker room UI complete
- Narrative beats:
  - Underground-vs-mainstream tension escalates (Marcus Webb character arc)
  - Crew recruitment dialogues
  - 3 ending paths branch based on player choices (Underground, Mainstream, Third Path)
- Audio implementation:
  - 4 district music themes (adaptive layers + horizontal sections)
  - 4 boss music suites
  - Full SFX suite (~430 sound files per ECHO's doc)
  - FMOD integration (if used; else Unity audio with custom beat detection)
- UI/UX (full):
  - Main menu, pause menu, settings
  - Phone system (rival calls, crew intel)
  - Results screens (all disciplines)
  - District map with event markers
  - REP/CASH HUD persistent
  - Style Meter UI (vertical bar, neon tube aesthetic)

**Exit Criteria**:
1. **Content Complete**: All 4 districts explorable, all 100+ events playable, all rivals encounter-able. No placeholder content remains except debug tools.
2. **Playable Start-to-Finish**: CRASH (QA Lead) completes full playthrough (0 REP to credits) in 30-40 hours without hitting a blocker bug.
3. **Performance Maintained**: All districts run at 60fps on Steam Deck. If any district drops below 55fps average, Environment Artist + Technical Artist optimize (LOD tuning, draw call reduction).
4. **Three Endings Reachable**: CRASH validates all three ending paths are accessible and trigger correctly based on player choices.

**Owner**:
- Districts: Environment Artists (2 additional contractors months 10-15)
- Rivals/Narrative: NOVA + BYTE (narrative data + AI implementation)
- Audio: ECHO (composition + implementation)
- UI/UX: UI Designer (contract, months 10-15)

**Duration**: 26 weeks (6 months) — Longest phase, most team members active
**Risk Level**: CRITICAL
- **Risk**: Content production takes longer than estimated. Team burns out. Scope creep sneaks in.
- **Mitigation**: CLOCK reviews weekly burn-down charts. If velocity drops 20% below estimate, cut content (reduce event count from 100 to 80, or cut one district). Monthly scope review meetings: "What can we cut to ship on time?"
- **Risk**: Team fatigue. 6 months of production grind is brutal.
- **Mitigation**: Milestone celebrations (pizza lunch when each district ships). CLOCK enforces no-crunch policy (40-hour weeks max). If crunch becomes necessary, it means planning failed. Cut scope instead.

**Dependencies**: Milestone 5 complete (foundation + one district done).

**Scope Checkpoint** (Month 12, Week 52): CLOCK reviews actual completion vs. plan. If less than 50% of content is done, we're behind. Options:
- Cut district count (ship with 3 districts, 4th is post-launch)
- Cut event count (60-80 events instead of 100)
- Cut stretch goals (crew multiplayer, create-a-legend definitely cut)
- Extend timeline by 2 months (ship in Month 20 instead of Month 18)

Decision made by CLOCK + team leads (REED, BYTE, NOVA, PIXEL, ECHO).

---

### Milestone 7: Alpha (Month 16, Weeks 66-69)

**Entry Criteria**: Milestone 6 complete (content production done).

**Goal**: Feature freeze. Focus shifts to bug fixing and balance.

**Deliverables**:
- Alpha build (feature-complete, may have bugs):
  - All features implemented
  - All content in-game
  - Save/load functional
  - Steam Cloud integration tested
  - No known crash bugs
- Internal alpha test:
  - All team members play 10-hour session
  - Bug database initialized (using Jira, Trello, or GitHub Issues)
  - Priority bugs identified (P0 = crash/blocker, P1 = major gameplay issue, P2 = minor, P3 = polish)
- Balance pass:
  - REED + CRASH review economy (REP/CASH earn rates, item costs)
  - Difficulty tuning (AI opponent strength, event difficulty tiers)
  - Style Meter tuning (gain rates, decay rate, UNDERGROUND MODE threshold)

**Exit Criteria**:
1. **No P0 Bugs**: Zero crash bugs or progression blockers. If any exist, BYTE fixes immediately.
2. **Balance Feels Right**: Economy playtesting shows players earning one meaningful purchase every 45-75 minutes. If off, REED tunes ScriptableObject values.
3. **Complete Playthrough Possible**: CRASH completes start-to-finish in one sitting (8-10 hour session) without hitting blockers.

**Owner**: CRASH (QA Lead) + BYTE (bug fixing) + REED (balance)
**Duration**: 4 weeks (1 month)
**Risk Level**: MEDIUM
- **Risk**: Bug count is overwhelming. Team can't fix everything.
- **Mitigation**: Triage ruthlessly. P0 bugs must be fixed. P1 bugs should be fixed. P2/P3 bugs are deferred to post-launch patches if time is tight.
- **Risk**: Balance is off and requires major tuning (e.g., economy is too tight, players feel starved).
- **Mitigation**: REED has final authority on balance. If tuning is contentious, playtest data decides (not opinions).

**Dependencies**: Milestone 6 complete.

**Feature Freeze Declaration**: At start of Week 66, CLOCK officially declares feature freeze. No new features. Bug fixes and balance only. Any feature requests are added to "post-launch wishlist."

---

### Milestone 8: Beta (Month 17, Weeks 70-73)

**Entry Criteria**: Milestone 7 complete (alpha stable).

**Goal**: External validation. Real players test the game. Polish and final bug fixing.

**Deliverables**:
- Beta build (polished, minimal bugs):
  - All P0/P1 bugs fixed
  - P2 bugs mostly fixed
  - Performance optimized (60fps on Steam Deck locked)
  - UI polish (animations, transitions smooth)
  - Audio mix finalized (ECHO's master mix pass)
- External beta test:
  - 50-100 external testers (recruited via Discord, Twitter, mailing list)
  - Beta runs for 2 weeks (Weeks 71-72)
  - Feedback form (what's fun, what's frustrating, what's confusing, bugs encountered)
  - CRASH monitors feedback daily, prioritizes fixes
- Steam store page live:
  - Screenshots (PIXEL provides, 10+ images)
  - Trailer (HYPE produces 90-second trailer, shows all four disciplines + Style Meter + rival system)
  - Description written (HYPE writes copy, CLOCK reviews)
  - Wishlist campaign starts

**Exit Criteria**:
1. **Positive Beta Reception**: 70%+ of beta testers report "I would recommend this game" on feedback form. If below 70%, identify pain points and fix in Week 73.
2. **No Critical Bugs**: Beta testers report zero crash bugs. If crashes occur, BYTE fixes immediately.
3. **Performance Validated on Real Hardware**: Beta testers with Steam Decks report smooth performance. If any report stuttering or frame drops, Technical Artist investigates.

**Owner**: CRASH (beta coordination) + HYPE (marketing) + Full Team (bug fixing)
**Duration**: 4 weeks (1 month)
**Risk Level**: HIGH
- **Risk**: Beta reveals a fundamental flaw (e.g., progression is too slow, one discipline is broken, rival AI is confusing).
- **Mitigation**: This is the last chance to fix major issues. If beta feedback is harsh, CLOCK calls emergency production meeting. Options: delay launch by 1 month, or cut/simplify broken feature.
- **Risk**: Marketing materials (trailer, screenshots) don't land. Wishlist growth is slow.
- **Mitigation**: HYPE monitors wishlist count daily. If growth is <100 wishlists/day, revise marketing messaging or increase outreach (Reddit posts, influencer outreach).

**Dependencies**: Milestone 7 complete.

**Code Freeze Declaration**: At end of Week 73, CLOCK declares code freeze. No more code changes except P0 crash fixes. All other bugs go into day-one patch plan.

---

### Milestone 9: Launch Prep & Gold Master (Month 18, Weeks 74-78)

**Entry Criteria**: Milestone 8 complete (beta validated).

**Goal**: Ship the game.

**Deliverables**:
- Gold master build (1.0):
  - Final build uploaded to Steam (Windows + Linux)
  - All known bugs either fixed or documented in known issues list
  - Day-one patch plan created (P2 bugs fixed post-launch)
  - Steam achievements implemented and tested
  - Save file tested across multiple playthroughs (no corruption)
- Launch marketing:
  - Trailer published on YouTube, Twitter, Reddit
  - Press outreach (HYPE sends emails to gaming press, indie curators)
  - Discord server active (community manager monitoring)
  - Reddit AMA scheduled (REED + NOVA + CLOCK answer community questions)
- Launch day plan:
  - CLOCK monitors Steam launch in real-time
  - BYTE on-call for critical bugs
  - CRASH monitors Steam forums, Discord, subreddit for reports
  - Patch 1.0.1 ready to deploy within 24 hours if critical bugs appear

**Exit Criteria**:
1. **Build Uploaded**: Gold master on Steam, tested via Steam's beta branches (internal testing).
2. **Launch Day Smooth**: Game launches at scheduled time (ideally Tuesday or Wednesday for press coverage, not Friday when news cycle is slow).
3. **No Launch-Day Crashes**: First 24 hours post-launch, no widespread crash reports. If crashes occur, Patch 1.0.1 deployed immediately.

**Owner**: CLOCK (launch coordination) + BYTE (technical readiness) + HYPE (marketing)
**Duration**: 4 weeks (1 month)
**Risk Level**: MEDIUM
- **Risk**: Launch-day critical bug discovered (e.g., save file corruption, crash on specific hardware).
- **Mitigation**: BYTE remains on-call for 72 hours post-launch. Patch 1.0.1 pre-prepared for rapid deployment. Steam allows instant patching (no cert process like consoles).
- **Risk**: Launch marketing doesn't drive sales. Game launches to silence.
- **Mitigation**: HYPE's job is to build wishlist pre-launch (target: 10k wishlists at launch). If wishlist count is low (<5k), temper sales expectations but proceed with launch. Post-launch word-of-mouth is more important than launch-day spike for indie games.

**Dependencies**: Milestone 8 complete.

**Launch Day**: Week 78, ideally mid-week (Tuesday/Wednesday). CLOCK monitors launch in real-time. Team celebrates. Then we wait for player feedback and sales data.

---

## 3. Sprint Structure

### 3.1 Sprint Cadence

**Sprint Length**: 2 weeks (10 business days)
- Week 1: Development, daily stand-ups
- Week 2: Development, QA testing (CRASH tests builds daily), sprint review Friday

**Total Sprints**: 39 sprints over 78 weeks

**Sprint Goals**: Each sprint has a deliverable goal (e.g., "Racing drift mechanic functional," "Southside district geometry complete"). No sprint ends without a shippable artifact (even if it's a prototype).

### 3.2 Sprint Ceremonies

**Daily Stand-up** (10 min, 9:30am daily):
- What I did yesterday
- What I'm doing today
- Blockers (CLOCK unblocks)
- No problem-solving in stand-up (take detailed discussions offline)

**Sprint Planning** (2 hours, Monday Week 1):
- CLOCK presents sprint backlog (tasks for next 2 weeks)
- Team estimates tasks (t-shirt sizing: S, M, L, XL)
- Team commits to sprint goal
- Tasks assigned to owners

**Sprint Review** (1 hour, Friday Week 2):
- Demo what shipped this sprint (show the build, not slides)
- REED + NOVA + PIXEL + ECHO give feedback
- CLOCK updates roadmap based on actual velocity

**Sprint Retrospective** (30 min, Friday Week 2, after review):
- What went well?
- What went poorly?
- What should we change next sprint?
- CLOCK takes one action item from retro and implements it

### 3.3 Backlog Management

**Backlog Owner**: CLOCK (Producer)

**Backlog Priority**:
1. P0: Blockers (must fix immediately)
2. P1: Critical path (must ship for 1.0)
3. P2: Important but not critical (nice-to-have for 1.0)
4. P3: Stretch goals (post-launch)

**Backlog Grooming**: Every other Friday (off-week from sprint review), CLOCK + REED + BYTE review backlog for 1 hour. Re-prioritize, cut stale tasks, add new tasks based on learnings.

### 3.4 Sample Sprint Breakdown (First 10 Sprints)

**Sprint 1 (Weeks 1-2)**: Project setup
- Git repo initialized
- Unity project structure
- CI pipeline (GitHub Actions)
- First build (empty scene, but it builds)

**Sprint 2 (Weeks 3-4)**: Racing prototype kickoff
- Vehicle physics prototype (basic Rigidbody + forces)
- Input handling (steering, throttle)
- Test track (flat plane, no visuals)

**Sprint 3 (Weeks 5-6)**: Racing drift
- Drift state machine (grip/drift/exit)
- Tire smoke particles
- Drift scoring (+15 points/sec)

**Sprint 4 (Weeks 7-8)**: Racing AI opponents
- Waypoint system
- 3 AI cars follow waypoints
- Rubber-banding basic implementation

**Sprint 5 (Weeks 9-10)**: Racing Style Meter
- Style Meter UI (vertical bar)
- Near-miss detection
- Style Meter decay
- Results screen (placement, style rank)

**Sprint 6 (Weeks 11-12)**: Racing event structure
- EventManager system
- Event ScriptableObject data pipeline
- Race start/finish triggers
- REP/CASH award system

**Sprint 7 (Weeks 13-14)**: Racing polish + validation
- Audio (engine loops, tire squeal)
- Camera (Cinemachine setup)
- One more race test (playtest validation)

**Sprint 8 (Weeks 15-16)**: Fighting prototype kickoff
- Character controller
- Frame data system
- Hitbox/hurtbox detection

**Sprint 9 (Weeks 17-18)**: Fighting combat
- 4 moves implemented
- Combo system
- AI opponent behavior tree

**Sprint 10 (Weeks 19-20)**: Fighting Style Meter integration
- Combat feeds Style Meter
- Taunt mechanic
- Results screen

(Continue pattern for all 39 sprints. Full sprint-by-sprint breakdown is maintained in project management tool, not duplicated here.)

---

## 4. Task Breakdown (Sample: Milestone 1 - Racing Prototype)

This section shows the level of task granularity needed. Each milestone breaks into tasks, each task is 1-2 days max, each task has an owner, dependency, and priority.

| Task ID | Task Description | Owner | Est. (days) | Dependency | Priority | Sprint |
|---------|------------------|-------|-------------|------------|----------|--------|
| RAC-001 | Set up vehicle Rigidbody + collider | BYTE | 0.5 | None | P1 | 2 |
| RAC-002 | Implement steering input (axis to torque) | BYTE | 0.5 | RAC-001 | P1 | 2 |
| RAC-003 | Implement throttle/brake (velocity control) | BYTE | 1 | RAC-001 | P1 | 2 |
| RAC-004 | Create test track (flat plane, boundaries) | Env Artist | 1 | None | P1 | 2 |
| RAC-005 | Implement drift detection (slip angle calc) | BYTE | 1.5 | RAC-002, RAC-003 | P1 | 3 |
| RAC-006 | Drift state machine (grip/initiate/drift/exit) | BYTE | 2 | RAC-005 | P1 | 3 |
| RAC-007 | Tire smoke particle system | Tech Artist | 1 | RAC-006 | P1 | 3 |
| RAC-008 | Drift scoring (+15 pts/sec) | BYTE | 0.5 | RAC-006 | P1 | 3 |
| RAC-009 | Style Meter data structure | BYTE | 0.5 | None | P1 | 3 |
| RAC-010 | Style Meter UI (vertical bar) | UI Designer | 1 | RAC-009 | P1 | 5 |
| RAC-011 | Style Meter fill/decay logic | BYTE | 1 | RAC-009 | P1 | 5 |
| RAC-012 | Waypoint system (editor tool) | BYTE | 1.5 | None | P1 | 4 |
| RAC-013 | AI vehicle controller (follows waypoints) | BYTE | 2 | RAC-012 | P1 | 4 |
| RAC-014 | Spawn 3 AI opponents at race start | BYTE | 0.5 | RAC-013 | P1 | 4 |
| RAC-015 | Lap counter + position tracker | BYTE | 1 | None | P1 | 5 |
| RAC-016 | Near-miss detection (SphereCast proximity) | BYTE | 1 | RAC-003 | P1 | 5 |
| RAC-017 | Near-miss scoring (+40 pts) | BYTE | 0.5 | RAC-016, RAC-011 | P1 | 5 |
| RAC-018 | Nitrous input + impulse force | BYTE | 1 | RAC-003 | P1 | 6 |
| RAC-019 | Results screen UI (placement, style rank) | UI Designer | 2 | RAC-015, RAC-011 | P1 | 6 |
| RAC-020 | REP/CASH calculation logic | BYTE | 1 | RAC-019 | P1 | 6 |
| RAC-021 | Engine audio loops (3 layers: idle/mid/redline) | ECHO | 2 | None | P1 | 7 |
| RAC-022 | Tire squeal audio (drift intensity-based) | ECHO | 1 | RAC-006 | P1 | 7 |
| RAC-023 | Cinemachine camera setup (follow car, drift tilt) | BYTE | 1.5 | RAC-006 | P1 | 7 |
| RAC-024 | Performance profiling on Steam Deck | BYTE | 1 | All above | P0 | 7 |
| RAC-025 | Internal playtest (one more race test) | CLOCK + Team | 0.5 | RAC-024 | P0 | 7 |

**Total estimated days**: ~25 days of work (split across BYTE, artists, ECHO, UI designer). Fits within 3-month Milestone 1 timeline with buffer.

**Task Dependency Visualization**:
```
RAC-001 (Rigidbody) --> RAC-002 (Steering) --> RAC-005 (Drift detect) --> RAC-006 (Drift state) --> RAC-008 (Scoring)
                    --> RAC-003 (Throttle) ---> RAC-016 (Near-miss) ---> RAC-017 (Near-miss score)
                                           ---> RAC-018 (Nitrous)

RAC-009 (Style Meter data) --> RAC-010 (UI) --> RAC-011 (Fill/decay) --> RAC-017, RAC-020

RAC-012 (Waypoints) --> RAC-013 (AI controller) --> RAC-014 (Spawn AI)

RAC-015 (Lap/Position) --> RAC-019 (Results screen) --> RAC-020 (REP calc)

RAC-006, RAC-021, RAC-023 (Polish) --> RAC-024 (Performance test) --> RAC-025 (Playtest validation)
```

**Critical Path** (longest dependency chain): RAC-001 -> RAC-003 -> RAC-005 -> RAC-006 -> RAC-008 -> RAC-011 -> RAC-017 -> RAC-020 -> RAC-024 -> RAC-025 (approximately 11 days of sequential work). Everything else can parallelize.

This level of task breakdown exists for every milestone. CLOCK maintains this in project management software (Jira, Notion, or Trello). Team pulls tasks from backlog daily.

---

## 5. Risk Register

Every project has risks. The producer's job is to see them coming and mitigate before they kill the project.

### 5.1 High-Severity Risks

**RISK 1: Four-genre complexity overwhelms team**

**Severity**: CRITICAL
**Likelihood**: HIGH (multi-genre is inherently complex)
**Impact**: Development takes 2x longer than estimated, scope creep spirals, never ship

**Mitigation Plan**:
- Build one discipline at a time to shippable quality before starting next
- Validate fun through playtesting at each milestone (don't proceed if discipline fails validation)
- Hard scope cut deadlines: Month 6 (cut tricks if needed), Month 12 (cut 4th district if needed)
- Maintain "MVP version" of each discipline (e.g., basketball can be simplified to 1v1 instead of 2v2 if needed)

**Contingency**:
- If by Month 9, only 2 disciplines are shippable quality, cut to 3-discipline game (racing, fighting, one other)
- If by Month 12, only 1 discipline is truly polished, pivot to single-genre game (racing-only) with deep customization

**Risk Owner**: CLOCK (monitors monthly, escalates at first sign of slippage)

---

**RISK 2: Racing physics don't feel good**

**Severity**: CRITICAL (racing is first discipline, sets foundation)
**Likelihood**: MEDIUM (arcade physics are hard to tune)
**Impact**: Milestone 1 fails, project stalls

**Mitigation Plan**:
- Weekly playtests during Months 1-3 (every Friday, REED + BYTE present)
- Reference existing games constantly (NFS Underground 2 is the north star)
- Hire consultant if needed (experienced vehicle physics programmer, 1-week contract to review code)
- License vehicle physics asset if custom implementation fails (Edy's Vehicle Physics ~$100, proven solution)

**Contingency**:
- If racing still doesn't feel good by Week 10, license Edy's Vehicle Physics
- If licensed solution also fails, pivot entire project (extremely unlikely but possible)

**Risk Owner**: BYTE (owns implementation), escalates to CLOCK if stuck

---

**RISK 3: Rival AI feels dumb/scripted**

**Severity**: HIGH (rival system is a core pillar)
**Likelihood**: MEDIUM (emergent AI is hard)
**Impact**: Game loses its "Nemesis System" USP, becomes generic

**Mitigation Plan**:
- Heavy investment in rival personality variance (25-30 rivals, distinct profiles)
- NOVA writes detailed personality attributes (Pride, Confidence, Grudge weights per rival)
- Playtest specifically for rival stories (ask testers: "Tell me about your most memorable rival")
- Iterate on attribute weights based on playtest feedback

**Contingency**:
- If emergent AI doesn't produce interesting stories by Month 12, hand-script 5-6 key rivalries (narrative beats)
- Let remaining 20 rivals be procedural flavor (less ambitious but still functional)

**Risk Owner**: BYTE + NOVA (co-own), report to CLOCK monthly

---

**RISK 4: Performance doesn't hit 60fps on Steam Deck**

**Severity**: HIGH (Steam Deck is validation target)
**Likelihood**: MEDIUM (Unity + dense city can be demanding)
**Impact**: Game feels sluggish on portable, negative reviews

**Mitigation Plan**:
- Monthly profiling on Steam Deck hardware (borrow devkit or buy Steam Deck for testing)
- Aggressive LOD system (LOD0/1/2 for all assets)
- Draw call budgets enforced (max 500 per frame)
- Technical Artist dedicated to optimization (months 10-18)

**Contingency**:
- If 800p doesn't hit 60fps, drop internal resolution to 720p and upscale (URP supports FSR-like upscaling)
- If still struggling, reduce NPC density (fewer ambient crowd members)
- Absolute worst case: lock to 30fps on Steam Deck (not ideal but playable for these genres)

**Risk Owner**: BYTE (performance ownership), Technical Artist (optimization execution)

---

**RISK 5: Scope creep kills schedule**

**Severity**: CRITICAL (most common indie game failure mode)
**Likelihood**: HIGH (team always wants to add "just one more thing")
**Impact**: Never ship, or ship late and over-budget

**Mitigation Plan**:
- Locked feature list (this production plan defines 1.0 scope)
- Monthly scope reviews (CLOCK facilitates: "What can we cut to ship on time?")
- Feature freeze at Month 16 (no exceptions)
- "Nice-to-have" features explicitly tagged and cut first when schedule slips
- Hard deadline: Month 18 launch, no extensions

**Contingency**:
- Month 6 scope checkpoint: If behind, cut tricks discipline
- Month 9 scope checkpoint: If behind, cut 4th district or reduce event count
- Month 12 scope checkpoint: If behind, cut stretch goals (crew multiplayer, create-a-legend)
- Month 15 final call: Ship whatever exists, even if incomplete

**Risk Owner**: CLOCK (enforces ruthlessly, resists team pressure to add features)

---

### 5.2 Medium-Severity Risks

**RISK 6: Key team member leaves mid-project**

**Severity**: HIGH (small team, everyone is critical)
**Likelihood**: LOW (but always possible)
**Impact**: Knowledge loss, schedule slip, morale hit

**Mitigation**: Documentation culture (code comments, design docs updated, no one owns knowledge alone). Cross-training where possible (second programmer can cover for BYTE in emergency).

**Contingency**: Hire replacement ASAP (recruiter on retainer), remaining team covers gap for 2-4 weeks during hiring.

---

**RISK 7: Unity engine bug blocks development**

**Severity**: MEDIUM
**Likelihood**: LOW (LTS versions are stable)
**Impact**: Development stalls until bug is fixed or workaround found

**Mitigation**: Use Unity 2022.3 LTS (not experimental versions). Monitor Unity forums for known issues. Test on multiple machines (Windows, Linux).

**Contingency**: Downgrade to previous LTS patch version if new patch introduces bug. Report to Unity and wait for fix (typically 1-2 weeks).

---

**RISK 8: Steam's policies change (pricing, revenue share, etc.)**

**Severity**: LOW
**Likelihood**: LOW (Valve is stable)
**Impact**: Business model affected

**Mitigation**: Monitor SteamWorks developer news. Maintain relationships with Steam BD reps (if available).

**Contingency**: Adapt to new policies (can't avoid compliance). Budget flexibility to absorb small revenue share changes.

---

**RISK 9: External beta reveals fundamental flaw**

**Severity**: HIGH (late discovery is expensive to fix)
**Likelihood**: MEDIUM (beta is specifically designed to catch this)
**Impact**: Delay launch or ship with known issues

**Mitigation**: Conduct internal alpha testing thoroughly (Milestone 7) to catch major issues before external beta. Structure beta feedback form to identify pain points clearly.

**Contingency**: If beta feedback is harsh, CLOCK calls emergency meeting. Options: 1-month launch delay to fix, or simplify/cut broken feature and ship on time with reduced scope.

---

**RISK 10: Marketing doesn't drive wishlists/sales**

**Severity**: MEDIUM (affects revenue but not product quality)
**Likelihood**: MEDIUM (indie marketing is hard)
**Impact**: Low sales, but game still exists

**Mitigation**: HYPE starts marketing early (Month 14). Build Discord community pre-launch. Trailer and screenshots emphasize unique hook (four genres, Style Meter, 2000s aesthetic). Reddit/Twitter outreach.

**Contingency**: Post-launch word-of-mouth marketing. Reach out to streamers/YouTubers for coverage. Price aggressively if needed ($19.99 launch price with 10-20% launch discount).

---

### 5.3 Risk Review Cadence

**Monthly Risk Review** (1 hour, last Friday of each month):
- CLOCK presents risk register
- Team assesses: Has likelihood changed? Has impact changed?
- New risks added based on learnings
- Mitigation plans updated

**Escalation Protocol**:
- If any CRITICAL risk likelihood increases to HIGH, CLOCK escalates immediately (don't wait for monthly review)
- Emergency production meeting called within 48 hours
- Decision made: mitigate aggressively, cut scope, or (rarely) delay launch

---

## 6. Critical Path Visualization

The critical path is the longest sequence of dependent tasks. It defines the minimum project duration. You can't ship faster than the critical path.

### 6.1 Milestone-Level Critical Path

```
START (Week 0)
    |
    v
Milestone 0: Pre-Production (Weeks 0-2)
    |
    v
Milestone 1: Racing Prototype (Weeks 3-14) <-- CRITICAL: First discipline validation
    |
    v
Milestone 2: Fighting Prototype (Weeks 15-22) <-- CRITICAL: Second discipline validation
    |
    v
Milestone 3: Basketball Prototype (Weeks 23-26) <-- CRITICAL: Third discipline validation
    |
    v
Milestone 4: Vertical Slice (Weeks 26-27) <-- CRITICAL: Go/No-Go decision
    |
    v
Milestone 5: Tricks + Full District 1 (Weeks 28-39) <-- CRITICAL: Fourth discipline + foundation
    |
    v
Milestone 6: Content Production (Weeks 40-65) <-- CRITICAL: Longest phase, most parallelization
    |                                                          but still on critical path
    v
Milestone 7: Alpha (Weeks 66-69) <-- CRITICAL: Feature freeze, bug fixing
    |
    v
Milestone 8: Beta (Weeks 70-73) <-- CRITICAL: External validation
    |
    v
Milestone 9: Launch Prep (Weeks 74-78) <-- CRITICAL: Gold master, launch
    |
    v
LAUNCH (Week 78)
```

**Total Critical Path Duration**: 78 weeks (18 months)

**Critical Path Tasks** (examples within milestones):
- Racing physics implementation (Milestone 1, ~11 days sequential)
- Fighting frame data system (Milestone 2, ~8 days sequential)
- Progression system implementation (Milestone 5, ~10 days sequential)
- District 1 geometry production (Milestone 5, ~20 days sequential)
- Content production for Districts 2-4 (Milestone 6, ~60 days sequential per district, but can parallelize across 3 environment artists)

**What's NOT on Critical Path** (can parallelize):
- Audio implementation (ECHO works independently after disciplines are defined)
- UI design (UI Designer works independently after wireframes approved)
- Narrative writing (NOVA writes rival profiles, dialogue while systems are being built)
- Art asset creation (artists produce models while programmers implement systems, as long as placeholder assets allow programming to proceed)

**Key Insight**: The critical path is mostly **discipline implementation** (Milestones 1-5) and **content production** (Milestone 6). These are sequential or partially parallelizable. Everything else (audio, UI, narrative) can happen alongside.

**Optimization Opportunities**:
- If we cut tricks discipline (Milestone 5 becomes shorter), we save ~6 weeks
- If we reduce district count from 4 to 3 (Milestone 6 becomes shorter), we save ~8 weeks
- If we simplify rival AI (cut obsession/recruitment mechanics), we save ~4 weeks

Total potential time savings from scope cuts: 18 weeks (4.5 months). This means absolute minimum ship time is 60 weeks (15 months) if we cut aggressively. But quality would suffer. 78 weeks is the realistic timeline for the full vision.

---

## 7. Scope Management

### 7.1 Scope Management Philosophy

**Scope is the lever you pull when time and resources are fixed.**

We have 18 months and a team of 10-15 people. Time is fixed (hard launch deadline). Team size is roughly fixed (can't easily scale). Therefore, scope is the variable.

Every feature is categorized:
- **MUST-HAVE** (P1): Core to the game's identity. If cut, the game is fundamentally different.
- **SHOULD-HAVE** (P2): Important but not definitional. Enhances the experience but game is playable without it.
- **NICE-TO-HAVE** (P3): Stretch goals. Ship if time allows, defer to post-launch if not.

### 7.2 Scope Tiers

**MUST-HAVE (P1) — Non-Negotiable for 1.0**:
- 3 disciplines minimum (racing, fighting, one other) — ideally all 4, but basketball or tricks can be cut if needed
- Style Meter system (core innovation)
- REP progression with tier unlocks
- 3 districts minimum (Southside, Docks, one other) — ideally 4, but can cut to 3
- 15-20 rivals minimum (down from 25-30 if needed)
- Basic customization (10-15 cars, 10-15 movesets, basic fashion)
- One ending (Underground path) — can cut to single ending if branching proves too expensive
- 60+ events minimum (down from 100+ if needed)
- 60fps on Steam Deck

**SHOULD-HAVE (P2) — Defer if Schedule Slips**:
- Fourth discipline (tricks) — becomes post-launch DLC if cut
- Fourth district (Heights) — becomes post-launch DLC if cut
- Full rival roster (25-30 rivals) — reduce to 15-20 if needed
- Three-ending branching narrative — simplify to one or two endings
- Full customization depth (30-40 cars, 20-30 movesets, full fashion catalog) — reduce variety
- 100+ events — reduce to 60-80
- Crew recruitment mechanic (can simplify to passive bonuses only, cut active assists)
- Boss multi-phase events (can simplify to single-discipline boss fights)

**NICE-TO-HAVE (P3) — Stretch Goals, Post-Launch if Not in 1.0**:
- Crew vs. Crew multiplayer (async rivalry)
- Music rhythm integration (beat-synced Style Meter)
- Create-A-Legend mode (export AI rival)
- District editor (UGC)
- Fifth discipline (skateboarding)
- Photo mode
- Additional districts post-launch
- New Game Plus mode
- Modding support

### 7.3 Scope Cut Decision Points

**Month 6 (Vertical Slice)**: If vertical slice reveals scope is too large:
- Option 1: Cut tricks discipline → Ship with 3 disciplines (racing, fighting, basketball)
- Option 2: Reduce district count from 4 to 3 → Faster content production
- Decision criteria: Velocity data (how fast are we actually building vs. estimate?)

**Month 9 (Full District 1 + Tricks)**: If still behind schedule:
- Option 1: Cut 4th district (Heights) → Ship with 3 districts
- Option 2: Reduce event count from 100+ to 60-80 → Faster content production
- Option 3: Simplify rival AI (cut obsession mechanic) → Less complex implementation
- Decision criteria: Burn-down charts, remaining work vs. time left

**Month 12 (Mid-Production Checkpoint)**: If significantly behind:
- Option 1: Reduce rival count from 25-30 to 15-20 → Less content to create
- Option 2: Cut branching endings, ship with one ending → Less narrative complexity
- Option 3: Simplify customization (reduce car/move variety by 30%) → Less asset production
- Decision criteria: If less than 50% of content is complete, aggressive cuts needed

**Month 15 (Final Scope Lock)**: Last chance to cut before alpha:
- All P3 features definitely cut (already assumed)
- P2 features cut if not implemented by now
- Focus entirely on P1 features + bug fixing

**Rule**: Once scope is cut, it stays cut. No adding features back. Cut features go into "post-launch DLC wishlist."

### 7.4 Scope Creep Prevention

**How scope creep happens**:
- Designer: "Wouldn't it be cool if..."
- Programmer: "I could add this feature in just 2 days..."
- Team: "The community will love this..."

**How to prevent it**:
1. **Feature Freeze at Month 16** — Absolute, no exceptions. After feature freeze, only bug fixes and balance tuning.
2. **"Post-Launch Wishlist"** — When team suggests new features, CLOCK adds them to wishlist, not backlog. Validate demand post-launch before implementing.
3. **Monthly Scope Reviews** — CLOCK presents: "Here's what we cut this month to stay on schedule." Normalize cutting.
4. **Data-Driven Decisions** — Scope changes require data (playtest feedback, velocity data, burn-down charts), not opinions or excitement.
5. **CLOCK Has Final Authority** — On scope questions, CLOCK decides. Debate is healthy, but decision is final once made.

---

## 8. Communication & Reporting

### 8.1 Daily Communication

**Daily Stand-up** (10 min, 9:30am):
- Whole team, verbal (in-office) or Slack thread (remote)
- Three questions: What I did, what I'm doing, blockers
- CLOCK unblocks or assigns blocker resolution

**Slack/Discord Channels**:
- `#general` — General discussion, memes, team bonding
- `#dev-updates` — Code commits, build notifications, CI/CD alerts
- `#playtesting` — Playtest feedback, bug reports
- `#art` — Art WIP, feedback, asset handoffs
- `#audio` — Audio WIP, feedback, music/SFX handoffs
- `#design` — Design discussions, balance proposals
- `#production` — CLOCK's daily updates, sprint planning reminders
- `#blockers` — Urgent issues that need immediate attention

**Async Communication Preference**: Default to async (Slack, Notion docs). Meetings only when necessary (planning, reviews, retros). Respect focus time (no expectation of instant replies during "deep work" hours, 10am-2pm).

### 8.2 Weekly Reporting

**Friday Sprint Review** (1 hour, every other Friday):
- Demo build (show what shipped this sprint)
- Velocity review (how many tasks completed vs. estimated)
- Roadmap update (CLOCK shows: "We're here, we're going there, this is the risk")

**Friday Playtest** (1 hour, every Friday):
- Team plays latest build
- Structured feedback (what's fun, what's broken, what's confusing)
- CLOCK documents feedback, prioritizes fixes for next sprint

**Weekly Digest** (Mondays, CLOCK sends email):
- Last week's wins
- This week's priorities
- Blockers/risks to watch
- Morale check-in ("How's everyone feeling? Burned out? Energized?")

### 8.3 Monthly Reporting

**Monthly All-Hands** (2 hours, last Friday of month):
- Milestone progress review (are we on track?)
- Risk register update (what's changed?)
- Scope checkpoint (do we need to cut anything?)
- Financial health (if relevant — budget spent vs. remaining)
- Open Q&A (team asks CLOCK anything)

**Monthly Metrics Dashboard** (CLOCK maintains, shared with team):
- Velocity trend (tasks completed per sprint, over last 3 months)
- Burn-down chart (remaining work vs. time left)
- Bug count trend (P0/P1 bugs over time)
- Performance metrics (framerate on Steam Deck, updated monthly)
- Scope status (P1 features: % complete, P2 features: % complete)

### 8.4 External Communication (Months 14-18)

**Community Building** (HYPE + CLOCK):
- Discord server launched (Month 14)
- Weekly dev blog posts (Fridays, alternating between team members — REED writes about design, PIXEL about art, ECHO about audio, etc.)
- Twitter updates (2-3 times/week, GIFs of gameplay, behind-the-scenes screenshots)
- Reddit posts (r/gamedev, r/indiegaming — dev journey posts, "here's what we're building")

**Press Outreach** (HYPE):
- Month 16: Press kit assembled (fact sheet, screenshots, trailer, demo build)
- Month 17: Email outreach to indie game press, YouTubers, streamers
- Month 18: Launch week interviews, AMAs, press coverage

---

## 9. Quality Assurance Strategy

### 9.1 QA Philosophy

**QA is not a phase. QA is a discipline.**

CRASH (QA Lead) is on the team from Day 1. Testing happens continuously, not just at the end.

### 9.2 Testing Tiers

**Tier 1: Developer Testing** (Daily)
- Programmers test their own code before committing
- Designers playtest their own balance changes
- Artists validate assets in-engine before handoff
- No broken builds on `main` branch

**Tier 2: Smoke Testing** (Daily, automated)
- CI/CD pipeline runs smoke test on every commit
- Smoke test: Launch game, load district, no crashes within 60 seconds
- If smoke test fails, build is marked red, BYTE investigates immediately

**Tier 3: Sprint Testing** (Weekly)
- CRASH plays full sprint build (tests new features implemented this sprint)
- Files bugs in bug database (Jira/Trello/GitHub Issues)
- Prioritizes bugs (P0/P1/P2/P3)
- Reports to CLOCK at Friday sprint review

**Tier 4: Milestone Testing** (End of each milestone)
- Full team plays milestone build for 2-4 hours
- Structured playtesting (scenarios, test cases)
- CRASH coordinates and consolidates feedback

**Tier 5: External Testing** (Month 17, Beta)
- 50-100 external testers
- CRASH monitors feedback, triages bugs, prioritizes fixes

### 9.3 Bug Triage

**Priority Definitions**:
- **P0 (Blocker)**: Crashes, save corruption, progression blockers. Must fix immediately (within 24 hours).
- **P1 (Critical)**: Major gameplay issues (e.g., Style Meter not filling, AI opponents don't move). Fix within 1 week.
- **P2 (Major)**: Noticeable issues but game is playable (e.g., UI misalignment, SFX missing). Fix within 1 sprint.
- **P3 (Minor)**: Polish issues (e.g., typo in text, visual glitch on specific hardware). Fix if time allows, defer to post-launch if needed.

**Bug Fixing Priority**:
- P0 bugs: Drop everything, fix now
- P1 bugs: Top of next sprint backlog
- P2 bugs: Scheduled into sprints as bandwidth allows
- P3 bugs: "Nice to fix" list, addressed during polish sprints (Months 16-18)

**Bug Metrics Tracked**:
- Total bug count (trending up or down?)
- P0/P1 bug count (critical issues trending up or down?)
- Bug close rate (how many bugs fixed per sprint?)
- Bug reopens (bugs marked fixed but reappear — indicates insufficient testing or related issues)

**Goal**: By Month 16 (Alpha), P0 bugs = 0, P1 bugs < 10. By Month 17 (Beta), P0 bugs = 0, P1 bugs < 5. By Month 18 (Launch), P0 bugs = 0, P1 bugs = 0, P2 bugs < 20.

### 9.4 Performance Testing

**Monthly Performance Profiling** (BYTE + Technical Artist):
- Test on Steam Deck hardware (800p, lowest settings)
- Test on mid-tier PC (1080p, medium settings)
- Test on high-end PC (1440p, high settings)
- Measure: FPS (avg, min, max), frame time (1% lows), memory usage
- Identify bottlenecks (CPU, GPU, memory)
- Optimize worst offenders

**Performance Targets** (validated monthly):
- Steam Deck (800p): 60fps minimum, 55fps 1% lows
- Mid-tier PC (1080p): 90fps minimum, 75fps 1% lows
- High-end PC (1440p): 120fps minimum, 100fps 1% lows

**Performance Regression Testing**: After major changes (new district added, new discipline implemented), re-profile immediately. If FPS drops below target, identify cause and optimize before moving forward.

### 9.5 Balance Testing

**Economy Balance** (REED + CRASH):
- Playtest sessions with spending logs (track REP/CASH earned per hour, purchases made)
- Target: One meaningful purchase every 45-75 minutes of play
- If players are cash-starved (2+ hours between purchases), increase earnings or reduce costs
- If players are cash-rich (buying everything easily), reduce earnings or increase costs

**Difficulty Balance** (REED + CRASH):
- Track win/loss rates per discipline, per difficulty tier
- Target: 70-80% win rate on Tier 1 events, 50-60% win rate on Tier 3 events
- If win rates are too high, increase AI difficulty (opponent speed, aggression)
- If win rates are too low, reduce difficulty or improve player feedback (better tutorials)

**Style Meter Balance** (REED + CRASH):
- Track Style Meter fill rate per discipline (points per minute)
- Target: Reach UNDERGROUND MODE once every 5-7 minutes of active play
- If too frequent, reduce gain rates or increase threshold
- If too rare, increase gain rates or reduce decay

---

## 10. Post-Launch Plan

### 10.1 Day One Priorities

**Launch Day (Week 78)**: CLOCK + BYTE + CRASH on-call

**Hour 0-24** (First 24 hours post-launch):
- Monitor Steam forums, Discord, subreddit for crash reports
- BYTE investigates any critical bugs immediately
- Patch 1.0.1 ready to deploy if needed (P0 crash fixes)
- CLOCK tracks sales data, reviews, sentiment

**Week 1 Post-Launch**:
- Daily monitoring (CRASH reads all bug reports)
- Patch 1.0.1 deployed if critical bugs found (typically within 3-7 days)
- HYPE monitors reviews, responds to player feedback
- CLOCK assesses: Is reception positive? Are sales meeting projections?

**Month 1 Post-Launch**:
- Patch 1.1 (balance tuning, P1/P2 bug fixes, QOL improvements based on feedback)
- Community engagement (Discord AMA, Reddit posts, respond to YouTubers/streamers)
- Sales milestone celebrations (10k units sold, etc.)

### 10.2 Post-Launch Content Roadmap (if game succeeds)

**Success Criteria**: 10k units sold in first month = profitable, greenlight post-launch content

**Patch Roadmap** (first 6 months post-launch):
- **Patch 1.1** (Month 1): Balance tuning, bug fixes, QOL improvements
- **Patch 1.2** (Month 2): Performance optimization, additional balance pass
- **Patch 1.3** (Month 3): New cars/moves (free update, 5-10 new items)
- **DLC 1** (Month 4-5): Cut content restoration (if tricks or 4th district was cut, release as paid DLC $4.99-9.99)
- **DLC 2** (Month 6-8): New district + new rivals (paid DLC $9.99-14.99)
- **Major Update** (Month 9-12): Crew vs. Crew multiplayer (if community requests it, free update)

**DLC Development**: Only proceed if sales justify it (10k+ units). DLC is built with skeleton crew (2-3 people), not full team. Full team moves to next project.

### 10.3 Metrics to Track Post-Launch

**Sales Metrics**:
- Units sold (daily, weekly, monthly)
- Revenue (after platform cuts)
- Refund rate (Steam allows refunds within 2 hours playtime)
- Wishlist conversion rate (% of wishlisters who purchase)

**Player Metrics** (via Steam API + optional analytics):
- Daily Active Users (DAU)
- Average session length (target: 60-90 minutes)
- Completion rate (% of players who reach credits)
- Discipline usage (are all four disciplines played? If one is ignored, it's a design problem)
- REP distribution (where do players plateau? Indicates difficulty spikes or content gaps)

**Community Metrics**:
- Steam reviews (% positive, total count)
- Discord member count
- Reddit subscriber count (if dedicated subreddit exists)
- YouTube/Twitch coverage (views, hours watched)

**Goal Metrics** (defines success):
- 10k units in Month 1 = Break even, profitable
- 70%+ positive Steam reviews = Quality validated
- 50k units in Year 1 = Strong success, fund sequel/major DLC
- 100k+ units = Breakout indie hit, consider console ports

### 10.4 Failure Plan (if game flops)

**Failure Criteria**: <5k units in first month, <50% positive reviews

**Response**:
- Conduct post-mortem (what went wrong? Design? Marketing? Pricing?)
- Assess if game is salvageable (can we patch to improve reception?)
- If yes: Deploy aggressive patches, reduce price, seek influencer coverage
- If no: Accept failure, document learnings, move on to next project

**Lessons to Document**:
- What worked (likely: individual discipline feel, Style Meter concept, 2000s aesthetic)
- What didn't work (likely: genre-switching confusion, rival AI not landing, economy balance off)
- What we'd do differently (scope tighter, prototype more, validate cross-discipline flow earlier)

Post-mortems are not blame sessions. They're learning sessions. Failure is data.

---

## 11. Team Health & Morale Management

### 11.1 Crunch Policy

**Hard Rule: No Mandatory Crunch**

40-hour work weeks are standard. If the schedule requires crunch, the schedule is wrong. Cut scope instead.

**Voluntary Crunch**: If individual team members want to work extra hours (because they're excited, not because they feel pressured), that's their choice. But:
- No expectation of extra hours from CLOCK or leads
- No competitive "who works longest" culture
- Extra hours do not earn special recognition (we celebrate shipped features, not hours worked)

**Why No Crunch**:
- Crunch is a producer failure (I failed to scope correctly)
- Crunch burns people out (retention > shipping one game faster)
- Crunch produces bugs (tired people make mistakes)
- Crunch is not sustainable (this is an 18-month project, not a 6-week sprint)

**If We're Behind Schedule**: Cut scope. That's the producer's job. Protect the team from the schedule, not the schedule from the team.

### 11.2 Morale Monitoring

**Monthly One-on-Ones** (CLOCK meets with each team member, 30 min):
- How are you feeling about the project?
- Are you excited about what you're working on?
- Is anything blocking you or frustrating you?
- Do you have concerns about the schedule/scope?
- Is work-life balance healthy?

**Team Health Indicators** (CLOCK watches for):
- Declining sprint velocity (team is slowing down = possible burnout)
- Increased sick days (stress manifests physically)
- Negative tone in Slack/stand-ups (frustration, cynicism)
- Decreased engagement in playtests (team stops caring)

**Morale Interventions** (if needed):
- Milestone celebrations (pizza lunch, team outing, bonus day off after major milestone)
- Scope cuts (if team feels overwhelmed, cut features to reduce pressure)
- Task rotation (if someone is bored/stuck, let them work on something else for a sprint)
- Bring in help (contract worker to handle grunt work, free up core team for creative tasks)

**Goal**: Team should be energized and proud of what we're building. If morale drops, address immediately. A burned-out team ships nothing.

### 11.3 Conflict Resolution

**Conflicts Happen**: Design disagreements, technical debates, personality clashes. This is normal.

**Conflict Resolution Process**:
1. **Direct conversation first**: Two people in conflict talk directly (no CLOCK mediation yet). Most conflicts resolve here.
2. **Lead mediation**: If unresolved, relevant lead (REED for design, BYTE for tech, etc.) mediates.
3. **CLOCK mediation**: If still unresolved, CLOCK mediates. Listen to both sides, make decision based on project goals.
4. **Decision is final**: Once CLOCK decides, debate ends. Execute.

**Healthy Conflict**: Disagreement is good. It means people care. Encourage debate, but:
- Attack ideas, not people
- Assume good intent
- Data over opinions (use playtest data, velocity data, reference games)
- Timebox debates (30 min max, then decide)

**Unhealthy Conflict**: Personal attacks, silent treatment, sabotage. This is unacceptable. If it happens, CLOCK addresses immediately (private conversation, warning, removal from project if behavior continues).

---

## 12. Conclusion: What Success Looks Like

**Month 18, Week 78**: UNDERGROUND launches on Steam.

**Success is**:
- Game is playable start-to-finish (30-40 hours to credits)
- Three disciplines minimum (ideally four) feel tight and integrated
- Style Meter works across all disciplines (cross-discipline innovation lands)
- Rival AI produces emergent stories (at least 50% of players report memorable rivalries)
- 60fps on Steam Deck (performance target met)
- 70%+ positive Steam reviews (quality validated)
- 10k+ units sold in Month 1 (profitable, sustainable)

**Success is NOT**:
- Perfect execution (there will be bugs, balance issues, cut features)
- Critical acclaim (nice-to-have, not required)
- Viral hit (we're not chasing TikTok fame, we're building a solid game)
- Everything we envisioned (scope cuts are inevitable, and that's okay)

**The Producer's Job**: Ship a game the team is proud of, on time, without burning people out. Scope is the lever. Use it early and often.

**What We're Building**: The 2000s street culture game that never existed. Four genres unified by one progression spine, 2000s aesthetic with 2026 systems depth, emergent AI rivalries. It's ambitious. It's risky. It's achievable if we stay disciplined.

**Core Production Principle**: A shipped game beats a perfect concept. Cut scope, not corners. Profile before optimizing. Iterate relentlessly. Protect the team. Ship it.

**Final Note**: This plan will change. Features will be cut. Timelines will slip. Crises will emerge. That's production. The plan is not the goal. Shipping a game we're proud of is the goal. This plan is the map. Let's start walking.

---

**Next Actions** (Week 1):
1. CLOCK schedules kickoff meeting (Week 0)
2. BYTE initializes Unity project + Git repo
3. REED finalizes racing prototype design doc
4. Team reads all design documents (pitch, GDD, narrative bible, art direction, sound design, tech architecture)
5. Sprint 1 backlog created (first 2 weeks of tasks)
6. Daily stand-ups begin (9:30am daily)

**Document Status**: Production Roadmap — Ready for Execution
**Version**: 1.0
**Owner**: CLOCK (Producer)
**Last Updated**: 2026-02-07

---

Now let's ship a game.

— CLOCK
