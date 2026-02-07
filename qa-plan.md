# UNDERGROUND — QA Plan

**Author**: CRASH (QA Lead)
**Status**: First Pass - Ready for Implementation
**Version**: 1.0
**Date**: 2026-02-07

---

## 1. Executive Summary

UNDERGROUND is four games pretending to be one. Racing, fighting, basketball, and tricks, all unified by a Style Meter and a REP economy, all running at 60fps on Steam Deck, all with emergent AI that remembers every humiliation you've inflicted.

This is the most complex thing this studio has attempted. It will break in ways we haven't imagined yet.

My job is to find every break before the player does. Every single one. The complexity isn't the enemy — shipping broken is the enemy. This document defines how we test a multi-genre game that has never been built before, with systems interacting in ways no other game has tried.

**Testing philosophy**: Test each discipline in isolation first. Then test the seams between them. Then stress-test the progression systems that tie it all together. Then test on minimum spec hardware until it bleeds. Then test again.

**Quality gates**: Nothing ships without passing the gates defined in section 9. No exceptions. Not for deadlines, not for features, not for marketing.

**Critical path**: Racing → Fighting → Basketball → Tricks → Cross-discipline integration → Rival AI → Progression economy → Performance validation → Full regression. In that order. If racing doesn't work, nothing else matters.

---

## 2. Test Plan by Feature Area

### 2.1 Racing System

**What we're testing**: Arcade racing with drift mechanics, Style Meter integration, 8-opponent AI, rubber-banding, nitrous, near-miss detection, waypoint navigation.

#### Test Cases: Core Racing Mechanics

**TC-RACE-001: Basic Vehicle Control**
- Preconditions: Player in racing event, stock car equipped
- Steps:
  1. Accelerate using throttle input
  2. Brake using brake input
  3. Steer left and right
  4. Verify vehicle responds to all inputs within 1 frame (16.67ms at 60fps)
- Expected: Vehicle accelerates, brakes, and steers with no input lag. No camera jitter. No clipping through track geometry.
- Priority: P0 (blocker)

**TC-RACE-002: Drift Initiation and Scoring**
- Preconditions: Player in racing event, approaching corner at 60+ kph
- Steps:
  1. Steer into corner while maintaining throttle
  2. Observe drift angle (velocity direction vs. facing direction)
  3. Hold drift for 3+ seconds
  4. Verify Style Meter increases by ~45 points (15/sec * 3)
  5. Verify visual feedback (tire smoke, underglow trail, screen effect)
- Expected: Drift triggers at >15-degree angle between velocity and facing. Style Meter gains are accurate (+/- 5 points). VFX are visible and synced to drift state.
- Priority: P0

**TC-RACE-003: Drift State Transitions**
- Preconditions: Player in racing event
- Steps:
  1. Enter drift (Grip → Drifting)
  2. Verify state transition occurs smoothly
  3. Exit drift by reducing steering angle (Drifting → Grip)
  4. Verify no physics pop or camera snap
  5. Re-enter drift immediately (Grip → Drifting)
- Expected: State machine transitions are smooth. No sudden velocity changes. Camera lerps between states, no hard cuts.
- Priority: P0

**TC-RACE-004: Nitrous Boost**
- Preconditions: Player in race, nitrous equipped and charged
- Steps:
  1. Activate nitrous
  2. Verify speed increase (should reach max speed 20-30% faster)
  3. Verify VFX (screen blur, nitrous flames)
  4. Verify nitrous depletes over duration
  5. Verify cooldown period before recharge
- Expected: Nitrous provides noticeable speed boost. Visual/audio feedback is immediate. No infinite nitrous exploit.
- Priority: P1

**TC-RACE-005: Near-Miss Detection**
- Preconditions: Player in race with traffic or opponents nearby
- Steps:
  1. Drive within 1m of obstacle at 60+ kph
  2. Verify Style Meter +40 points awarded
  3. Verify near-miss VFX (slow-mo flash, screen shake)
  4. Verify near-miss does NOT trigger if speed <40 kph
  5. Verify multiple near-misses in sequence award points for each
- Expected: Near-miss detection is consistent. Points awarded once per obstacle per proximity event. No double-counting.
- Priority: P1

**TC-RACE-006: Lap Completion and Position Tracking**
- Preconditions: Player in 3-lap race with 8 opponents
- Steps:
  1. Complete lap 1
  2. Verify lap counter updates (1/3 → 2/3)
  3. Verify position display updates based on race order
  4. Cross finish line after 3 laps
  5. Verify race ends and results screen triggers
- Expected: Lap tracking is accurate. Position never shows impossible values (0th place, 10th place in 9-car race). Finish line detection is reliable.
- Priority: P0

#### Test Cases: AI Opponents

**TC-RACE-AI-001: Opponent Pathfinding**
- Preconditions: Race with 8 AI opponents
- Steps:
  1. Observe AI opponent navigation for full race
  2. Verify AI follows waypoints correctly
  3. Verify AI does not get stuck on geometry
  4. Verify AI takes corners at reasonable speeds
- Expected: AI completes race without getting stuck. AI pathing looks intentional, not random. AI doesn't stop mid-track unless crashed.
- Priority: P0

**TC-RACE-AI-002: Rubber-Banding (Player Ahead)**
- Preconditions: Player in 1st place by 200+ meters
- Steps:
  1. Maintain large lead for 30+ seconds
  2. Check opponent speeds (via debug overlay if available)
  3. Verify opponents receive speed boost to catch up
  4. Verify player can still win with skilled driving
- Expected: AI gets faster when player is far ahead, but not impossibly fast. Player should still be able to win with clean racing.
- Priority: P1

**TC-RACE-AI-003: Rubber-Banding (Player Behind)**
- Preconditions: Player in 8th place by 200+ meters
- Steps:
  1. Stay far behind for 30+ seconds
  2. Verify opponents slow down to keep race competitive
  3. Verify player can catch up with moderate skill
- Expected: AI slows when player is far behind. Race remains winnable for struggling players.
- Priority: P1

**TC-RACE-AI-004: AI Collision Behavior**
- Preconditions: Race with opponents
- Steps:
  1. Collide with AI opponent at high speed
  2. Verify physics response (both cars react)
  3. Verify AI recovers and continues racing
  4. Verify AI doesn't infinitely ram player
- Expected: Collisions feel physical but fair. AI doesn't grief player. AI recovers from crashes within 3 seconds.
- Priority: P1

#### Test Cases: Edge Cases

**TC-RACE-EDGE-001: Wrong-Way Driving**
- Preconditions: Player in race
- Steps:
  1. Turn car around and drive backwards on track
  2. Verify "Wrong Way" warning appears after 3 seconds
  3. Continue wrong-way for 10+ seconds
  4. Verify car is respawned facing correct direction after 10 seconds
- Expected: Wrong-way detection triggers. Respawn is automatic after grace period. No soft-lock.
- Priority: P2

**TC-RACE-EDGE-002: Out of Bounds**
- Preconditions: Player in race
- Steps:
  1. Drive off track into invalid area (water, off-map void)
  2. Verify respawn triggers within 3 seconds
  3. Verify car respawns on track, facing correct direction
  4. Verify no loss of position beyond natural race progression during respawn
- Expected: OOB detection is fast. Respawn is clean. No falling through world geometry.
- Priority: P0

**TC-RACE-EDGE-003: Finish Line Edge Case (Nearly Tied)**
- Preconditions: Player and AI opponent neck-and-neck at finish
- Steps:
  1. Cross finish line within 0.1 seconds of opponent
  2. Verify position assignment is consistent
  3. Replay scenario 5 times
  4. Verify same positions for same relative crossing times
- Expected: Position calculation is deterministic. No random flip-flopping in photo finishes.
- Priority: P2

**TC-RACE-EDGE-004: Zero Opponents (Solo Race)**
- Preconditions: Race event configured with 0 opponents (if possible via config)
- Steps:
  1. Start race
  2. Verify race starts and runs normally
  3. Complete race
  4. Verify results screen shows 1st place
- Expected: Game handles solo races without crashing. Edge case for tutorial or time trial modes.
- Priority: P3

**TC-RACE-EDGE-005: Car Stuck on Geometry**
- Preconditions: Player in race
- Steps:
  1. Deliberately wedge car between obstacles (walls, barriers)
  2. Attempt to free car using throttle/reverse
  3. If stuck for 5+ seconds, verify auto-unstuck triggers (nudge or respawn)
- Expected: Player is never permanently stuck. Auto-recovery within 5 seconds if no player input resolves it.
- Priority: P1

### 2.2 Fighting System

**What we're testing**: Frame-data-driven combat, hitbox/hurtbox detection, combo system, hitstun, blocking, taunting, rival AI behavior trees.

#### Test Cases: Core Combat Mechanics

**TC-FIGHT-001: Basic Attack Execution**
- Preconditions: Player in fight, opponent at medium range
- Steps:
  1. Execute light attack (button press)
  2. Verify startup frames (animation starts)
  3. Verify active frames (hitbox appears, shown via debug overlay if available)
  4. Verify recovery frames (character returns to idle)
  5. Verify total frame count matches design spec (4-6 startup + 2-3 active + 8-10 recovery)
- Expected: Attack animation plays. Hitbox timing matches frame data. No hitbox persists after active frames.
- Priority: P0

**TC-FIGHT-002: Hit Detection (Clean Hit)**
- Preconditions: Player attacking, opponent in range and not blocking
- Steps:
  1. Execute light attack with opponent in hitbox range during active frames
  2. Verify hit connects (damage applied, hitstun triggered)
  3. Verify hit VFX (impact flash, screen shake)
  4. Verify hit SFX plays
  5. Verify Style Meter increases by move's style value
- Expected: Hit detection is frame-accurate. Damage applied matches move data. Visual/audio feedback is immediate.
- Priority: P0

**TC-FIGHT-003: Blocking**
- Preconditions: Player defending, opponent attacking
- Steps:
  1. Hold block input
  2. Verify block animation plays
  3. Have opponent attack
  4. Verify attack is blocked (reduced/no damage, no hitstun)
  5. Verify block VFX (block spark)
- Expected: Blocking negates or reduces damage. Player is not stunned while blocking. Block is responsive.
- Priority: P0

**TC-FIGHT-004: Combo System (3-Hit Combo)**
- Preconditions: Player in fight, opponent not blocking
- Steps:
  1. Execute Light → Light → Heavy input sequence
  2. Verify each hit connects
  3. Verify combo counter displays (1 → 2 → 3 hits)
  4. Verify total damage is sum of all hits
  5. Verify Style Meter bonus for combo (progressive per hit after 2nd)
- Expected: Combo links work within cancel windows. Combo counter is accurate. Style gains increase per hit in combo.
- Priority: P0

**TC-FIGHT-005: Combo Drop (Invalid Link)**
- Preconditions: Player in fight
- Steps:
  1. Execute Light attack
  2. Wait until recovery frames complete
  3. Execute second Light attack (outside cancel window)
  4. Verify second attack starts fresh (combo does NOT continue)
  5. Verify combo counter resets to 1
- Expected: Combo system respects frame data cancel windows. Invalid links reset combo.
- Priority: P1

**TC-FIGHT-006: Taunt Mechanic**
- Preconditions: Player in fight, Style Meter <1000
- Steps:
  1. Execute taunt input
  2. Verify taunt animation plays (duration: 1.2 seconds / 72 frames at 60fps)
  3. Verify player is vulnerable during taunt (cannot block, cannot cancel)
  4. If taunt completes uninterrupted, verify +60 Style Meter
  5. If opponent hits player during taunt, verify hit connects normally
- Expected: Taunt is high-risk/high-reward. Full vulnerability during animation. Style bonus only if completed.
- Priority: P1

**TC-FIGHT-007: Health Depletion and KO**
- Preconditions: Player in fight, opponent at low health
- Steps:
  1. Execute attack that depletes opponent health to 0
  2. Verify KO triggers (opponent enters KO animation, does not stand back up)
  3. Verify fight ends and results screen appears
  4. Verify player is awarded round win
- Expected: KO is clean. Fight ends immediately on health depletion. No post-KO attacks possible.
- Priority: P0

#### Test Cases: AI Opponents

**TC-FIGHT-AI-001: Aggressive AI Behavior**
- Preconditions: Fight against rival with Aggressive personality
- Steps:
  1. Observe AI behavior over 60 seconds
  2. Count attack frequency vs. block frequency
  3. Verify Aggressive AI attacks >60% of the time
  4. Verify AI uses pressure tactics (moves forward, closes distance)
- Expected: Aggressive AI feels aggressive. High attack frequency. Less blocking.
- Priority: P1

**TC-FIGHT-AI-002: Defensive AI Behavior**
- Preconditions: Fight against rival with Defensive personality
- Steps:
  1. Observe AI behavior over 60 seconds
  2. Count block frequency and counter-attack attempts
  3. Verify Defensive AI blocks >50% of player attacks
  4. Verify AI uses counter-attacks after successful blocks
- Expected: Defensive AI feels cautious. High block rate. Reactive, not proactive.
- Priority: P1

**TC-FIGHT-AI-003: AI Combo Execution**
- Preconditions: Fight against mid-tier opponent
- Steps:
  1. Observe AI attacks over multiple rounds
  2. Verify AI can execute 3+ hit combos
  3. Verify AI doesn't spam single moves infinitely
  4. Verify AI combos respect frame data (valid links only)
- Expected: AI fights like a player. Uses combos, not just mashing. Feels competent.
- Priority: P1

**TC-FIGHT-AI-004: AI Difficulty Scaling**
- Preconditions: Fights against Tier-1, Tier-3, and Tier-5 opponents
- Steps:
  1. Fight each tier for 3 rounds
  2. Measure time-to-KO for each tier
  3. Verify higher-tier opponents are harder (take longer to defeat)
  4. Verify difficulty scales through AI competence (better combos, better blocking), not just damage/health buffs
- Expected: Difficulty curve is noticeable. Tier-5 feels legitimately hard. Scaling is fair, not cheap.
- Priority: P1

#### Test Cases: Edge Cases

**TC-FIGHT-EDGE-001: Simultaneous KO (Double KO)**
- Preconditions: Both fighters at very low health
- Steps:
  1. Execute simultaneous attacks that KO both fighters
  2. Verify game handles double KO gracefully
  3. Verify results screen shows tie or retry option
- Expected: Game doesn't crash or soft-lock. Outcome is deterministic (draw, retry, or first-to-hit wins).
- Priority: P2

**TC-FIGHT-EDGE-002: Infinite Combo Prevention**
- Preconditions: Player against low-skill AI
- Steps:
  1. Attempt to execute 10+ hit combo by finding AI exploit
  2. Verify hitstun degradation or combo breaker mechanic prevents infinite
  3. Verify AI can recover after max combo length
- Expected: No true infinites. Combo system has natural cap (hitstun decay, knockback, or breaker). AI is never helpless.
- Priority: P1

**TC-FIGHT-EDGE-003: Hit Priority (Simultaneous Attacks)**
- Preconditions: Player and AI execute attacks on same frame
- Steps:
  1. Time attacks to collide (both active frames overlap)
  2. Verify outcome is consistent (both hit, neither hit, or priority system decides)
  3. Repeat 10 times to verify determinism
- Expected: Simultaneous hits have clear, consistent resolution. No random outcomes.
- Priority: P2

**TC-FIGHT-EDGE-004: Hitbox Lingering Bug**
- Preconditions: Player in fight
- Steps:
  1. Execute attack
  2. Verify hitbox disappears after active frames end
  3. Move toward opponent during recovery frames
  4. Verify no phantom hits occur (hitbox must not persist)
- Expected: Hitboxes are frame-accurate. No lingering hitboxes after active frames.
- Priority: P0

**TC-FIGHT-EDGE-005: Frame-Perfect Input Buffer**
- Preconditions: Player in fight
- Steps:
  1. Execute combo with frame-perfect timing (input second move during cancel window)
  2. Execute same combo with 1-frame-late input (just outside cancel window)
  3. Verify frame-perfect input links combo
  4. Verify late input does NOT link (combo drops)
- Expected: Frame data is respected. 1 frame makes the difference between link and drop. This is hard but fair.
- Priority: P1

### 2.3 Basketball System

**What we're testing**: 2v2 streetball, ball physics, shooting mechanics, crossover system, AI teammate/opponent behavior, score tracking.

#### Test Cases: Core Basketball Mechanics

**TC-BALL-001: Ball Possession and Dribbling**
- Preconditions: Player in basketball event, has ball possession
- Steps:
  1. Move player character with ball
  2. Verify ball follows player (IK-driven animation)
  3. Verify dribble animation loops continuously
  4. Verify ball physics is disabled while dribbling (ball is kinematic, not physics-driven)
- Expected: Ball sticks to player hands during dribble. No physics glitches. Ball doesn't clip through floor.
- Priority: P0

**TC-BALL-002: Shooting Mechanics**
- Preconditions: Player has ball, near hoop
- Steps:
  1. Press shoot button
  2. Verify shooting animation plays
  3. Verify ball is released from hands at correct frame
  4. Verify ball trajectory arcs toward hoop (projectile physics)
  5. If shot is good (timing/position), ball enters hoop trigger
  6. Verify score updates (1 or 2 points depending on distance)
- Expected: Shot feels responsive. Ball physics are believable. Hoop detection is reliable.
- Priority: P0

**TC-BALL-003: Crossover Mechanic (Success)**
- Preconditions: Player has ball, defender within 2m
- Steps:
  1. Execute crossover input during timing window (200ms)
  2. Verify defender is moving in wrong direction during window
  3. Verify ankle-breaker triggers (defender stun animation, slow-mo, VFX)
  4. Verify +35 Style Meter awarded
  5. Verify player gains brief speed boost
- Expected: Crossover feels impactful. Timing window is tight but fair. Defender reaction is obvious.
- Priority: P1

**TC-BALL-004: Crossover Mechanic (Fail)**
- Preconditions: Player has ball, defender within 2m
- Steps:
  1. Execute crossover input when defender is well-positioned
  2. Verify crossover fails (defender doesn't fall)
  3. Verify turnover occurs (ball goes to defender)
  4. Verify player loses possession cleanly (no stuck state)
- Expected: Failed crossover has consequence. Turnover is clean. Defender takes possession.
- Priority: P1

**TC-BALL-005: Passing**
- Preconditions: Player has ball, AI teammate is open
- Steps:
  1. Press pass button while aiming at teammate
  2. Verify ball is thrown to teammate
  3. Verify teammate catches ball (possession transfers)
  4. Verify passing animation is smooth
- Expected: Passing is reliable. AI catches 95%+ of reasonable passes. No ball teleportation.
- Priority: P0

**TC-BALL-006: Score Tracking (1-Point and 2-Point)**
- Preconditions: 2v2 game in progress
- Steps:
  1. Score from inside arc (should award 1 point)
  2. Verify score updates correctly (+1)
  3. Score from outside arc (should award 2 points)
  4. Verify score updates correctly (+2)
  5. Verify first team to 11 points wins
  6. Verify game ends and results screen appears
- Expected: Score tracking is accurate. Win condition triggers at 11 points. No off-by-one errors.
- Priority: P0

#### Test Cases: AI Teammates and Opponents

**TC-BALL-AI-001: AI Teammate Positioning**
- Preconditions: Player has ball, AI teammate on player's team
- Steps:
  1. Hold ball and observe AI teammate for 10 seconds
  2. Verify AI moves to open position
  3. Verify AI doesn't stand idle
  4. Verify AI calls for pass (UI indicator or audio cue)
- Expected: AI teammate is helpful. Positions intelligently. Player can pass to AI and trust they'll be useful.
- Priority: P1

**TC-BALL-AI-002: AI Teammate Shooting**
- Preconditions: Pass ball to AI teammate when they're open
- Steps:
  1. AI receives pass
  2. Observe AI decision-making (shoot or pass back)
  3. If AI shoots, verify shot attempt is reasonable (not impossible angle)
  4. Verify AI shot success rate is calibrated (40-60% depending on difficulty)
- Expected: AI teammate doesn't sabotage player. Makes smart decisions. Feels competent.
- Priority: P1

**TC-BALL-AI-003: Opponent Defender Behavior**
- Preconditions: Player has ball, opponent defender nearby
- Steps:
  1. Observe defender AI for 10 seconds
  2. Verify defender stays between player and hoop
  3. Verify defender reacts to crossover attempts
  4. Verify defender attempts steals when player is stationary
- Expected: Defender AI feels like opposition. Applies pressure. Reacts to player actions.
- Priority: P1

**TC-BALL-AI-004: AI Difficulty Scaling (Shooting Accuracy)**
- Preconditions: Games against Tier-1, Tier-3, Tier-5 opponents
- Steps:
  1. Play full game against each tier
  2. Track opponent shooting accuracy
  3. Verify higher tiers have higher accuracy (Tier-1: 40%, Tier-5: 70%)
  4. Verify player can still win with skill
- Expected: Difficulty scales noticeably but fairly. Tier-5 is hard but not impossible.
- Priority: P1

#### Test Cases: Edge Cases

**TC-BALL-EDGE-001: Ball Out of Bounds**
- Preconditions: Ball in play
- Steps:
  1. Pass or shoot ball out of court boundaries
  2. Verify OOB detection triggers
  3. Verify possession is awarded to correct team (opposite of last touch)
  4. Verify ball respawns at inbound position
- Expected: OOB is detected reliably. Possession logic is correct. No ball lost in void.
- Priority: P0

**TC-BALL-EDGE-002: Stuck Ball (On Rim)**
- Preconditions: Player shoots ball
- Steps:
  1. Shoot at angle that causes ball to get stuck on rim (wedged in collision)
  2. Observe for 5 seconds
  3. Verify ball auto-resets if stuck (falls through or respawns)
- Expected: Ball never stays stuck permanently. Auto-recovery within 5 seconds.
- Priority: P2

**TC-BALL-EDGE-003: Simultaneous Shot Attempts**
- Preconditions: Two players (or player + AI) shoot at same time
- Steps:
  1. Trigger simultaneous shot animations
  2. Verify game handles two balls in flight gracefully (or only one ball exists)
  3. Verify scoring logic is correct for whichever ball enters hoop first
- Expected: Game handles edge case without crash. Only one ball scores per possession.
- Priority: P3

**TC-BALL-EDGE-004: AI Teammate Ball Hogging**
- Preconditions: Pass to AI teammate repeatedly
- Steps:
  1. Pass ball to AI 5 times in a row
  2. Observe AI behavior (does AI pass back or keep shooting?)
  3. Verify AI doesn't hog ball infinitely (should pass back or shoot within 10 seconds)
- Expected: AI shares the ball. Game doesn't become AI-only. Player stays engaged.
- Priority: P2

### 2.4 Tricks System

**What we're testing**: Tony Hawk-style trick system, score attack, combo linking, grind mechanics, manual balance, bail detection, landing precision.

#### Test Cases: Core Trick Mechanics

**TC-TRICK-001: Basic Trick Execution**
- Preconditions: Player in trick event, airborne
- Steps:
  1. Execute trick input (e.g., Grab + Up for Indy)
  2. Verify trick animation plays
  3. Verify trick name displays on screen
  4. Verify base score is awarded when landing cleanly
- Expected: Trick triggers reliably. Animation matches input. Score is awarded on landing, not during air.
- Priority: P0

**TC-TRICK-002: Trick Combo Linking**
- Preconditions: Player airborne off ramp
- Steps:
  1. Execute first trick (e.g., Grab trick)
  2. While still airborne, execute second trick (e.g., Flip trick)
  3. Verify combo counter updates (x2 multiplier)
  4. Land cleanly
  5. Verify total score = (trick1 + trick2) * multiplier
- Expected: Tricks link in air. Multiplier increases per trick. Score calculation is correct.
- Priority: P0

**TC-TRICK-003: Clean Landing**
- Preconditions: Player airborne after trick
- Steps:
  1. Execute trick
  2. Rotate character to land wheels-down (correct angle)
  3. Land on flat ground at acceptable speed (<80 kph)
  4. Verify landing succeeds (combo score locks in)
  5. Verify visual feedback (clean landing VFX)
- Expected: Clean landing is forgiving but has standards. Reasonable angle/speed window. Score is locked in.
- Priority: P0

**TC-TRICK-004: Bail Detection (Bad Landing)**
- Preconditions: Player airborne after trick
- Steps:
  1. Execute trick
  2. Land at steep angle (>45 degrees off vertical) or too fast (>100 kph)
  3. Verify bail triggers (character falls, bail animation plays)
  4. Verify combo score is lost (resets to 0)
  5. Verify 2-second recovery time before player can move again
- Expected: Bail is clearly triggered. Score loss is obvious. Recovery time feels fair but punishing.
- Priority: P0

**TC-TRICK-005: Grinding Mechanics**
- Preconditions: Player approaching rail
- Steps:
  1. Jump onto rail trigger
  2. Verify grind state activates (character locks to rail spline)
  3. Verify balance meter appears
  4. Use left stick to balance (maintain center of balance meter)
  5. Grind for 5+ seconds
  6. Verify grind score accumulates over time
  7. Exit rail cleanly
- Expected: Grind locks to rail smoothly. Balance meter is visible and responsive. Score accumulates while grinding.
- Priority: P1

**TC-TRICK-006: Grind Bail (Lost Balance)**
- Preconditions: Player grinding on rail
- Steps:
  1. Deliberately fail to balance (let balance meter hit edge)
  2. Verify bail triggers (player falls off rail)
  3. Verify combo is lost
  4. Verify recovery time applies
- Expected: Grinding has risk. Losing balance = bail. Combo resets.
- Priority: P1

**TC-TRICK-007: Manual Mode (Combo Extension)**
- Preconditions: Player lands from air trick
- Steps:
  1. Execute trick and land
  2. Immediately enter manual mode (wheelie input)
  3. Verify manual animation plays
  4. Verify balance meter appears
  5. Maintain manual for 3+ seconds while moving
  6. Verify combo multiplier persists (doesn't reset on landing)
  7. Execute another trick off next ramp
  8. Verify multiplier continues from previous combo
- Expected: Manual allows combo extension across flat ground. Balance is required. Multiplier chains through manual.
- Priority: P1

#### Test Cases: Edge Cases

**TC-TRICK-EDGE-001: Max Combo Multiplier**
- Preconditions: Player chaining tricks
- Steps:
  1. Link 10+ tricks in a single combo (via manual/grind chaining)
  2. Verify multiplier caps at reasonable value (e.g., x10 or x20)
  3. Verify score doesn't overflow or break UI
- Expected: Multiplier has a cap. No score overflow. UI displays large numbers correctly.
- Priority: P2

**TC-TRICK-EDGE-002: Trick Spamming (Same Trick Repeated)**
- Preconditions: Player in air
- Steps:
  1. Execute same trick 3 times in one combo
  2. Verify score penalty for repetition (diminishing returns)
- Expected: Repeating tricks is discouraged (lower score per repeat). Variety is rewarded.
- Priority: P2

**TC-TRICK-EDGE-003: Landing on Rail (Direct Air-to-Grind)**
- Preconditions: Player airborne above rail
- Steps:
  1. Execute air trick
  2. Land directly onto rail (skip ground landing)
  3. Verify grind state activates immediately
  4. Verify combo continues (no reset)
- Expected: Air-to-grind transition is smooth. Combo persists. Feels stylish.
- Priority: P2

**TC-TRICK-EDGE-004: Fall Through World (Failed Geometry)**
- Preconditions: Player in trick area
- Steps:
  1. Attempt to find geometry gaps or collision holes
  2. If player falls through world, verify respawn triggers
  3. Verify combo is lost (fair penalty)
  4. Verify respawn is fast (<3 seconds)
- Expected: If world collision fails, respawn is automatic. Player is never stuck in void.
- Priority: P1

### 2.5 Style Meter (Universal System)

**What we're testing**: Cross-discipline meter accumulation, decay, tier thresholds, UNDERGROUND MODE activation, visual/audio feedback.

#### Test Cases: Style Meter Accumulation

**TC-STYLE-001: Meter Gain (Racing)**
- Preconditions: Player in racing event
- Steps:
  1. Perform drift for 2 seconds (should award ~30 points at +15/sec)
  2. Verify Style Meter increases
  3. Trigger near-miss (+40 points)
  4. Verify cumulative total is correct (~70 points)
- Expected: Meter gains match design spec. Visual bar updates in real-time.
- Priority: P0

**TC-STYLE-002: Meter Gain (Fighting)**
- Preconditions: Player in fight
- Steps:
  1. Execute 3-hit combo (20 points per hit after 2nd = 40 points total)
  2. Verify Style Meter increases by ~40 points
  3. Execute taunt successfully (+60 points)
  4. Verify cumulative total (~100 points)
- Expected: Meter gains are accurate across fighting actions. Taunt risk/reward is clear.
- Priority: P0

**TC-STYLE-003: Meter Gain (Basketball)**
- Preconditions: Player in basketball event
- Steps:
  1. Execute crossover (+35 points)
  2. Verify meter increases
  3. Score alley-oop (+45 points)
  4. Verify cumulative total (~80 points)
- Expected: Basketball actions feed Style Meter. Values match spec.
- Priority: P0

**TC-STYLE-004: Meter Gain (Tricks)**
- Preconditions: Player in trick event
- Steps:
  1. Link 3 tricks in combo (25 points per link after first = 50 points)
  2. Verify meter increases correctly
- Expected: Trick linking feeds Style Meter appropriately.
- Priority: P0

**TC-STYLE-005: Cross-Discipline Meter Persistence**
- Preconditions: Player completes racing event with 600 Style Meter
- Steps:
  1. Exit race
  2. Enter fight event within 10 minutes (game time)
  3. Verify Style Meter carries over (starts fight at 600 points)
  4. Verify +100 discipline switch bonus applied (700 total)
- Expected: Style Meter persists between events for 10 minutes. Discipline switch bonus is awarded.
- Priority: P0

**TC-STYLE-006: Meter Decay**
- Preconditions: Player has 500 Style Meter, no stylish actions for 4+ seconds
- Steps:
  1. Stop performing stylish actions (idle or safe play)
  2. After 4 seconds, observe meter decay (-8 points/sec)
  3. Verify meter decreases over time
  4. Verify decay stops if player performs stylish action
- Expected: Decay activates after 4-second grace period. Decay rate matches spec. Decay pauses during stylish play.
- Priority: P1

#### Test Cases: Style Meter Tiers

**TC-STYLE-007: Tier Transitions (COLD → WARM → HOT → ON FIRE)**
- Preconditions: Player starting event with 0 Style Meter
- Steps:
  1. Accumulate 250 points (WARM tier)
  2. Verify tier-up VFX and audio cue
  3. Verify +10% REP gain buff is active (check results screen after event)
  4. Accumulate 500 points (HOT tier)
  5. Verify tier-up effects (+25% REP, visual glow intensifies, crowd louder)
  6. Accumulate 750 points (ON FIRE tier)
  7. Verify tier-up effects (+50% REP, time window forgiveness, max VFX)
- Expected: Each tier transition is clear. Buffs are applied correctly. Visual/audio feedback is distinct per tier.
- Priority: P0

**TC-STYLE-008: UNDERGROUND MODE Activation**
- Preconditions: Player has 1000 Style Meter (max)
- Steps:
  1. Verify UI prompt to activate UNDERGROUND MODE appears
  2. Press activation button
  3. Verify 12-second timer starts
  4. Verify slow-mo effect (15% time dilation)
  5. Verify enhanced move properties (wider drift, longer stun, etc.)
  6. Verify +100% REP gain during window
  7. After 12 seconds, verify mode ends and meter drains to 0
- Expected: UNDERGROUND MODE is flashy and powerful. 12-second duration is noticeable. Meter fully drains after use.
- Priority: P0

**TC-STYLE-009: UNDERGROUND MODE During Boss Event**
- Preconditions: Player in boss event with 1000 Style Meter
- Steps:
  1. Activate UNDERGROUND MODE during boss fight/race/game
  2. Verify REP multiplier bonus is tracked
  3. Complete event during or after UNDERGROUND MODE
  4. Verify final REP calculation includes +100% bonus for 12 seconds of event
- Expected: UNDERGROUND MODE timing affects REP gains. Strategic activation is rewarded.
- Priority: P1

#### Test Cases: Edge Cases

**TC-STYLE-EDGE-001: Meter Gain During UNDERGROUND MODE**
- Preconditions: UNDERGROUND MODE active
- Steps:
  1. Perform stylish actions during UNDERGROUND MODE
  2. Verify meter does NOT increase (mode is already maxed)
  3. After mode ends and meter drains, verify new stylish actions start filling meter again from 0
- Expected: Meter is locked during UNDERGROUND MODE. Can refill after mode ends.
- Priority: P2

**TC-STYLE-EDGE-002: Decay During Event vs. Free Roam**
- Preconditions: Player has 500 Style Meter
- Steps:
  1. Exit event and enter free roam
  2. Idle for 10+ seconds
  3. Verify meter does NOT decay during free roam
  4. Enter new event
  5. Idle for 4+ seconds during event
  6. Verify decay activates during event
- Expected: Decay only happens during active events, not free roam. Players aren't punished for exploration.
- Priority: P1

**TC-STYLE-EDGE-003: Negative Meter (Underflow Check)**
- Preconditions: Player has 10 Style Meter, decay is active
- Steps:
  1. Let decay reduce meter to 0
  2. Verify meter stops at 0 (doesn't go negative)
  3. Perform stylish action
  4. Verify meter increases from 0 normally
- Expected: Meter floor is 0. No negative values. No underflow bugs.
- Priority: P2

### 2.6 REP and Progression System

**What we're testing**: REP earning, tier progression, diminishing returns, REP gates, district unlocks, rival interactions.

#### Test Cases: REP Earning

**TC-REP-001: REP Award (Event Win with Style)**
- Preconditions: Player completes event with A-rank style
- Steps:
  1. Win racing event (base 100 REP)
  2. Achieve A-rank style (assume +50% multiplier from HOT/ON FIRE tier)
  3. Verify REP awarded = 150 (100 * 1.5)
  4. Verify REP total updates in player save data
- Expected: REP calculation is correct. Multipliers apply. Save data updates immediately.
- Priority: P0

**TC-REP-002: REP Award (Event Loss with Style)**
- Preconditions: Player loses event but achieves B-rank style
- Steps:
  1. Lose racing event (0 base REP for loss)
  2. But B-rank style awards 30 REP (consolation)
  3. Verify 30 REP is awarded despite loss
- Expected: Stylish losses still award partial REP. Encourages risk-taking even when losing.
- Priority: P1

**TC-REP-003: Diminishing Returns (Same Event Type)**
- Preconditions: Player completes 4 racing events in same district in one session
- Steps:
  1. Complete 1st race: Verify 100% REP (e.g., 150 REP)
  2. Complete 2nd race (same type): Verify 80% REP (120 REP)
  3. Complete 3rd race: Verify 50% REP (75 REP)
  4. Complete 4th race: Verify 25% REP (37.5 REP)
- Expected: Diminishing returns kick in as designed. Player is incentivized to switch disciplines.
- Priority: P0

**TC-REP-004: Diminishing Returns Reset (New Session)**
- Preconditions: Player completed 4 races with diminishing returns active
- Steps:
  1. Exit game and reload save
  2. Complete another race in same district
  3. Verify REP is back to 100% (diminishing returns reset per session)
- Expected: Diminishing returns reset between play sessions. Fresh start each session.
- Priority: P1

**TC-REP-005: Cross-Discipline Variety Bonus**
- Preconditions: Player completes race, then fight, then basketball in sequence
- Steps:
  1. Complete race (REP awarded normally)
  2. Complete fight (different discipline, verify no diminishing returns)
  3. Complete basketball (third discipline in row, verify Triple Threat bonus: +200 REP flat)
- Expected: Discipline variety is rewarded. Triple Threat bonus is significant incentive.
- Priority: P1

#### Test Cases: REP Tiers and Unlocks

**TC-REP-006: REP Tier Progression (NOBODY → LOCAL)**
- Preconditions: Player has 0 REP (NOBODY tier)
- Steps:
  1. Earn 1000 REP (threshold for LOCAL tier)
  2. Verify tier-up notification appears
  3. Verify new district events become accessible
  4. Verify NPC dialogue changes (NPCs now recognize player)
- Expected: Tier transitions are celebrated. Unlocks are clear. World reacts to new tier.
- Priority: P0

**TC-REP-007: District Boss REP Gate**
- Preconditions: Player has 4500 REP (below boss threshold of 5000)
- Steps:
  1. Approach district boss event marker
  2. Verify event is locked (UI message: "Need 5000 REP to challenge boss")
  3. Earn 500 more REP (total 5000)
  4. Return to boss marker
  5. Verify event is now unlocked
- Expected: REP gates function correctly. Player is informed of requirements. Unlock is immediate upon hitting threshold.
- Priority: P0

**TC-REP-008: REP Loss (Declining Rival Challenge)**
- Preconditions: Player has 5000 REP, rival issues direct challenge
- Steps:
  1. Decline challenge (walk away or select "No" in dialogue)
  2. Verify -200 REP penalty is applied
  3. Verify new REP total (4800)
  4. Verify rival's Respect toward player decreases
- Expected: Declining has consequence. REP loss is immediate. Rival relationship is affected.
- Priority: P1

#### Test Cases: Edge Cases

**TC-REP-EDGE-001: REP Overflow (Max REP)**
- Preconditions: Player has 99,999 REP (near hypothetical cap)
- Steps:
  1. Complete event that would award +1000 REP
  2. Verify REP updates correctly (doesn't overflow or wrap to negative)
  3. Verify UI displays large REP values correctly
- Expected: REP has a safe cap (or no cap with safe int handling). No overflow bugs.
- Priority: P3

**TC-REP-EDGE-002: REP Underflow (Losing More Than Player Has)**
- Preconditions: Player has 100 REP
- Steps:
  1. Decline rival challenge (-200 REP penalty)
  2. Verify REP goes to 0, not -100 (REP floor is 0)
- Expected: REP cannot go negative. Floor is 0.
- Priority: P2

**TC-REP-EDGE-003: REP Award Timing (Quit Before Results Screen)**
- Preconditions: Player completes event
- Steps:
  1. Win event but quit game before results screen fully loads
  2. Reload game
  3. Verify REP was (or was not) saved depending on when auto-save triggers
  4. Document behavior for expected outcome
- Expected: REP is saved at a consistent point (either on event completion or results screen display). Player understands when progress is saved.
- Priority: P1

### 2.7 Rival AI System

**What we're testing**: Personality attributes (Pride, Respect, Grudge, Confidence), behavior evolution, obsession mechanic, recruitment, breaking point, counter-building.

#### Test Cases: Rival Behavior

**TC-RIVAL-001: Initial Rival Encounter**
- Preconditions: Player enters district, rival is present
- Steps:
  1. Trigger first encounter with named rival
  2. Verify rival intro (name, personality hint in dialogue)
  3. Complete event against rival
  4. Verify rival's stats are initialized (Respect: 0, Grudge: 0, Confidence: baseline)
- Expected: First encounter sets up rival relationship. Stats are tracked from first interaction.
- Priority: P0

**TC-RIVAL-002: Respect Gain (Stylish Win)**
- Preconditions: Player challenges rival
- Steps:
  1. Win event with A or S rank style
  2. Verify rival's Respect increases by +10
  3. Check rival's post-event dialogue (should acknowledge player's skill)
- Expected: Stylish wins earn respect. Rival attitude shifts positively.
- Priority: P1

**TC-RIVAL-003: Grudge Accumulation (Humiliating Win)**
- Preconditions: Player challenges rival
- Steps:
  1. Win with S rank and/or use taunts
  2. Verify rival's Grudge increases by +25 (humiliation penalty)
  3. Check rival's post-event dialogue (should show anger/frustration)
- Expected: Humiliation builds grudge. Rival becomes hostile.
- Priority: P1

**TC-RIVAL-004: Confidence Drop (Player Win)**
- Preconditions: Rival has 60 Confidence
- Steps:
  1. Defeat rival
  2. Verify Confidence decreases by -10
  3. If Confidence drops to <30, verify rival becomes more cautious (less likely to challenge)
- Expected: Winning shakes rival's confidence. Low confidence changes behavior.
- Priority: P1

**TC-RIVAL-005: Obsessed State (70+ Grudge)**
- Preconditions: Rival has 70+ Grudge
- Steps:
  1. Verify rival enters Obsessed state (UI notification or rival phone call)
  2. Enter any event in rival's home district
  3. Verify 40% chance for rival to interrupt event (crash race, invade fight)
  4. Verify rival's counter-build is active (if player uses drift car, rival uses grip car)
- Expected: Obsessed rivals are aggressive. Interruptions feel like escalation. Counter-build makes rival harder.
- Priority: P1

**TC-RIVAL-006: Recruitment (60+ Respect)**
- Preconditions: Rival has 60+ Respect, not yet recruited
- Steps:
  1. Verify recruitment dialogue triggers (rival offers to join crew)
  2. Accept recruitment
  3. Verify rival is added to crew
  4. Verify rival's passive bonus is applied (e.g., +5% Style Meter gain in their specialty)
  5. Verify rival no longer appears as opponent
- Expected: High respect leads to recruitment. Crew bonuses are applied. Rival becomes ally.
- Priority: P1

**TC-RIVAL-007: Breaking Point (0 Confidence + 50+ Grudge)**
- Preconditions: Rival has 0 Confidence and 60 Grudge
- Steps:
  1. Defeat rival one more time
  2. Verify rival "breaks" (narrative event triggers)
  3. Verify rival leaves district permanently
  4. Later in game, verify rival may reappear in different context (e.g., working for mainstream antagonists)
- Expected: Breaking a rival has permanent consequences. Narrative reflects broken state.
- Priority: P2

#### Test Cases: Edge Cases

**TC-RIVAL-EDGE-001: Multiple Rivals Obsessed Simultaneously**
- Preconditions: 3+ rivals at 70+ Grudge (all Obsessed)
- Steps:
  1. Enter event
  2. Verify only one rival interrupts per event (not all 3 at once)
  3. Verify subsequent events can be interrupted by different Obsessed rivals
- Expected: Game prevents rival spam. One interrupt per event max. Feels dramatic, not overwhelming.
- Priority: P2

**TC-RIVAL-EDGE-002: Rival Stat Overflow (Max Grudge/Respect)**
- Preconditions: Rival has 100 Grudge or +100 Respect
- Steps:
  1. Perform action that would increase stat further
  2. Verify stat caps at max value (100 or +100)
  3. Verify no overflow or weird behavior
- Expected: Stats have hard caps. No overflow bugs.
- Priority: P3

**TC-RIVAL-EDGE-003: Recruiting Then Losing to Former Rival**
- Preconditions: Rival is recruited to crew
- Steps:
  1. Verify recruited rival does NOT appear as opponent in events
  2. Attempt to trigger scenario where crew rival would oppose player (should not happen)
- Expected: Recruited rivals are permanently allies. No paradox situations.
- Priority: P2

**TC-RIVAL-EDGE-004: Rival Counter-Build Effectiveness**
- Preconditions: Player uses high-drift car (low grip), rival is Obsessed
- Steps:
  1. Race against Obsessed rival
  2. Verify rival uses high-grip car (counter to player's drift setup)
  3. Verify rival is noticeably harder than non-countering rivals
  4. Verify player can still win with skill (counter isn't unbeatable)
- Expected: Counter-building makes rivals harder but fair. Adds strategic layer.
- Priority: P2

### 2.8 Customization and Build System

**What we're testing**: Car parts, fighting moves, basketball skills, trick loadouts, stat tradeoffs, synergy detection, garage/locker UI.

#### Test Cases: Customization Mechanics

**TC-CUSTOM-001: Car Part Purchase**
- Preconditions: Player has 500 CASH, in garage
- Steps:
  1. View available car parts
  2. Select engine upgrade (cost: 500 CASH)
  3. Purchase part
  4. Verify CASH is deducted
  5. Verify part is added to inventory
  6. Equip part
  7. Verify car stats update (e.g., Power increases from 75 to 85)
- Expected: Purchase flow works. CASH is deducted. Stats update correctly.
- Priority: P0

**TC-CUSTOM-002: Stat Tradeoffs (Weight vs. Speed)**
- Preconditions: Player equipping lightweight vs. heavyweight car part
- Steps:
  1. Equip lightweight part (low mass, high acceleration)
  2. Test race: Verify fast acceleration, less drift stability
  3. Equip heavyweight part (high mass, slow acceleration, better drift)
  4. Test race: Verify slower start, easier to maintain drift
- Expected: Stat tradeoffs are noticeable in gameplay. No strictly superior build.
- Priority: P1

**TC-CUSTOM-003: Fighting Move Purchase and Equip**
- Preconditions: Player in locker room with CASH
- Steps:
  1. Purchase new combo move
  2. Equip move (replacing old move in loadout)
  3. Enter fight
  4. Verify new move is executable
  5. Verify old move is no longer available (loadout has limited slots)
- Expected: Move equipping works. Loadout limits force choices.
- Priority: P0

**TC-CUSTOM-004: Synergy Detection (Drift King + Ankle Breaker)**
- Preconditions: Player has drift-tuned car (grip <50) AND flashy crossover basketball skill equipped
- Steps:
  1. Complete race, then basketball game in sequence
  2. Verify Style Meter carries 25% more between disciplines (synergy bonus)
  3. Verify no UI explicitly tells player about synergy (hidden mechanic)
  4. Verify synergy bonus is consistently applied when conditions are met
- Expected: Synergy bonuses are real and measurable. Players discover through experimentation.
- Priority: P1

**TC-CUSTOM-005: Fashion Items (Cosmetic with Mechanical Edge)**
- Preconditions: Player purchases flashy clothing item
- Steps:
  1. Equip fashion item
  2. Enter event with crowd
  3. Verify +5-15% Style Meter gain from crowd reactions (fashion bonus)
  4. Compare to event without fashion item equipped
- Expected: Fashion has small mechanical benefit. Not mandatory but helpful.
- Priority: P2

#### Test Cases: Edge Cases

**TC-CUSTOM-EDGE-001: Insufficient CASH (Purchase Attempt)**
- Preconditions: Player has 100 CASH, part costs 500
- Steps:
  1. Attempt to purchase part
  2. Verify purchase is blocked (UI error message: "Not enough CASH")
  3. Verify CASH is not deducted
  4. Verify part is not added to inventory
- Expected: Game prevents purchases player can't afford. No negative CASH exploit.
- Priority: P0

**TC-CUSTOM-EDGE-002: Selling Parts (40% Value Return)**
- Preconditions: Player owns part worth 1000 CASH
- Steps:
  1. Sell part
  2. Verify 400 CASH returned (40% of original cost)
  3. Verify part is removed from inventory
- Expected: Selling works. Value loss is clear. No duplication exploit.
- Priority: P1

**TC-CUSTOM-EDGE-003: Equip Same Part Multiple Times**
- Preconditions: Player owns engine part, already equipped
- Steps:
  1. Attempt to equip same part again
  2. Verify game prevents duplicate equipping (or unequips/re-equips harmlessly)
- Expected: No duplicate equip bugs. Stat stacking exploit is impossible.
- Priority: P2

**TC-CUSTOM-EDGE-004: Synergy Stacking (Multiple Synergies Active)**
- Preconditions: Player has 3 different synergies active simultaneously
- Steps:
  1. Verify all 3 bonuses apply (e.g., +25% cross-discipline, +15% universal Style gain, +10% REP)
  2. Verify bonuses stack additively (not multiplicatively, unless designed that way)
  3. Verify no overflow or balance-breaking scenarios
- Expected: Synergy stacking is powerful but balanced. Deep builds are rewarded.
- Priority: P2

### 2.9 Save/Load System

**What we're testing**: Save triggers, save file integrity, Steam Cloud sync, corrupted save handling, progress persistence.

#### Test Cases: Save/Load Functionality

**TC-SAVE-001: Auto-Save After Event**
- Preconditions: Player completes event
- Steps:
  1. Win event and view results screen
  2. Verify auto-save notification (or subtle indicator)
  3. Force-quit game immediately after results screen
  4. Reload game
  5. Verify REP, CASH, and event completion are saved
- Expected: Auto-save triggers after event completion. Progress is not lost.
- Priority: P0

**TC-SAVE-002: Manual Save**
- Preconditions: Player in menus
- Steps:
  1. Select "Save Game" option
  2. Verify save completes (confirmation message)
  3. Quit game
  4. Reload save
  5. Verify all progress is intact
- Expected: Manual save works. Players can save on demand.
- Priority: P0

**TC-SAVE-003: Save File JSON Integrity**
- Preconditions: Player has active save file
- Steps:
  1. Locate save file (persistent data path)
  2. Open save.json in text editor
  3. Verify JSON is well-formed (no syntax errors)
  4. Verify key data is present (totalREP, currentCash, rivals array, etc.)
- Expected: Save file is human-readable JSON. Data structure matches spec.
- Priority: P1

**TC-SAVE-004: Steam Cloud Sync (Upload)**
- Preconditions: Player on Steam with Cloud enabled
- Steps:
  1. Complete event (trigger auto-save)
  2. Verify save file is uploaded to Steam Cloud (check Steam client)
  3. Note cloud timestamp
- Expected: Save syncs to Steam Cloud automatically. No manual upload required.
- Priority: P1

**TC-SAVE-005: Steam Cloud Sync (Download)**
- Preconditions: Save exists on Steam Cloud from different PC
- Steps:
  1. Launch game on new PC
  2. Verify game detects Steam Cloud save
  3. Verify game downloads and loads cloud save
  4. Verify progress matches last sync point
- Expected: Cloud save download is automatic. Progress is portable across PCs.
- Priority: P1

**TC-SAVE-006: Corrupted Save Handling**
- Preconditions: Manually corrupt save.json (delete half the file or insert invalid JSON)
- Steps:
  1. Launch game
  2. Verify game detects corrupt save
  3. Verify game displays error message ("Save file corrupted. Starting new game.")
  4. Verify game creates fresh save (doesn't crash)
- Expected: Corrupted saves don't crash game. Player is informed. New game starts cleanly.
- Priority: P0

#### Test Cases: Edge Cases

**TC-SAVE-EDGE-001: Save During Event (Mid-Race Quit)**
- Preconditions: Player in middle of race
- Steps:
  1. Quit game mid-race (before completion)
  2. Reload game
  3. Verify player is returned to free roam (not mid-race)
  4. Verify REP/CASH from incomplete race is not saved
- Expected: Incomplete events are not saved. No progress for partial completion. Fair.
- Priority: P1

**TC-SAVE-EDGE-002: Multiple Save Slots (If Implemented)**
- Preconditions: Game supports multiple save slots
- Steps:
  1. Create Save Slot 1, earn 1000 REP
  2. Create Save Slot 2, earn 5000 REP
  3. Load Save Slot 1
  4. Verify 1000 REP (not 5000)
  5. Load Save Slot 2
  6. Verify 5000 REP (not 1000)
- Expected: Save slots are independent. No data bleed between slots.
- Priority: P2 (if feature exists)

**TC-SAVE-EDGE-003: Save File Versioning (Schema Update)**
- Preconditions: Save file from older game version exists
- Steps:
  1. Update game to new version with schema changes
  2. Load old save file
  3. Verify migration logic converts old save to new schema
  4. Verify game loads correctly with migrated data
- Expected: Save versioning handles schema changes gracefully. Players don't lose progress on updates.
- Priority: P1 (critical for post-launch patches)

### 2.10 Performance and Stability

**What we're testing**: Frame rate on target hardware, load times, memory usage, draw call optimization, crash stability.

#### Test Cases: Performance Targets

**TC-PERF-001: Framerate on Steam Deck (800p, Racing)**
- Preconditions: Game running on Steam Deck, racing event
- Steps:
  1. Start race with 8 opponents
  2. Use framerate overlay (Steam's built-in FPS counter)
  3. Observe FPS during race (especially during drifts with heavy VFX)
  4. Verify FPS stays at or above 60fps for 90%+ of race duration
- Expected: 60fps minimum on Steam Deck during racing. Dips below 60 are rare and brief.
- Priority: P0

**TC-PERF-002: Framerate on Steam Deck (Fighting)**
- Preconditions: Steam Deck, fighting event
- Steps:
  1. Fight with heavy VFX (lots of hits, particle effects)
  2. Monitor FPS
  3. Verify consistent 60fps (fighting should be cheapest discipline)
- Expected: 60fps locked during fights. No performance issues.
- Priority: P0

**TC-PERF-003: Framerate on Steam Deck (Basketball)**
- Preconditions: Steam Deck, basketball event
- Steps:
  1. Play 2v2 game with crowd NPCs active
  2. Monitor FPS
  3. Verify 60fps throughout
- Expected: 60fps stable. Crowd NPCs don't tank performance.
- Priority: P0

**TC-PERF-004: Framerate on Steam Deck (Tricks)**
- Preconditions: Steam Deck, trick event
- Steps:
  1. Perform long combo with multiple VFX (sparks, trails)
  2. Monitor FPS
  3. Verify 60fps
- Expected: 60fps during tricks. VFX are optimized.
- Priority: P0

**TC-PERF-005: Load Time (District Transition)**
- Preconditions: Player transitioning from Southside to Docks
- Steps:
  1. Trigger district transition
  2. Measure load time (from transition start to gameplay resume)
  3. Verify load time <10 seconds
- Expected: District loads in under 10 seconds. Transition feels snappy.
- Priority: P1

**TC-PERF-006: Memory Usage (4GB Budget)**
- Preconditions: Game running on Steam Deck
- Steps:
  1. Load district and play for 30 minutes
  2. Monitor memory usage (Steam overlay or dev tools)
  3. Verify memory stays under 4GB
  4. Transition to new district
  5. Verify old district is unloaded (memory freed)
- Expected: Memory budget is respected. No memory leaks. Old districts unload cleanly.
- Priority: P0

**TC-PERF-007: Draw Call Count (Target <500)**
- Preconditions: Dev build with profiler
- Steps:
  1. Enable Unity Profiler
  2. Run racing event
  3. Check draw call count per frame
  4. Verify draw calls <500
- Expected: Batching is effective. Draw calls are optimized. GPU isn't bottlenecked.
- Priority: P1

#### Test Cases: Stability

**TC-STAB-001: Crash Test (Extended Play Session)**
- Preconditions: Fresh game launch
- Steps:
  1. Play continuously for 2 hours
  2. Perform variety of actions (all disciplines, multiple events, menu transitions)
  3. Verify no crashes, no soft-locks, no freezes
- Expected: Game is stable for extended sessions. No memory leaks cause crashes.
- Priority: P0

**TC-STAB-002: Alt-Tab Stability (PC)**
- Preconditions: Game running on PC
- Steps:
  1. During active event, alt-tab to desktop
  2. Leave game minimized for 30 seconds
  3. Alt-tab back to game
  4. Verify game resumes correctly (no freeze, no crash)
- Expected: Alt-tabbing is safe. Game pauses gracefully when minimized.
- Priority: P1

**TC-STAB-003: Controller Disconnect (Mid-Event)**
- Preconditions: Player in event using controller
- Steps:
  1. Mid-event, disconnect controller
  2. Verify game pauses or displays warning
  3. Reconnect controller
  4. Verify game resumes with controller active
- Expected: Controller disconnect doesn't crash game. Graceful handling.
- Priority: P1

**TC-STAB-004: Rapid Menu Transitions**
- Preconditions: Player in menus
- Steps:
  1. Rapidly open and close menus (garage, map, settings) 20 times in 10 seconds
  2. Verify no crashes, no UI breaking
- Expected: Menu spam doesn't break anything. UI is robust.
- Priority: P2

**TC-STAB-005: Save Spam (Rapid Save Requests)**
- Preconditions: Player in menu with manual save option
- Steps:
  1. Trigger manual save 10 times rapidly
  2. Verify game handles multiple save requests gracefully (queues or blocks redundant saves)
  3. Verify save file is intact (not corrupted by rapid writes)
- Expected: Rapid save requests don't corrupt data. Game handles edge case.
- Priority: P2

---

## 3. Cross-Discipline Integration Testing

**What we're testing**: Discipline switching, Style Meter persistence, camera transitions, control remapping, progression continuity.

### Test Cases

**TC-CROSS-001: Race to Fight Transition**
- Preconditions: Player completes race with 600 Style Meter
- Steps:
  1. Exit race
  2. Immediately enter fight event (within 10 game-minutes)
  3. Verify Style Meter carries over (600 + 100 discipline switch bonus = 700)
  4. Verify camera transitions smoothly (2-second cinematic blend from race cam to fight cam)
  5. Verify controls remap appropriately (throttle/brake become punch/kick)
- Expected: Transition is seamless. Style persists. Camera/controls adapt to new discipline.
- Priority: P0

**TC-CROSS-002: Triple Discipline Chain (Race → Fight → Ball)**
- Preconditions: Player completes race, then fight, then basketball
- Steps:
  1. Complete all three in sequence within 30 game-minutes
  2. Verify Triple Threat bonus awarded after basketball (+200 REP)
  3. Verify REP calculation includes all bonuses
- Expected: Triple Threat bonus is rewarded. Incentivizes variety.
- Priority: P1

**TC-CROSS-003: Style Meter Expiration (10-Minute Timeout)**
- Preconditions: Player completes race with 500 Style Meter
- Steps:
  1. Free roam for 11 game-minutes (do not enter event)
  2. Enter new event
  3. Verify Style Meter has reset to 0 (10-minute persistence window expired)
- Expected: Style Meter decays after 10 minutes. Time limit is enforced.
- Priority: P1

**TC-CROSS-004: Discipline Proficiency Tracking**
- Preconditions: Player completes 3 racing events
- Steps:
  1. Verify Racing proficiency increases (e.g., from 0 to 1)
  2. Complete 3 more racing events (total 6)
  3. Verify proficiency increases again (1 to 2)
  4. Verify proficiency is independent per discipline (Fighting stays 0 if no fights completed)
- Expected: Proficiency tracks per discipline. Levels up consistently.
- Priority: P1

---

## 4. Narrative and World Integration Testing

**What we're testing**: District unlocks, boss events, crew recruitment, mainstream vs. underground choice, environmental storytelling.

### Test Cases

**TC-WORLD-001: District Unlock (REP Gate)**
- Preconditions: Player has 4900 REP (below 5000 threshold for District 2)
- Steps:
  1. Attempt to enter District 2
  2. Verify entry is blocked (UI message: "Need 5000 REP")
  3. Earn 100 more REP
  4. Attempt to enter District 2
  5. Verify entry is now allowed
- Expected: District unlocks are gated by REP. Messaging is clear.
- Priority: P0

**TC-WORLD-002: Boss Event (Multi-Phase Challenge)**
- Preconditions: Player challenges Southside boss (King)
- Steps:
  1. Complete Phase 1 (race against King)
  2. Win race
  3. Verify Phase 2 triggers (fight against King)
  4. Win fight
  5. Verify boss is defeated and district is claimed
  6. Verify narrative beat plays (King acknowledges defeat)
- Expected: Multi-phase boss events work. Both phases must be won. Story reflects outcome.
- Priority: P0

**TC-WORLD-003: Crew Recruitment (Rival Joins)**
- Preconditions: Rival has 65 Respect
- Steps:
  1. Verify recruitment dialogue triggers
  2. Accept recruitment
  3. Verify rival is added to crew roster
  4. Verify rival's passive bonus applies (check stat screen)
  5. Verify rival no longer appears as opponent
- Expected: Recruitment works. Crew bonuses are active. Rival becomes ally.
- Priority: P1

**TC-WORLD-004: Mainstream Choice (Marcus's Offer)**
- Preconditions: Player reaches mid-game, Marcus offers mainstream deal
- Steps:
  1. Accept Marcus's offer
  2. Verify Mainstream Meter increases (hidden value, check via debug if available)
  3. Verify world changes (music becomes more polished, crowds have more tourists)
  4. Verify NPC dialogue reflects choice (some characters are disappointed)
- Expected: Choice has consequences. World reacts. Mainstream path is distinct from Underground path.
- Priority: P1

**TC-WORLD-005: Environmental Storytelling (Graffiti Changes)**
- Preconditions: Player defeats district boss
- Steps:
  1. Observe graffiti in district before boss defeat
  2. Defeat boss
  3. Return to same area
  4. Verify graffiti has changed (boss's tag crossed out, player's tag appears)
- Expected: World reflects player actions. Environmental details update.
- Priority: P2

---

## 5. Input and Controls Testing

**What we're testing**: Controller support, keyboard/mouse, input buffering, rebinding, accessibility.

### Test Cases

**TC-INPUT-001: Controller Detection (Steam Input)**
- Preconditions: Game launched with Xbox/PlayStation/Steam controller connected
- Steps:
  1. Verify controller is detected automatically
  2. Verify button prompts match controller type (Xbox A/B/X/Y or PlayStation X/O/Square/Triangle)
  3. Test all inputs (throttle, brake, steer, attack, jump, etc.)
- Expected: Controller works out of box. Prompts are correct. All buttons functional.
- Priority: P0

**TC-INPUT-002: Keyboard/Mouse Support**
- Preconditions: Game launched without controller
- Steps:
  1. Verify keyboard/mouse controls work
  2. Test racing (WASD + mouse steering or arrow keys)
  3. Test fighting (keyboard combos)
  4. Verify button prompts switch to keyboard labels
- Expected: Keyboard/mouse is functional. Not primary input but viable.
- Priority: P1

**TC-INPUT-003: Input Buffering (Combo Execution)**
- Preconditions: Player in fight
- Steps:
  1. Input Light → Light → Heavy rapidly
  2. Verify combo executes even if inputs are slightly early (within 10-frame buffer)
  3. Verify late inputs (outside buffer) do not combo
- Expected: Input buffer makes combos feel responsive. Tight but fair timing.
- Priority: P1

**TC-INPUT-004: Control Remapping**
- Preconditions: Player in settings menu
- Steps:
  1. Remap throttle from RT to A button
  2. Enter racing event
  3. Verify throttle now activates on A button (not RT)
  4. Verify remapping persists after game restart
- Expected: Remapping works. Changes are saved.
- Priority: P2

**TC-INPUT-005: Accessibility (Hold vs. Toggle)**
- Preconditions: Player in settings
- Steps:
  1. Enable "Toggle" mode for drift (instead of hold)
  2. Enter race
  3. Tap drift button once to start drift
  4. Tap again to end drift (no holding required)
- Expected: Toggle mode works. Reduces hand strain for accessibility.
- Priority: P2

---

## 6. Audio Testing

**What we're testing**: Music integration, SFX triggering, beat-sync, audio mixing, dynamic music.

### Test Cases

**TC-AUDIO-001: Music Playback (Event Start)**
- Preconditions: Player enters racing event
- Steps:
  1. Verify music track starts playing
  2. Verify music matches district/event type (Southside has specific music)
  3. Verify music loops seamlessly (no gaps or pops)
- Expected: Music enhances atmosphere. Looping is clean.
- Priority: P1

**TC-AUDIO-002: SFX Triggering (Drift)**
- Preconditions: Player drifting in race
- Steps:
  1. Initiate drift
  2. Verify tire screech SFX plays
  3. Verify SFX volume scales with drift intensity
  4. Exit drift
  5. Verify SFX stops cleanly
- Expected: SFX are synchronized to actions. Volume is appropriate.
- Priority: P1

**TC-AUDIO-003: Crowd Reaction Audio (Style Tier Change)**
- Preconditions: Player in basketball event, Style Meter at 250 (WARM tier)
- Steps:
  1. Perform action that pushes Style to 500 (HOT tier)
  2. Verify crowd audio intensifies (louder cheering, more energy)
  3. Perform action that pushes Style to 750 (ON FIRE tier)
  4. Verify crowd is deafening
- Expected: Crowd audio reflects Style Meter tier. Escalation is noticeable.
- Priority: P2

**TC-AUDIO-004: Audio Mixing (Multiple Sources)**
- Preconditions: Player in race with music, engine sounds, drift SFX, near-miss SFX all active
- Steps:
  1. Trigger multiple audio sources simultaneously
  2. Verify all sources are audible and balanced (no source drowns out others)
  3. Verify no audio crackling or distortion
- Expected: Audio mixing is clean. No source dominates inappropriately.
- Priority: P1

**TC-AUDIO-005: Beat-Sync (Style Meter Fills on Beat)**
- Preconditions: Player in event with beat-synced music
- Steps:
  1. Perform stylish action on beat (e.g., drift during bass drop)
  2. Verify Style Meter gain has bonus if action syncs to beat
  3. Verify off-beat actions still award points (just no bonus)
- Expected: Beat-sync is subtle reward. Not required but nice touch.
- Priority: P3 (stretch goal)

---

## 7. UI/UX Testing

**What we're testing**: HUD readability, menu navigation, results screens, garage UI, accessibility.

### Test Cases

**TC-UI-001: HUD Visibility (All Disciplines)**
- Preconditions: Player in each discipline event
- Steps:
  1. Verify HUD elements are visible and readable:
     - Style Meter (vertical bar, left side)
     - Speed/health/score (appropriate per discipline)
     - Position/time/combo counter
  2. Verify HUD does not obstruct critical gameplay view
  3. Verify HUD scales correctly at different resolutions (800p, 1080p, 1440p)
- Expected: HUD is clear. Not intrusive. Scales correctly.
- Priority: P0

**TC-UI-002: Results Screen (Post-Event)**
- Preconditions: Player completes event
- Steps:
  1. View results screen
  2. Verify all data is displayed:
     - Placement (1st, 2nd, etc. or Win/Loss)
     - Style Rank (D through S)
     - REP earned (with breakdown if possible)
     - CASH earned
     - Rival reaction (if applicable)
  3. Verify results screen is dismissible (button prompt visible)
- Expected: Results screen is comprehensive and clear. Player understands outcome.
- Priority: P0

**TC-UI-003: Garage UI (Car Customization)**
- Preconditions: Player in garage
- Steps:
  1. Navigate to car parts list
  2. Verify parts are categorized (Engine, Tires, Body, etc.)
  3. Select part
  4. Verify stat preview shows before/after values
  5. Verify 3D model updates when part is equipped (visual change if applicable)
  6. Verify UI is navigable with controller (no keyboard required)
- Expected: Garage UI is intuitive. Stat changes are clear. Controller navigation works.
- Priority: P0

**TC-UI-004: Map UI (District and Event Markers)**
- Preconditions: Player opens map
- Steps:
  1. Verify map displays all districts
  2. Verify event markers are visible (color-coded by discipline if designed)
  3. Verify locked events are indicated (grayed out or locked icon)
  4. Select event marker
  5. Verify event details are displayed (discipline, difficulty, REP requirement)
  6. Verify fast travel option (if implemented)
- Expected: Map is functional and informative. Player can plan next action.
- Priority: P0

**TC-UI-005: Accessibility (Colorblind Mode)**
- Preconditions: Player enables colorblind mode in settings
- Steps:
  1. Verify UI uses colorblind-friendly palette
  2. Verify critical information is not conveyed by color alone (use icons/text)
  3. Test in race (drift VFX, near-miss indicators)
  4. Verify readability for colorblind players
- Expected: Colorblind mode makes game accessible. No critical info lost.
- Priority: P2

---

## 8. Edge Case and Exploits Testing

**What we're testing**: Game-breaking bugs, exploits, soft-locks, sequence breaks, save scumming.

### Test Cases

**TC-EXPLOIT-001: Infinite CASH (Selling Exploit)**
- Preconditions: Player owns item
- Steps:
  1. Sell item for 40% value
  2. Attempt to re-purchase item, sell again, repeat
  3. Verify CASH cannot be infinitely generated (buy price > sell price prevents infinite loop)
- Expected: No infinite money exploit. Economy is closed-loop.
- Priority: P0

**TC-EXPLOIT-002: REP Farming (Repeating Same Event)**
- Preconditions: Player completes same event 5 times in one session
- Steps:
  1. Verify diminishing returns reduce REP to 25% by 4th repeat
  2. Verify player cannot farm REP efficiently by grinding one event
- Expected: Diminishing returns prevent farming. Variety is enforced.
- Priority: P0

**TC-EXPLOIT-003: Style Meter Exploits (Taunt Spam)**
- Preconditions: Player in fight against low-skill AI
- Steps:
  1. Attempt to spam taunts to fill Style Meter
  2. Verify each taunt has 1.2-second vulnerability window
  3. Verify AI punishes taunt spam (hits player during taunt animation)
- Expected: Taunt spam is high-risk. AI counters predictable play.
- Priority: P1

**TC-EXPLOIT-004: Sequence Break (Accessing Locked District)**
- Preconditions: Player below REP threshold for District 2
- Steps:
  1. Attempt to bypass gate via out-of-bounds routes or glitches
  2. If bypass is possible, enter locked district
  3. Verify events are still locked (even if geography is accessible)
  4. Document if sequence break is possible (may be acceptable if events remain locked)
- Expected: Locked content stays locked even if geography is accessible. Progression gates hold.
- Priority: P2

**TC-EXPLOIT-005: Save Scumming (Boss Event Retry)**
- Preconditions: Player about to fight boss
- Steps:
  1. Manual save before boss
  2. Fight boss and lose
  3. Reload save
  4. Verify boss fight resets (no progress saved from loss)
  5. Fight boss and win
  6. Verify win is saved correctly
- Expected: Save scumming is possible (acceptable). Losses are not saved unless player wants them.
- Priority: P3 (save scumming is player choice, not exploit)

**TC-EXPLOIT-006: Crew Duplication (Recruit Same Rival Twice)**
- Preconditions: Rival is recruited
- Steps:
  1. Verify rival is in crew
  2. Attempt to trigger recruitment dialogue again (should not be possible)
  3. Verify rival's passive bonus is only applied once
- Expected: Rival cannot be recruited twice. No bonus stacking exploit.
- Priority: P2

---

## 9. Quality Gate Criteria

**These are the non-negotiable checkpoints. Nothing ships without passing these gates.**

### Gate 1: Discipline Vertical Slices (Month 3)

- [ ] Racing: One district, 3 opponents, drift mechanics, Style Meter functional, 60fps on Steam Deck
- [ ] Racing passes "one more race" test (5/5 playtesters want to play again immediately)
- [ ] Zero P0 bugs in racing
- [ ] Fighting prototype exists and is playable (even if rough)

**Failure state**: If racing isn't fun by month 3, stop and fix it. Do not proceed to other disciplines.

### Gate 2: Multi-Discipline Integration (Month 6)

- [ ] Racing, fighting, basketball all playable
- [ ] Cross-discipline Style Meter persistence works
- [ ] Camera transitions between disciplines are smooth (no hard cuts)
- [ ] One district with events from all three disciplines
- [ ] 60fps on Steam Deck for all three disciplines
- [ ] Zero P0 bugs across all three disciplines
- [ ] Playtesters confirm discipline switching feels like one game, not three games duct-taped together

**Failure state**: If disciplines feel disjointed, iterate on transition systems before adding tricks.

### Gate 3: Core Loop Complete (Month 12)

- [ ] Full progression system functional (REP, CASH, tier unlocks)
- [ ] Rival AI system implemented (personality, grudge, respect, obsession)
- [ ] Four districts with events
- [ ] All four disciplines playable
- [ ] Save/load system works (including Steam Cloud)
- [ ] Zero P0 bugs, <5 P1 bugs
- [ ] Playable from start to first district boss with full loop intact
- [ ] 60fps on Steam Deck consistently

**Failure state**: If core loop is broken, do not proceed to content. Fix the loop.

### Gate 4: Content Complete (Month 16)

- [ ] All 25-30 rivals implemented with unique personalities
- [ ] All 100+ events placed and tested
- [ ] All customization items implemented
- [ ] Narrative beats functional (underground vs. mainstream choice)
- [ ] Audio implementation complete (music, SFX)
- [ ] Zero P0 bugs, <10 P1 bugs, P2 bugs documented

**Failure state**: If content is incomplete, cut scope. Ship with fewer rivals/events rather than delay.

### Gate 5: Beta Ready (Month 17)

- [ ] Game is feature-complete
- [ ] Performance targets met (60fps on Steam Deck across all disciplines)
- [ ] Zero P0 bugs, <5 P1 bugs
- [ ] All quality gates 1-4 passed
- [ ] External beta testers can play start-to-finish without critical bugs
- [ ] Save/load is stable (no corrupted saves in testing)

**Failure state**: If beta testers hit critical bugs in first hour, delay beta and fix.

### Gate 6: Launch Ready (Month 18)

- [ ] Zero P0 bugs
- [ ] Zero P1 bugs
- [ ] <20 P2 bugs (documented, acceptable for launch)
- [ ] Performance targets met on all platforms
- [ ] Steam store page complete
- [ ] Day-one patch plan documented (for bugs found post-launch)
- [ ] Regression testing complete (all test cases in this document passed)

**Failure state**: If P0 or P1 bugs exist at launch window, delay launch. Shipping broken is worse than shipping late.

---

## 10. Regression Testing Checklist

**This checklist is executed before every major milestone and before launch.**

Run all test cases in sections 2.1 through 8. Priority order:

1. **P0 tests first** (blockers - game cannot ship with these failing)
2. **P1 tests second** (major issues - significantly impact experience)
3. **P2 tests third** (minor issues - polish and edge cases)
4. **P3 tests last** (nice-to-have - stretch goals)

**Regression cadence**:
- **Weekly**: P0 tests only (smoke test)
- **Monthly**: P0 + P1 tests (major regression)
- **Pre-beta**: All tests (full regression)
- **Pre-launch**: All tests (full regression)

**Regression blocking criteria**:
- Any P0 failure blocks next milestone
- 5+ P1 failures block next milestone
- P2/P3 failures are documented but do not block

**Regression ownership**: QA lead (CRASH) assigns test cases to team members. Every discipline has a test owner. Every system has a test owner. No one ships their own code without another team member's validation.

---

## 11. Bug Triage and Priority Definitions

### Priority 0 (P0): Blocker
- Game crashes
- Soft-locks (player stuck, cannot progress)
- Save corruption
- Performance <30fps on target hardware
- Core mechanic completely broken (can't drift, can't attack, can't shoot)

**Action**: Drop everything and fix immediately. No other work proceeds until P0 is resolved.

### Priority 1 (P1): Major
- Mechanic works but feels broken (input lag, physics glitches)
- AI completely incompetent or unfair
- UI blocks critical information
- Audio missing or severely distorted
- Progression system awards incorrect values (REP/CASH off by >20%)

**Action**: Fix within 1 sprint (2 weeks). Assign owner immediately.

### Priority 2 (P2): Minor
- Polish issues (animation pops, minor visual glitches)
- Edge case bugs (rare occurrences, <5% of players will see)
- Balance issues (economy too tight/loose, difficulty spikes)
- UX friction (menu navigation clunky but functional)

**Action**: Fix if time allows. Document for post-launch patch if not critical.

### Priority 3 (P3): Trivial
- Cosmetic issues (typos, minor art inconsistencies)
- Stretch goal features not working (beat-sync, advanced synergies)
- Exploits that require deliberate effort and don't break economy

**Action**: Nice to fix, not required for launch. Community can report for future patches.

---

## 12. Playtesting Protocol

### Internal Playtests (Weekly)

**Participants**: Full team (programmers, designers, artists)
**Duration**: 1 hour
**Format**: Structured
**Goals**: Find obvious bugs, validate new features, feel-check

**Process**:
1. CRASH assigns focus area (e.g., "Test racing AI this week")
2. Team plays for 45 minutes
3. 15-minute feedback session (what broke? what felt bad?)
4. Bugs logged immediately
5. High-priority bugs assigned before next standup

### External Playtests (Monthly, starting Month 6)

**Participants**: 10-20 external testers (friends, community, paid testers)
**Duration**: 2 hours
**Format**: Unstructured (players choose what to do)
**Goals**: Find edge cases, validate progression pacing, measure engagement

**Process**:
1. Send build to testers with minimal instructions
2. Testers play and fill out feedback form:
   - What did you do?
   - What was fun?
   - What was frustrating?
   - What was confusing?
   - Did you want to keep playing?
3. Optional: Watch testers play via screen share (identify confusion points)
4. CRASH compiles feedback into prioritized bug/feature list
5. Team reviews and assigns fixes

### Beta Test (Month 17)

**Participants**: 50-100 external testers (public signups via Discord/social)
**Duration**: 2 weeks
**Format**: Full game access, unstructured
**Goals**: Stress test, find critical bugs, validate balance

**Process**:
1. Publish beta build to Steam (private branch)
2. Testers report bugs via Discord or in-game form
3. CRASH triages daily:
   - P0 bugs: Fixed immediately
   - P1 bugs: Fixed within beta window
   - P2/P3 bugs: Documented for post-launch
4. End of beta: Regression test all P0/P1 fixes
5. If new P0 bugs found, extend beta

---

## 13. Known Risks and Mitigation

### Risk 1: Four Disciplines = Four Times the Bug Surface

**Severity**: Critical
**Likelihood**: Certain

**Mitigation**:
- Test each discipline in isolation first (vertical slice approach)
- Don't integrate until each discipline is stable
- Dedicate QA time per discipline (not just cross-discipline)
- Accept that bugs will multiply. Plan QA budget accordingly.

### Risk 2: Cross-Discipline Bugs Are Hard to Reproduce

**Severity**: High
**Likelihood**: High

**Example**: "Style Meter didn't carry over from race to fight, but only sometimes."

**Mitigation**:
- Logs. Logs everywhere. Every Style Meter change, every discipline transition, logged with timestamp.
- Repro steps must include full context (which district, which rival, which events in sequence, what time of session)
- If bug is not reproducible in 3 attempts, deprioritize until more data is available.

### Risk 3: Rival AI Bugs Are Emergent (Hard to Predict)

**Severity**: High
**Likelihood**: Medium

**Example**: "Rival became Obsessed and now crashes every single event. Game is unplayable."

**Mitigation**:
- Rival state is saved and inspectable (debug overlay shows Respect, Grudge, Confidence)
- Hard caps on Obsession interrupt rate (40% per event, not 100%)
- Kill switch: If rival AI breaks, player can "retire" rival via debug menu (last resort)

### Risk 4: Performance Degrades Over Session (Memory Leak)

**Severity**: High
**Likelihood**: Medium

**Mitigation**:
- Long-play tests (2+ hour sessions) weekly
- Memory profiler active during tests
- If memory usage trends upward, identify leak source immediately (likely particle systems or audio sources not being pooled)

### Risk 5: Save Corruption in the Wild

**Severity**: Critical
**Likelihood**: Low (but devastating if it happens)

**Mitigation**:
- Backup save system: Game keeps last 3 saves (save.json, save_backup1.json, save_backup2.json)
- If primary save is corrupt, load most recent backup
- Logging: Every save operation logs success/failure to separate log file
- If corruption reports come in, analyze logs to find root cause

---

## 14. Post-Launch QA Plan

### Week 1 Post-Launch

**Monitoring**:
- Steam forums, Discord, Reddit for bug reports
- Crash analytics (Unity Analytics or Sentry.io)
- Player completion rates (are players dropping off at specific points?)

**Hotfix criteria**:
- P0 bugs reported by 5+ players: Hotfix within 24-48 hours
- P1 bugs reported by 20+ players: Hotfix within 1 week

### Month 1 Post-Launch

**Balance patch**:
- Analyze economy data (are players cash-starved or swimming in money?)
- Analyze discipline usage (are all four disciplines played equally?)
- Adjust REP/CASH payouts, difficulty scaling based on data

**Bug fixes**:
- Address all P1 bugs found in first month
- Document P2 bugs for future patches

### Ongoing Support (Months 2-6)

**Monthly patches**:
- Bug fixes from community reports
- Balance tweaks based on player feedback
- Performance optimizations if issues are found on specific hardware

**DLC considerations** (if game is successful):
- New district
- Fifth discipline (skateboarding?)
- Advanced rival system features

---

## 15. Conclusion

UNDERGROUND is the most complex game this studio has built. Four genres, emergent AI, cross-discipline progression, 60fps on Steam Deck. Every system talks to every other system. The bug surface is massive.

But the testing strategy is clear:

1. **Test in isolation first.** Each discipline must work alone before integration.
2. **Test the seams.** Cross-discipline transitions are where bugs hide.
3. **Test on minimum spec.** Steam Deck is the floor. If it runs there, it runs everywhere.
4. **Test for hours, not minutes.** Memory leaks, progression bugs, and emergent AI issues only appear in long sessions.
5. **Test with real players.** Internal testing finds mechanical bugs. External testing finds confusion and frustration.

Quality gates are non-negotiable. If racing isn't fun by month 3, we do not proceed. If the core loop is broken at month 12, we do not add content. Every gate exists because past projects failed by skipping them.

Regression is not optional. Before every milestone, before beta, before launch: run the full test suite. P0 bugs block everything. P1 bugs block milestones. P2/P3 bugs are documented but don't stop the ship.

This is not a game that can be "figured out in post." Every bug we ship is a player's entire experience. Every soft-lock is a 1-star review. Every crash is someone who paid money and got nothing.

We find the bugs before the players do. Every single one. That's the job.

Let's break this thing until it's unbreakable.

---

**Document version**: 1.0
**Next review**: After racing vertical slice (Month 3)
**Owner**: CRASH (QA Lead)

---

*What happens if the player does THIS? Now let's find out.*
