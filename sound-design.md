# UNDERGROUND — Audio Design Document

**Author**: ECHO (Sound Designer & Composer)
**Status**: Complete Audio Direction — Ready for Implementation
**Version**: 1.0
**Date**: 2026-02-07

---

## 1. Sonic Identity Statement

**The sound of UNDERGROUND is asphalt breathing — the wet hiss of tire smoke against neon rain, the thud of a body hitting chain-link, the swish of net and the crack of a kickflip reverberating through a city that never stops listening.**

This is the sound of legend-making at street level. Every drift, punch, crossover, and grind leaves an auditory mark. Close your eyes and you still know exactly what discipline you're in, exactly what the stakes are, exactly how much style you're generating. Audio IS game feel here. Take the sound away and you're left with a tech demo pretending to be 2003.

---

## 2. Sonic Palette

### 2.1 Keynote

**Urban Mechanical Warmth**. The keynote is the hum of the city at 2 AM — distant traffic, electrical transformer buzz, fluorescent light flicker, ventilation systems breathing. Underneath everything, there's a low-frequency pulse that matches the Style Meter's heartbeat. The city has a resting frequency: 55-80 Hz, felt more than heard. When the Style Meter hits UNDERGROUND MODE, that frequency shifts up to 85-110 Hz and becomes explicit in the mix. The world literally resonates with your performance.

The keynote is never silent. Even in menus, you hear the city. Silence is not absence of sound — it's the negative space between two beats. The moment before impact. The breath before the drop.

### 2.2 Texture

**Warm analog crunch meets cold digital precision.**

- **Warm**: Engine growls recorded with contact mics on metal, not clean studio recordings. Footsteps with real concrete scuff. Punch impacts layered with leather foley, raw and visceral. The human elements — breath, cloth, skin contact — are warm, saturated, slightly distorted like they're passing through a tape deck.

- **Cold**: UI sounds are FM-synthesized tones with short decay. The Style Meter fill-up uses digital granular synthesis. Neon signs hum with pure sine waves. The city's infrastructure is sterile, mathematical, uncaring. The contrast matters — your actions are warm, the world is cold, until you heat it up with style.

- **Saturation**: Everything pushing just past clean. 3-5% harmonic distortion on most SFX, giving them body and presence without sounding broken. This is the PS2 era's technical limitation turned into aesthetic choice. We're not emulating lo-fi for nostalgia — we're using saturation to make every sound feel THICK.

### 2.3 Space

The city is dense and intimate, not vast and open. Sound reflects. Alleyways give you 120-180ms reverb tails, tight and metallic. Open parking garages bloom into 400-600ms reverb with pre-delay, cavernous but controlled. Rooftop courts are dry and exposed, with barely 30ms early reflections — the only space where your sound doesn't echo back at you.

Every district has its own reverb signature:
- **Southside (racing district)**: Concrete underpass reverb, mid-heavy, 300ms tail
- **The Docks (fighting district)**: Warehouse metal reverb, bright and harsh, 450ms tail
- **Midtown (basketball district)**: Chain-link and brick, dry with sharp slap-back at 80ms
- **Industrial Zone (tricks district)**: Open air with distant buildings, subtle 200ms ambiance

The player should be able to close their eyes, hear a single footstep, and know where they are.

### 2.4 Reference Tracks & Games

These are the sonic touchstones. The frequencies we're chasing.

**Music References:**
1. **Dilated Peoples — "Worst Comes to Worst" (2001)**: The baseline for hip-hop in the game. Boom-bap drums, analog warmth, mid-tempo groove. This is the frequency of cruising through the city at night.
2. **The Roots — "The Seed 2.0" (2002)**: Distorted bassline, live drums mixed with samples. Genre-bending before genre-bending was everywhere. The energy we want when the Style Meter hits HOT.
3. **OutKast — "B.O.B." (2000)**: Controlled chaos. Fast tempo, dense production, never lets up. This is UNDERGROUND MODE's anthem energy.
4. **Pharoahe Monch — "Simon Says" (1999)**: That Godzilla sample. Aggressive, immediately iconic, impossible to ignore. The hookiness we need in boss fight themes.
5. **DJ Shadow — "Building Steam With a Grain of Salt" (1996)**: For exploration moments. Downtempo, textured, sample-heavy. Proof that instrumental hip-hop can carry emotional weight.

**Game Audio References:**
1. **Need for Speed Underground 2 (2004)**: The gold standard for racing audio + soundtrack integration. Engine notes that sing, tire squeals that telegraph grip loss, nitrous that sounds like controlled explosion. We take the engine design philosophy wholesale.
2. **Def Jam: Fight for NY (2004)**: Impact design that feels like it costs something. Punches have weight, slams shake the screen, crowd reaction is a character. We're aiming for this fight audio fidelity.
3. **Tony Hawk's Pro Skater 3 (2001)**: Trick chaining audio design with the grind pitch-shift system and the perfect "pop" sound. The audio tells you if you're in the combo zone or about to bail. Crystal-clear audio communication.
4. **NBA Street Vol. 2 (2003)**: The swish sound design, the trash-talk integration, the gamebreaker buildup. Sports audio that's stylish first, realistic second.
5. **Jet Set Radio Future (2002)**: Not a direct genre match, but the ENERGY. The way music drives momentum, the way SFX are percussive and rhythmic. The fearlessness to let audio be LOUD and PRESENT.

### 2.5 What This Game Does NOT Sound Like

- Not photo-realistic. Not Forza's pristine engine recordings or UFC's clean punch foley. We're not simulating — we're expressing.
- Not ambient or minimal. Every action needs audio feedback. Silence is a tool, not a default.
- Not retro chiptune or lo-fi fetishism. The PS2 aesthetic is VISUAL. The audio uses modern DSP to create a saturated, thick, present soundscape that the PS2 could only dream of.
- Not licensed soundtrack reliance. The music is original, written for adaptive implementation. Licensed tracks (if budget allows) are accents, not the foundation.

---

## 3. Sound Effects Design

### 3.1 SFX Organization Philosophy

Every sound serves one of three functions:
1. **Critical Feedback**: Information the player needs to react (low health, critical hit, meter full)
2. **Performance Feedback**: Reinforcement of player actions (footsteps, tire squeal, ball bounce)
3. **World Presence**: Environmental texture that makes the space feel alive (ambient traffic, crowd chatter, neon hum)

Mix priority follows that order. If a critical feedback sound plays, everything else ducks. No exceptions.

---

### 3.2 RACING SFX

#### 3.2.1 Engine & Drivetrain

**Base Engine Loop (per car class)**:
- **Description**: 3-layer engine system — idle layer (800-1200 RPM), mid-range layer (2000-4500 RPM), redline layer (5000-7200 RPM). Each layer recorded with contact mics on actual engine blocks, not exhaust pipes. We want the mechanical vibration, the combustion texture, not clean exhaust note. Layers crossfade based on RPM with 200ms crossfade time.
- **Emotional Function**: The engine is the player's voice in racing. It needs to feel responsive, alive, eager. At idle, it should sound restrained. At redline, it should sound desperate to move.
- **Variation Needs**: 4 engine types (tuner 4-cylinder, V6, muscle V8, rotary). Each type needs 3 full loop layers + decel loops + backfire variants. Total: 60 engine loops.
- **Implementation**: FMOD parameter-driven pitch and volume curves. RPM mapped to RTPC. Gear shifts trigger momentary pitch drop + clutch sound.

**Gear Shift**:
- **Description**: 80-120ms mechanical clunk + transmission whine. Pitch varies by gear (higher gears = lower pitch shift, 50Hz down at 1st, 20Hz down at 5th). On perfect shifts (shift at redline), add a subtle "click" at 8kHz for that satisfying snap.
- **Emotional Function**: Tactile confirmation. The difference between a sloppy shift and a perfect shift should be audible before it's visible in performance.
- **Variation Needs**: 5 per car (one per gear). 4 car types. 20 total samples.

**Tire Squeal & Drift**:
- **Description**: Contact-based tire squeal, not musical squeal. Recorded at multiple slip angles: light squeal (5-15 degree slip), mid squeal (15-30 degree), full drift (30-45 degree). Frequency content: 800Hz-3kHz, gritty and granular. Drift smoke adds a subtle low-frequency rumble (60-120Hz) felt through controller haptics more than heard.
- **Emotional Function**: The tire squeal is the feedback loop for drift mastery. Light squeal = you're on the edge. Mid squeal = you're in the pocket. Silence = you've lost it.
- **Variation Needs**: 3 intensity layers x 4 surfaces (asphalt, concrete, metal grating, wet asphalt). 12 loops. Plus: 8 one-shot tire chirps for sudden corrections.

**Nitrous**:
- **Description**: Two-stage sound. Stage 1: Activation (200ms) — pressurized gas release, sharp hiss at 6-8kHz. Stage 2: Burn (duration varies, 2-5 seconds) — sustained mid-frequency roar (400-800Hz) with wavering pitch modulation to suggest instability. On nitrous end, a subtle "gasp" as the system depressurizes.
- **Emotional Function**: Power. Barely controlled explosion. Using nitrous should feel dangerous and thrilling.
- **Variation Needs**: 2 types (burst vs. sustained, from the build system). 4 samples total (2 types x activation+burn).

**Collision & Damage**:
- **Description**: Impact is frequency-split. Low impact (<20mph difference): 200-500Hz crunch, short (150ms), sounds like fender damage. Mid impact (20-40mph): 150-600Hz, longer (400ms), includes glass break layer. High impact (40+mph): full-spectrum (80Hz-8kHz), 800ms, sounds catastrophic. Every impact adds a metallic resonance tail that rings based on car weight (heavy cars = lower pitch ring).
- **Emotional Function**: Punishment. Every hit should make the player wince. Damage is not just visual — it's sonic trauma.
- **Variation Needs**: 5 impact severities x 3 material types (car-to-car, car-to-concrete, car-to-metal). 15 one-shots + 5 glass break layers.

**Near-Miss Bonus**:
- **Description**: When player passes within 1 meter of traffic/obstacles at speed, trigger a 60ms whoosh (2-6kHz wind rush) + a 40ms metallic "zing" (8-10kHz). This sound is LOUD (+6dB above mix) and attention-grabbing. It says "you almost died and it was awesome."
- **Emotional Function**: Risk reward. The sound is a dopamine hit.
- **Variation Needs**: 4 variants with slight pitch variation to avoid repetition fatigue.

**Underglow Audio Signature**:
- **Description**: Underglow kits emit a barely-audible 120Hz electrical hum when active. Subtle, almost subliminal, but adds to the car's presence. When Style Meter hits HOT tier, the underglow hum shifts up to 180Hz and gains a subtle flanger effect.
- **Emotional Function**: Presence. Your car announces itself.
- **Variation Needs**: 2 states (normal, HOT+). Loopable.

#### 3.2.2 Environment (Racing)

**Traffic Ambiance**:
- **Description**: Distant traffic loop, 2-4 cars passing per 10 seconds, panned across stereo field. Doppler shift applied. Mix sits at -24dB, barely there unless you're listening for it.
- **Emotional Function**: The city is alive whether you're racing or not.

**Rain (Wet Races)**:
- **Description**: Light rain layer (high-frequency patter, 4-8kHz) + tire-on-wet-asphalt layer (adds splash sounds, 200-400Hz). Rain never gets heavy — this is atmospheric drizzle, not a storm.
- **Emotional Function**: Texture. Makes night races feel colder, more dangerous.

---

### 3.3 FIGHTING SFX

#### 3.3.1 Combat Impact

**Punch (Light)**:
- **Description**: 3-layer hit. Layer 1: Fist-on-skin foley (80-300Hz, meaty thud). Layer 2: Body displacement whoosh (400-800Hz, short tail). Layer 3: Clothing rustle (2-4kHz, quick). Total duration: 150ms. Light punches sit at -6dB relative to heavy punches.
- **Emotional Function**: Feedback without overwhelming. Fast jabs should sound quick and sharp, not heavy.
- **Variation Needs**: 8 variants (2 per limb).

**Punch (Heavy)**:
- **Description**: Same 3-layer structure but each layer is 40% longer in duration and +6dB louder. Add a low-frequency sub-thump at 50-80Hz for controller rumble. Heavy punches have a slight pitch-down on the impact (start at 1.0x, drop to 0.92x over 100ms) to give them weight.
- **Emotional Function**: Consequence. A heavy hit should interrupt the player's breathing rhythm.
- **Variation Needs**: 8 variants (2 per limb).

**Kick**:
- **Description**: Heavier than punch. Impact layer is 100-400Hz, thicker and more resonant. Add a "whip" sound before impact (600ms lead-in, high-frequency air cut, 3-6kHz) to telegraph the kick. On connect, briefly duck all other SFX by -4dB for 80ms to emphasize impact.
- **Emotional Function**: The most damaging basic move. Should sound definitive.
- **Variation Needs**: 6 variants.

**Grab & Throw**:
- **Description**: Two-part sound. Part 1: Grab (200ms) — cloth grab foley + brief struggle grunt from opponent. Part 2: Throw impact (300ms after grab) — body-slam sound (full-spectrum thud, 60Hz-2kHz) + environmental reaction (chain-link rattle if near fence, concrete scrape if ground, etc.). Throw impacts are +3dB louder than heavy punches.
- **Emotional Function**: Spectacle. Grabs are high-commitment moves and need audio that matches.
- **Variation Needs**: 4 grab variants, 6 throw impact variants (2 per surface type).

**Counter/Parry**:
- **Description**: Sharp, high-frequency "snap" (3-8kHz) + immediate silence for 100ms (everything except music ducks to near-zero). The silence is the sound design. The counter is so clean it creates a gap in the audio. After the silence, a subtle low-frequency "thoom" (40-60Hz) as the counter follow-up lands.
- **Emotional Function**: Mastery. A successful counter should feel like stopping time.
- **Variation Needs**: 3 variants.

**Taunt**:
- **Description**: Character vocalization (recorded lines, 800ms-1.5s, pitched to character) + crowd reaction surge (crowd volume +6dB for duration of taunt). No foley impact — this is pure performance.
- **Emotional Function**: Risk and provocation. The sound is confident, almost reckless. You're daring the opponent to hit you.
- **Variation Needs**: 12 taunt lines per character archetype (3 archetypes = 36 total lines).

**Finisher**:
- **Description**: Multi-stage sound event. Stage 1: Wind-up (1-2 seconds, rising pitch tone from 200Hz to 800Hz + heartbeat-like bass pulse). Stage 2: Impact (full-spectrum explosion of sound, 30Hz-12kHz, everything-at-once, peak at +3dB above all other SFX). Stage 3: Aftermath (3-second reverb tail, crowd eruption, slow-motion audio processing — pitch down 15%, time-stretch without pitch artifacts).
- **Emotional Function**: Climax. The end of the fight. Should feel earned and definitive.
- **Variation Needs**: 4 finisher types (each with unique wind-up signature).

#### 3.3.2 Movement (Fighting)

**Footsteps (Combat)**:
- **Description**: Heavier and more aggressive than exploration footsteps. Each step is 100-250Hz concrete scuff + slight cloth rustle. Footsteps trigger on every step during combat at full volume. Outside combat, footsteps are -12dB quieter.
- **Emotional Function**: Rhythm. The footsteps are the beat of the fight.
- **Variation Needs**: 8 step variants x 3 surfaces (concrete, metal, dirt). 24 samples.

**Dodge Roll/Weave**:
- **Description**: 400ms cloth rustle + air displacement whoosh (600Hz-2kHz). Pitch bends down slightly at the end to suggest settling.
- **Emotional Function**: Evasion. Sounds slippery and quick.
- **Variation Needs**: 4 variants.

#### 3.3.3 Environment (Fighting)

**Crowd (Fighting)**:
- **Description**: Layered crowd loop. Base layer: 40-person crowd loop, general chatter and anticipation, sits at -18dB. Reaction layers (triggered by events): "ooh" reaction (on near-miss or counter, +10dB spike for 1 second), "roar" reaction (on knockdown or finisher, +12dB spike for 2-3 seconds), "taunt reaction" (on player taunt, mixed jeers and cheers, +8dB for duration of taunt).
- **Emotional Function**: The crowd is a character. They amplify your success and mock your failure.
- **Variation Needs**: 3 crowd base loops per fight venue (indoor warehouse, outdoor cage, underground club). 8 reaction one-shots.

**Chain-Link Fence Rattle**:
- **Description**: When fighters are slammed into fence or when crowd grabs fence, trigger metallic rattle (1-4kHz, decays over 800ms). Sounds harsh and industrial.
- **Emotional Function**: Environmental storytelling. This is not a clean fight.

---

### 3.4 STREET SPORTS (BASKETBALL) SFX

#### 3.4.1 Ball Handling

**Ball Bounce**:
- **Description**: Single bounce on concrete: 200-400Hz thud with short decay (150ms). Frequency varies by bounce intensity — hard dribble is lower (180Hz fundamental), soft dribble is higher (350Hz). Each bounce triggers a subtle high-frequency "slap" (2-3kHz, 30ms) from hand-to-ball contact.
- **Emotional Function**: Rhythm and control. The bounce is the metronome of the game.
- **Variation Needs**: 6 bounce intensities. 12 samples (6 intensities x 2 for L/R hand panning).

**Crossover**:
- **Description**: Rapid double-bounce (two bounces within 200ms) + hand slap + rubber squeak from shoe pivot (1-3kHz, quick). On successful ankle-breaker, add a sharp "snap" sound (6kHz, 50ms) — not realistic, purely expressive.
- **Emotional Function**: Style and domination. The crossover snap is the "got 'em" audio cue.
- **Variation Needs**: 4 crossover variants.

**Pass**:
- **Description**: Ball leaving hand: air whoosh (400-800Hz, 150ms duration scaled to pass distance). Ball catch: thud (200Hz) + hand clap (1-2kHz). Alley-oop passes add a rising pitch whoosh to suggest loft.
- **Emotional Function**: Team play. Passes should sound crisp and intentional.
- **Variation Needs**: 3 pass types (chest pass, bounce pass, alley-oop). 9 samples.

**Shot Release**:
- **Description**: Ball release: subtle hand-flick sound (2-4kHz, 60ms) + cloth rustle from shooting motion. No net sound yet — that's the payoff.
- **Emotional Function**: Anticipation. The moment before success or failure.

**Swish**:
- **Description**: The most satisfying sound in the game. Net rustle (1-4kHz, crisp and clean, 400ms duration with tail) + a subtle "ding" (6kHz sine tone, 80ms) that's not literally there but IMPLIED by the mix. Perfect swishes (shots taken at optimal release timing) get a pitch-perfect 1320Hz tone (E6 note) layered in at -12dB. Imperfect swishes omit the tone.
- **Emotional Function**: Perfection. The swish is the audio reward for execution.
- **Variation Needs**: 2 variants (perfect swish with tone, normal swish without).

**Rim Hit/Brick**:
- **Description**: Ball hits rim: metallic clang (800-2kHz, harsh and dissonant, 300ms decay). On brick (missed shot that hits rim hard), emphasize the 1.2kHz frequency band for maximum harshness. No net sound.
- **Emotional Function**: Failure. Should sting a little.
- **Variation Needs**: 4 variants (light rim touch, hard rim hit, front rim brick, back rim out).

#### 3.4.2 Movement (Basketball)

**Shoe Squeak**:
- **Description**: Rubber-on-concrete squeak, 1-3kHz, duration varies (50ms for quick cut, 200ms for sustained pivot). Squeak intensity tied to change in direction vector — sharp cuts trigger louder squeaks.
- **Emotional Function**: Agility. The squeak is the audio signature of court control.
- **Variation Needs**: 8 variants (various pitches and durations).

**Dunk Impact**:
- **Description**: Multi-layer explosion. Layer 1: Rim stress (metallic groan, 200-600Hz, 400ms). Layer 2: Backboard shake (low-frequency rumble, 40-100Hz, 600ms). Layer 3: Net violent rustle (1-4kHz, 500ms). Layer 4: Crowd eruption (+12dB spike, 2 seconds). On contact dunks (defender nearby), add a body-collision layer from fighting SFX.
- **Emotional Function**: Dominance. The dunk is the fight finisher of basketball.
- **Variation Needs**: 3 dunk types (standard, contact, alley-oop).

#### 3.4.3 Environment (Basketball)

**Court Ambiance**:
- **Description**: Outdoor court: distant traffic (barely audible, -28dB), breeze (high-frequency texture, 4-8kHz, intermittent), chain-link fence creak. Indoor gym: HVAC hum (120Hz fundamental), shoe squeaks from other courts (distant, -20dB).
- **Emotional Function**: Place and stakes. Outdoor feels raw, indoor feels organized.

**Crowd (Basketball)**:
- **Description**: Smaller crowd than fighting (10-20 people), more reactive. Constant low-level chatter (-20dB). React to: made shots (+6dB cheer, 800ms), missed shots (brief silence, 400ms), crossovers (+8dB "oooh", 600ms), dunks (+10dB roar, 2 seconds).
- **Emotional Function**: Amplification. Your highlights get hyped.

---

### 3.5 FREESTYLE TRICKS SFX

#### 3.5.1 Skateboard (or BMX/Inline)

**Wheel Roll**:
- **Description**: Continuous loop, frequency content 200-800Hz, granular and gritty. Volume and pitch tied to speed. At low speed (0-5 mph): quiet, 250Hz. At high speed (20+ mph): loud, 600Hz with added wind layer (1-4kHz).
- **Emotional Function**: Speed feedback. You should hear acceleration.
- **Variation Needs**: Single loop with parameter-driven pitch/volume.

**Ollie/Pop**:
- **Description**: Tail hits ground: sharp crack (1-3kHz, 80ms) + wood stress creak (400-800Hz, 100ms). The pop is the initiation of every trick. Needs to be sharp and responsive.
- **Emotional Function**: Initiation. The first beat in the trick rhythm.
- **Variation Needs**: 4 pop variants (slight pitch variation).

**Grind**:
- **Description**: Metal-on-metal scrape (primary frequency 800-3kHz, harsh and sustained). Pitch varies by grind surface material. Rails (metal): bright, 2-3kHz emphasis. Ledges (concrete): darker, 600-1200Hz. Add sparks layer (high-frequency crackle, 6-10kHz, intermittent). Grinds trigger rumble (60-120Hz) felt through haptics.
- **Emotional Function**: Texture and risk. The grind sound is abrasive and exciting.
- **Variation Needs**: 3 surface types x 2 grind types (trucks vs. board). 6 loops.

**Land (Clean)**:
- **Description**: Wheels reconnect with ground: solid thud (150-400Hz, 100ms) + brief wheel skip sound (400Hz, 60ms). Clean lands are tight and satisfying.
- **Emotional Function**: Success. The punctuation mark on a combo.
- **Variation Needs**: 3 variants.

**Land (Rough)**:
- **Description**: Wheels hit unevenly: lower-frequency thud (100-300Hz, longer duration 200ms) + wood stress sound (board flexing, 300-600Hz, 150ms). Rough lands don't break the combo but sound less confident.
- **Emotional Function**: Near-failure. You made it, but barely.
- **Variation Needs**: 3 variants.

**Bail/Crash**:
- **Description**: Board hits ground separately from rider. Board clatter (wood bouncing on concrete, 400Hz-2kHz, 1-2 seconds of decay). Body impact (dull thud, 80-200Hz, 300ms) + cloth scrape (1-3kHz, 500ms). Ends combo. Painful.
- **Emotional Function**: Consequence. The sound of ambition exceeding ability.
- **Variation Needs**: 4 bail variants (varying severity).

**Manual/Balance**:
- **Description**: When in manual (balancing on two wheels), add a subtle ticking sound (wood stress, 600-1200Hz, ticks every 200ms) to indicate instability. The longer the manual, the faster the ticking (down to 100ms intervals). When manual ends (lands on all wheels), ticking stops, replaced by clean land sound.
- **Emotional Function**: Tension. The ticking is the countdown to failure.

#### 3.5.2 Environment (Tricks)

**Industrial Ambiance**:
- **Description**: Warehouse/industrial zone: metal creaks (intermittent, 200-800Hz), distant machinery hum (80-150Hz, constant), air movement through large spaces (reverb tail 400-600ms).
- **Emotional Function**: Space. These areas feel abandoned but alive.

**Trick Callout/Combo Counter**:
- **Description**: On trick completion, brief UI sound (FM-synth tone, 1.5kHz, 40ms, staccato). Pitch rises with combo count (1.5kHz for first trick, up to 3kHz by 10th trick). At combo 5+, add a subtle riser (200Hz-800Hz sweep over 2 seconds) building tension.
- **Emotional Function**: Progress and risk awareness. The rising pitch tells you how much you have to lose.

---

### 3.6 UNIVERSAL / UI SFX

#### 3.6.1 Style Meter

**Meter Fill (Continuous)**:
- **Description**: Subtle granular synthesis tone that rises in pitch as meter fills. At COLD (0-249 points): 200Hz, barely audible. At WARM (250-499): 400Hz, +3dB. At HOT (500-749): 700Hz, +6dB. At ON FIRE (750-999): 1000Hz, +9dB, starts to pulse rhythmically (pulse every 400ms). The tone is felt more than heard — it sits under the mix but adds tension.
- **Emotional Function**: Awareness. The player should subconsciously know their meter state from the audio bed.
- **Variation Needs**: Parameter-driven single layer.

**Meter Tier Transition**:
- **Description**: When crossing tier thresholds, trigger a brief "whomp" (sub-bass hit, 40-60Hz, 100ms) + ascending tone (sweep from current tier frequency to next tier frequency over 200ms). Transition to ON FIRE includes a kick drum hit (synthesized 808-style, 50Hz, punchy).
- **Emotional Function**: Milestone. You're leveling up your performance in real-time.
- **Variation Needs**: 3 sounds (COLD->WARM, WARM->HOT, HOT->ON FIRE).

**Underground Mode Activation**:
- **Description**: Everything ducks -6dB for 200ms (except music). Then: massive sub-bass drop (30-50Hz, sustained for 800ms) + high-frequency "shatter" (8-12kHz, crystalline break, 400ms) + vinyl scratch sample (nostalgic nod, 1-4kHz, 300ms). Music changes mix (bass boost, high-hat emphasis, everything gets louder and more present). World SFX pitch down 15% for duration of mode (slow-motion effect). The activation sound is the biggest singular SFX event in the game outside of boss finishers.
- **Emotional Function**: Power. Becoming legendary feels like breaking reality.
- **Variation Needs**: 1 sound (too iconic to vary).

**Underground Mode Deactivation**:
- **Description**: Pitch and time return to normal over 400ms. Brief "exhale" sound (not literal breath, but a release of pressure — synthesized downward sweep, 800Hz to 200Hz, 300ms). Meter drains with a granular disintegration sound (like sand falling, 2-6kHz, 1 second).
- **Emotional Function**: Return to earth. The high is over.

#### 3.6.2 UI Feedback

**Menu Navigation**:
- **Description**: Cursor move: short FM-synth blip (1.2kHz, 30ms, staccato). Button hover: same blip +200Hz (1.4kHz). These are cold, digital, sterile. The menus are the only part of the game that don't have warmth.
- **Emotional Function**: Clarity. UI sounds should never be confused with world sounds.
- **Variation Needs**: 2 sounds (move, hover).

**Menu Confirm**:
- **Description**: Low-frequency thud (120Hz, 80ms) + high-frequency "ding" (2.8kHz, 60ms). Satisfying and definitive.
- **Variation Needs**: 1 sound.

**Menu Cancel/Back**:
- **Description**: Reverse of confirm — descending tone (1.5kHz to 800Hz over 100ms), softer.
- **Variation Needs**: 1 sound.

**Purchase/Upgrade**:
- **Description**: Cash register "cha-ching" (not literal, synthesized — ascending chord, 800Hz + 1200Hz + 1600Hz, staggered by 40ms each, total 200ms). Warm and rewarding.
- **Variation Needs**: 1 sound.

**Insufficient Funds/Error**:
- **Description**: Dissonant buzz (200Hz + 207Hz beating against each other, 300ms). Unpleasant. You don't want to hear this sound.
- **Variation Needs**: 1 sound.

**Notification/Phone Ring**:
- **Description**: Flip-phone vibration buzz (emulated through granular noise, 400-800Hz, rhythmic pulse 200ms on / 200ms off, repeats 3 times) + subtle melodic ringtone (2000s polyphonic phone melody, 8 notes, 2 seconds total). When player opens phone, notification sound plays: brief ascending tone (600Hz to 1.2kHz, 150ms).
- **Emotional Function**: Nostalgia and urgency. The phone is your connection to the crew and the underground.
- **Variation Needs**: 3 ringtone melodies, 1 vibration loop, 1 open sound.

**REP Gain (On-Screen)**:
- **Description**: Subtle coin-collect sound (not Mario, more subtle — 1.5kHz sine tone, 60ms + soft bell layer at 3kHz, 100ms). Pitch varies by REP amount gained — small gains (under 50 REP): 1.5kHz, large gains (500+ REP): 2.4kHz. On massive REP gains (boss defeats, 1000+ REP), add a brief fanfare (4-note ascending melody, 800-1600Hz range, 1.5 seconds).
- **Emotional Function**: Reward feedback. Every bit of progress should register.
- **Variation Needs**: 3 sounds (small, large, massive).

**Rival Challenge Incoming**:
- **Description**: Siren-like warning (not literal siren — synthesized frequency sweep, 800Hz to 1.2kHz and back, looping, gets faster). Plays when rival enters proximity or issues challenge. Stops when player acknowledges or ignores.
- **Emotional Function**: Threat and opportunity. Something is about to happen.
- **Variation Needs**: 1 sound.

#### 3.6.3 Ambiance & World Presence

**City Base Ambiance (Omnipresent)**:
- **Description**: Layered loop, 4 layers mixed at varying volumes depending on district. Layer 1: distant traffic (cars passing, 200-800Hz, -28dB). Layer 2: electrical hum (transformer buzz, 120Hz fundamental with harmonics, -24dB). Layer 3: wind/air movement (high-frequency texture, 4-8kHz, -26dB). Layer 4: distant sirens/city life (intermittent, -30dB). This loop plays at all times, even in menus (quieter, -32dB). The city never stops.
- **Emotional Function**: Place. You are in a living world.

**Neon Sign Hum**:
- **Description**: Pure sine wave tone at 120Hz (or 60Hz in some districts for variation). Triggered by proximity to neon signs (under 5 meters). Stereo-panned based on sign location. Flickers occasionally (brief silence for 100ms, returns).
- **Emotional Function**: Detail. The environment has texture.

**Rain (Environmental)**:
- **Description**: Layered rain. Layer 1: close rain (high-frequency, 6-10kHz, sounds like individual drops on metal/concrete). Layer 2: distant rain (mid-frequency wash, 1-4kHz, sounds like rain on rooftops far away). Layer 3: puddle splash (intermittent, 200-600Hz, triggered when player moves through puddles). Rain is atmospheric, not oppressive — always light to medium intensity.
- **Emotional Function**: Mood. Rain makes the night feel colder and more cinematic.

**Crowd (Street/Ambient)**:
- **Description**: When events are active, crowd forms dynamically. Base crowd loop: 20-40 people, chatter and anticipation, -18dB. Proximity-based — closer to event circle, louder crowd (up to -6dB at center). Crowd reacts to player actions even if player hasn't entered event yet (walk by a race and you hear cheers as cars pass, walk by a fight and you hear impact reactions).
- **Emotional Function**: Invitation. The city is calling you to perform.

---

## 4. Music Direction

### 4.1 Style & Genre

**Primary Genre: Instrumental Hip-Hop / Boom-Bap with Electronic Flourishes**

The music is rooted in early-2000s underground hip-hop production aesthetics — sample-based, drum-heavy, analog warmth, mid-tempo grooves — but it's not limited by nostalgia. We're allowed to use modern production techniques (side-chain compression, granular synthesis, spatial mixing) to create something that SOUNDS like it could have existed in 2003 but is actually built for adaptive game audio in 2026.

**BPM Range**: 85-105 BPM for exploration and low-intensity gameplay. 110-135 BPM for high-intensity (combat, racing, boss events). UNDERGROUND MODE triggers a temporary pitch-up of +5-8% on the music, increasing perceived tempo without changing the actual timeline (keeps adaptive sync intact).

**Instrumentation**:
- **Foundation**: Sampled drum breaks (prioritize: Amen break, Funky Drummer, Think break) processed through bit-crushing and saturation. Kick at 60-80Hz, snare at 200-400Hz, hi-hats at 6-10kHz. Drums are LOUD in the mix, borderline aggressive. This is not background music.
- **Bass**: Sub-bass synth (Moog-style, 40-80Hz fundamental) + sampled upright bass or Fender Precision (100-250Hz for melodic movement). Bass is the second-loudest element after drums. The low-end is thick and ever-present.
- **Melodic Elements**: Rhodes electric piano, sampled vinyl crackle as texture, vinyl horn stabs, dusty string samples (filtered, lo-fi, nostalgic), occasional guitar licks (clean or slightly overdriven, Jazz/funk style). Melodic elements sit at -6dB relative to drums, providing texture not dominance.
- **Electronic Elements**: Analog synth pads (soft, warm, filling space), FM synthesis lead stabs (bright, cutting through at key moments), vinyl scratch samples as percussion (integrated into the beat, not just DJ flourishes).
- **Atmosphere**: Vinyl crackle and tape hiss as constant texture layer (-32dB, always present, adds warmth). Field recordings from the city (distant traffic, train pass-bys, muffled conversations) processed as rhythmic elements.

**What We Are NOT Doing**:
- Licensed soundtrack approach (music reacts to gameplay, not playlist-style)
- Trap/modern hip-hop production (no hi-hat rolls, no 808 slides, no super-compressed loud mastering)
- Orchestral or ambient electronica (this is STREET, not cinematic epicness or chill study beats)
- Realistic instrument emulation (the artificiality of samples is part of the aesthetic)

### 4.2 Emotional Arc Across Game

The music should mirror the player's emotional journey from nobody to legend:

| Game Phase | Music Characteristics | Emotional Target |
|------------|---------------------|------------------|
| **Early (Hours 0-5)**: Player is learning, struggling, hungry | Sparse arrangements. Kick, snare, hi-hat, bass, one melodic element max. Lots of space in the mix. Slower tempos (85-95 BPM). Minor key tonality (Am, Dm, Em). Occasional vinyl crackle silence gaps. | Loneliness, hunger, determination. The music should feel like a lo-fi mixtape recorded in a basement. |
| **Mid (Hours 5-15)**: Player is competent, building name, forming rivalries | Fuller arrangements. Add Rhodes, horn stabs, second melodic layer. Tempos rise (95-105 BPM). Key shifts to minor but with major chord resolutions (Am to C, giving hope). More confident drum programming (more fills, more variation). | Confidence, momentum, the taste of success. The music feels more produced, more intentional. |
| **Late (Hours 15-30)**: Player is known, stakes are high, district bosses falling | Dense arrangements. All elements present. Tempos hit 100-110 BPM. More harmonic complexity (7th chords, suspended chords, chromatic movement). Synth layers add tension. Drums are relentless. | Pressure, intensity, the weight of reputation. The music is as tight as the player's skill. |
| **Endgame (Hours 30+)**: Player is legendary, making final choices | Music becomes MORE sparse again, but now it's a choice, not a limitation. Return to simpler arrangements but with richer sound design. Tempos vary wildly (85 BPM for reflection, 130 BPM for final bosses). Key ambiguity (neither major nor minor, unresolved). | Reflection, consequence, legacy. The music knows you've made it and asks "was it worth it?" |

### 4.3 Adaptive Layers & Horizontal Sequencing

The music system uses a combination of vertical layering (adding/removing instruments) and horizontal sequencing (switching between sections) to react to gameplay state in real-time.

#### 4.3.1 Vertical Layering (Intensity System)

Every music track is composed in 5 layers that can be dynamically mixed:

1. **Foundation Layer (always playing)**: Kick, snare, hi-hat, bass. The rhythmic core. This layer NEVER stops. Even in menus.
2. **Texture Layer (plays at Style Meter WARM or higher)**: Vinyl crackle, atmospheric pad, field recording bed. Adds warmth.
3. **Melodic Layer 1 (plays at Style Meter HOT or higher)**: Primary melodic element (Rhodes, synth lead, horn stabs). Adds musicality.
4. **Melodic Layer 2 (plays during events / high engagement)**: Secondary melodic element, counter-melody, harmonic fills. Adds density.
5. **Accent Layer (plays at Style Meter ON FIRE or during UNDERGROUND MODE)**: Vinyl scratches as percussion, synth stabs, drum fills, everything gets more aggressive. Adds spectacle.

**Parameter Mapping**:
- Style Meter value -> controls layer volumes and low-pass filter cutoff on higher layers
- Event state (in-event vs. free-roam) -> triggers layer 4 activation
- UNDERGROUND MODE -> activates layer 5, pitch-shifts entire mix +6%, adds sidechain pumping (kick ducks everything else by -3dB on every beat)

#### 4.3.2 Horizontal Sequencing (Sections)

Each district has a musical "theme" composed in multiple sections that transition based on game state:

**Section Types**:
- **A Section (Exploration)**: 8-bar loop, sparse, groove-focused, no melodic resolution. Plays during free-roam.
- **B Section (Event Intro)**: 4-bar transitional phrase, builds tension, ends on suspended chord. Plays when entering an event.
- **C Section (Event Active)**: 16-bar loop, full intensity, melodic development, resolves every 16 bars. Plays during events.
- **D Section (Boss Intro)**: 8-bar one-shot, dramatic shift, often tempo change or key change. Plays when boss event triggers.
- **E Section (Boss Active)**: 32-bar loop, maximum density, most aggressive. Plays during boss fights.
- **F Section (Victory Sting)**: 2-bar one-shot, major chord resolution, triumphant. Plays on event win.
- **G Section (Defeat Sting)**: 2-bar one-shot, dissonant, unresolved. Plays on event loss.

**Transition Rules**:
- A -> B: Triggered on event enter, crossfade 2 beats
- B -> C: Triggered when event starts (countdown ends), hard transition on downbeat
- C -> A: Triggered on event exit, crossfade 4 beats
- C -> D: Triggered on boss challenge, hard cut
- D -> E: Triggered when boss fight starts, hard transition on downbeat
- E -> F/G: Triggered on boss win/loss, immediate transition (no crossfade, the finisher sound is the transition)
- F/G -> A: Triggered 2 seconds after sting completes, crossfade 8 beats

#### 4.3.3 District-Specific Musical Themes

Each of the four main districts has its own harmonic identity and instrumentation emphasis:

**Southside (Racing District)**:
- **Key**: A minor
- **Tempo**: 95-100 BPM (cruising speed)
- **Instrumentation Focus**: Bass-heavy (sub-bass always present), Rhodes electric piano for melody, minimal drums (kick and hi-hat prioritized for groove)
- **Mood**: Cool, nocturnal, blue-tinted. The sound of neon reflecting off wet asphalt.
- **Reference**: DJ Shadow's "Building Steam With a Grain of Salt" meets Nujabes

**The Docks (Fighting District)**:
- **Key**: D minor
- **Tempo**: 90-95 BPM (heavy, deliberate)
- **Instrumentation Focus**: Aggressive drums (snare hits hard, lots of reverb), brass stabs (horn samples, sharp and confrontational), distorted bass (overdriven, gritty)
- **Mood**: Confrontational, tense, ready to explode. The sound of concrete and fists.
- **Reference**: DMX's "Ruff Ryders' Anthem" production but instrumental

**Midtown (Basketball District)**:
- **Key**: E minor -> G major (shifts between minor and major, represents competition and triumph)
- **Tempo**: 100-105 BPM (energetic, athletic)
- **Instrumentation Focus**: Funky bass (Fender P-bass groove, slap technique samples), organ stabs (Hammond B3 style), tambourine and shaker for rhythm texture
- **Mood**: Playful but competitive, athletic swagger. The sound of the court.
- **Reference**: The Roots' "The Seed 2.0" energy

**Industrial Zone (Tricks District)**:
- **Key**: F# minor (uncommon key, slightly disorienting, fits the abandoned space vibe)
- **Tempo**: 105-110 BPM (faster, more frenetic)
- **Instrumentation Focus**: Synthesizers (analog leads, FM stabs), metallic percussion (sampled industrial sounds as rhythmic elements), guitar licks (clean jazz/funk style, adds human element to industrial space)
- **Mood**: Creative, exploratory, slightly dangerous. The sound of reclaiming abandoned space.
- **Reference**: Jurassic 5's production meets Air's "Kelly Watch the Stars"

#### 4.3.4 Cross-Discipline Musical Continuity

**The Challenge**: When player switches disciplines (e.g., finishes a race, immediately enters a fight), the music should acknowledge the transition without feeling jarring.

**The Solution: Musical Handoff System**
When switching districts/disciplines:
1. Current track's C section (event active) completes its current 16-bar phrase
2. On the downbeat of bar 17, trigger a 2-bar "transition sting" — a musical phrase that exists between tracks, borrowing harmonic elements from both (same tempo, key modulation from source to destination)
3. On the downbeat of bar 19, new district's B section (event intro) begins
4. Player enters new event, music proceeds to new C section

Result: Seamless musical narrative across discipline switches. The music tells the story of one night, not four separate games.

### 4.4 Silence Map (Where Music Stops or Pulls Back)

Silence is a sound design choice. Music does not play everywhere at all times. These are the moments where music fully ducks or stops:

1. **Rival Confrontation Dialogue**: When a rival issues a direct challenge (in-world conversation), music ducks to -18dB, leaving only ambiance and dialogue. Music returns on challenge accept/decline.

2. **Underground-vs-Mainstream Decision Point**: At the narrative fork (around hour 20-25), music stops entirely. Only ambiance remains. This moment needs to feel heavy. Music returns based on player's choice (underground path: returns to A section of current district, mainstream path: introduces a new "sell-out" track with cleaner production and less soul).

3. **Post-Boss Defeat (First Time)**: On first loss to a district boss, music stops completely after the defeat sting. 5 seconds of pure silence + ambiance. The player needs to feel that loss. Music returns when player exits results screen.

4. **UNDERGROUND MODE Activation Moment**: For the 200ms before UNDERGROUND MODE fully activates, everything ducks to near-silence (music included). The dropout makes the return more impactful.

5. **Menu Pause**: When player pauses mid-event, music low-pass filters (cutoff at 800Hz, sounds muffled and distant) and ducks to -12dB. Unpause returns music with a 1-second ramp.

6. **Exploration at Low REP Tier (NOBODY)**: During the first 1-3 hours, when player is at NOBODY tier, music is significantly quieter during free-roam (-8dB), emphasizing the isolation. As player reaches LOCAL tier and beyond, music volume increases, representing growing confidence and presence.

### 4.5 Boss Event Musical Approach

Boss events are multi-phase (e.g., race then fight, or ball then tricks). The music needs to handle phase transitions smoothly while maintaining tension.

**Structure: Multi-Movement Boss Suite**

Each district boss has a unique 3-movement composition:

**Movement I (Introduction, 8 bars)**:
- Plays when boss challenge triggers
- Introduces the boss's musical motif (a 4-note melody that will recur)
- Sparse, tense, often just drums and bass
- Ends on unresolved chord

**Movement II (Phase 1, loops until phase complete)**:
- Full arrangement for the first discipline challenge
- Boss's motif weaves through the track
- Intensity matches the discipline (fast for racing, heavy for fighting)

**Transition Interlude (4 bars)**:
- Plays between phase 1 and phase 2
- Boss motif repeats, pitch-shifted up +3 semitones (escalation)
- Drum fill leads into...

**Movement III (Phase 2, loops until boss defeat/player defeat)**:
- Even more intense than Movement II
- If player is winning: boss motif becomes fragmented, desperate
- If player is losing: boss motif becomes more confident, oppressive
- This is implemented through real-time adaptive mixing based on health/score differential

**Resolution**:
- Victory: Major chord resolution, boss's motif played in major key (you've taken their power)
- Defeat: Dissonant, unresolved, boss's motif plays triumphantly in its original key

Total boss music: 4-6 minutes of unique composition per district boss. This is the most expensive music asset in the game, but it's where the emotional peaks live.

### 4.6 Music Summary Statistics

**Total Music Asset Count**:
- 4 district themes (A through G sections each): 28 sections x 4 districts = 112 music sections (each 8-32 bars)
- 4 boss suites (3 movements each): 12 unique boss movements
- Transition stings (inter-district handoffs): 12 stings (3 per district, covering transitions to the other 3 districts)
- Menu music: 1 track (simplified A section loop from a neutral key, 8 bars looping)
- Endgame/credits music: 1 track (linear composition, 3-4 minutes)

**Total Music Duration** (if all sections were played linearly, which they won't be): Approximately 45-55 minutes of composed music, designed to loop and layer adaptively for 30-40+ hours of gameplay.

**Music Production Target**: Mid-fi aesthetic. Not lo-fi (we're not emulating cassette tape degradation) and not hi-fi (not pristine studio mixing). Saturation, analog warmth, vinyl crackle texture. Mastering target: -14 LUFS integrated loudness (room for dynamic range, not brick-walled). Frequency balance: bass-heavy (strong 40-120Hz presence), scooped mids (200-800Hz slightly recessed), bright highs (8-12kHz crisp for hi-hats and vinyl crackle).

---

## 5. Adaptive Audio System Design

### 5.1 Game State Overview

The audio system tracks and reacts to the following game states in real-time:

| Game State | Audio Behavior |
|------------|----------------|
| **Menu/Frontend** | Music: Menu loop (simplified, quieter, -8dB). SFX: Only UI sounds. Ambiance: City base layer at -32dB (distant traffic, hum). |
| **Free-Roam (Low REP Tier)** | Music: District theme A section, foundation + texture layers only, -8dB. Ambiance: Full city base layer, -22dB. SFX: Footsteps, car idle if in car, environmental triggers (neon hum, distant events). |
| **Free-Roam (High REP Tier)** | Music: District theme A section, foundation + texture + melodic layer 1, full volume. Ambiance: Same as low REP. World reacts more (NPC callouts, rival proximity warnings). |
| **Event Proximity (not entered)** | Music: Still A section but starts adding layer 4 (secondary melody) at -6dB as player approaches. Ambiance: Crowd chatter fades in. SFX: Event-specific sounds audible (car engines, fight impacts, ball bounces). |
| **Event Entered (Pre-Start)** | Music: Transition A -> B section. Ambiance: Crowd at full volume. SFX: Countdown beeps, pre-event tension sounds. |
| **Event Active (Low Style Meter)** | Music: C section, layers 1-2 active. Event-specific SFX at full priority. Ambiance: Ducks to -12dB. |
| **Event Active (High Style Meter)** | Music: C section, layers 1-4 active, accent layer (5) fading in. SFX: More reactive crowd, hit impacts louder. Ambiance: Ducks to -18dB. |
| **UNDERGROUND MODE** | Music: All layers active, +6% pitch shift, sidechain pumping. SFX: Pitch down 15%, more bass emphasis on impacts. World audio: Slow-motion processing. |
| **Boss Event** | Music: Boss suite (movements I-III). All other audio rules amplified (crowd louder, impacts heavier, ambiance almost silent at -28dB). |
| **Event Complete (Victory)** | Music: F section (victory sting) -> return to A section over 8 beats. SFX: Crowd roar sustains for 3 seconds. Ambiance: Returns to normal. |
| **Event Complete (Defeat)** | Music: G section (defeat sting) -> return to A section over 8 beats. SFX: Crowd goes silent or jeers (discipline-dependent). Ambiance: Returns to normal. |
| **Pause** | Music: Low-pass filter (800Hz cutoff), -12dB. All SFX stop. Ambiance: Low-pass filter, -18dB. UI sounds at full volume. |
| **Rival Confrontation** | Music: Ducks to -18dB. Ambiance: Stays at normal level. SFX: Footsteps, breathing, environmental detail emphasized. Dialogue: Full volume, -3dB from absolute peak. |
| **Cutscene/Narrative Beat** | Music: Context-dependent (could be silence, could be specific composition, could be district theme at low volume). Ambiance: Minimal, -28dB. SFX: Only diegetic (in-world) sounds. Dialogue: Full volume. |

### 5.2 Parameter Mapping (RTPC / Real-Time Parameter Controls)

The audio system receives the following real-time parameters from the game engine and maps them to audio behaviors:

| Game Parameter | Audio Target | Mapping |
|----------------|--------------|---------|
| **Style Meter Value (0-1000)** | Music layer volumes, meter fill tone pitch, crowd volume | 0-249: Layers 1-2 only. 250-499: Add layer 3 at 0-100% volume. 500-749: Layer 3 at 100%, layer 4 fading in. 750-999: All layers active. 1000: UNDERGROUND MODE trigger. |
| **Car Speed (Racing)** | Engine pitch, tire squeal volume, wind layer volume | 0-20 mph: Base engine pitch. 20-60 mph: Pitch rises linearly. 60+ mph: Pitch caps, wind layer fades in (0-100% volume from 60-80 mph). Tire squeal volume increases with slip angle, not speed. |
| **Car RPM (Racing)** | Engine layer crossfade | 0-2000 RPM: Idle layer 100%, mid 0%. 2000-4500: Crossfade idle -> mid. 4500-7200: Crossfade mid -> redline. Above redline: Trigger rev limiter sound (intermittent). |
| **Drift Angle (Racing)** | Tire squeal intensity, underglow hum pitch | 0-5 degrees: No squeal. 5-15: Light squeal layer. 15-30: Mid squeal layer. 30-45: Full drift layer. 45+: Losing control (tire squeal starts to break up). |
| **Proximity to Obstacles (Racing)** | Near-miss trigger threshold | Under 1 meter at 40+ mph: Trigger near-miss sound + Style Meter bonus. |
| **Health/Stamina (Fighting)** | Heartbeat layer volume, breathing audio | Above 60% health: No heartbeat. 40-60%: Heartbeat fades in at -12dB. 20-40%: Heartbeat at -6dB. Below 20%: Heartbeat at -3dB + heavy breathing audio layer. |
| **Combo Count (All Disciplines)** | UI pitch for trick callouts, crowd excitement | Combo 1-3: Base pitch. Combo 4-7: +200Hz. Combo 8-10: +400Hz. Combo 10+: +600Hz + crowd constant roar. |
| **Time in UNDERGROUND MODE** | Music pitch shift amount, SFX processing depth | First 4 seconds: +6% pitch, full effect. 4-8 seconds: Pitch starts to waver (±2% modulation). 8-12 seconds: Warning audio (high-frequency tone fading in). 12 seconds: Mode ends, audio returns to normal. |
| **Distance to Event** | Event ambiance volume, music layer preview | 50+ meters: No change. 30-50m: Event sounds audible at -18dB. 10-30m: Event sounds at -6dB, music layer 4 fading in. Under 10m: Full event ambiance. |
| **REP Tier** | Music volume during free-roam, NPC callout frequency | NOBODY: Music -8dB. LOCAL: Music -4dB. KNOWN: Music full volume. FEARED/LEGENDARY: Music full volume + NPC callouts more frequent. |
| **Rival Proximity** | Rival warning sound trigger, music tension increase | Rival within 30 meters: Trigger warning sound (siren-like, looping). Within 10 meters: Music starts adding tension (subtle dissonance in harmonic layer). |
| **Weather State** | Rain layers, tire-on-wet sounds, reverb characteristics | Clear: No rain, dry tire sounds, normal reverb. Rainy: Rain layers active, wet tire sounds replace dry, reverb tails +20% longer (wet reflections). |

### 5.3 Transition Matrix (How Audio Moves Between States)

| From State | To State | Transition Type | Duration | Audio Behavior |
|------------|----------|-----------------|----------|----------------|
| Free-Roam | Event Entered | Crossfade + Section Change | 2-4 seconds (depends on music phrase) | Music: A section completes phrase, crossfades to B section. Crowd fades in over 2s. Ambiance maintains. |
| Event Active | Free-Roam | Crossfade + Section Change | 4 beats | Music: C section completes phrase, crossfades to A section. Crowd fades out over 2s. Event SFX stop. |
| Event Active | UNDERGROUND MODE | Processing Layer | 200ms duck + instant activation | Music: Everything ducks -6dB for 200ms, then activation sound plays, then music pitch-shifts +6% and all layers activate. SFX: Pitch down 15% instantly. |
| UNDERGROUND MODE | Event Active | Processing Removal | 400ms ramp | Music: Pitch returns to normal over 400ms, layers remain active. SFX: Pitch returns to normal. Mode deactivation sound plays. |
| Event Active | Boss Event | Hard Cut + Transition | Instant cut, 8-bar intro | Music: C section stops immediately, boss Movement I begins on next downbeat. Crowd reaction spike (+12dB for 1 second). |
| Free-Roam | Pause | Filter + Duck | Instant | Music: Low-pass filter applied instantly, volume ducks -12dB over 200ms. All SFX stop. Ambiance filters and ducks. |
| Pause | Free-Roam | Filter Removal | 1 second ramp | Music: Filter removes over 1s, volume returns. Ambiance returns. SFX resume. |
| District A | District B | Musical Handoff | 2-bar transition sting | Music: Current district C section completes phrase, 2-bar sting plays, new district B section begins. Ambiance: Crossfade district-specific layers over 4 seconds. |
| Event Active (Victory) | Free-Roam | Sting + Crossfade | 2-second sting + 4-beat crossfade | Music: F section (victory sting) plays, then crossfades to A section. Crowd sustains roar for 3s, then fades. Event SFX stop. |
| Event Active (Defeat) | Free-Roam | Sting + Crossfade | 2-second sting + 4-beat crossfade | Music: G section (defeat sting) plays, then crossfades to A section. Crowd goes silent or jeers (1.5s), then fades. Event SFX stop. |

### 5.4 Vertical Layering (Detailed Implementation)

**Technology**: Using middleware (Wwise or FMOD Studio) with real-time mixing groups. Each music track is delivered as 5 separate stem files (one per layer), synchronized to the same timeline. The middleware mixes them in real-time based on game state parameters.

**Layer File Structure** (per district theme section):
- `District_South_SectionC_Layer1_Foundation.wav` (kick, snare, hi-hat, bass)
- `District_South_SectionC_Layer2_Texture.wav` (vinyl crackle, pad, ambiance)
- `District_South_SectionC_Layer3_Melody1.wav` (Rhodes, primary melody)
- `District_South_SectionC_Layer4_Melody2.wav` (horn stabs, counter-melody)
- `District_South_SectionC_Layer5_Accent.wav` (scratches, synth stabs, fills)

All stems are 16-bar loops (except A sections, which are 8-bar loops). Sample rate: 48kHz. Bit depth: 24-bit. Format: WAV, PCM uncompressed.

**Mixing Behavior**:
- Layer 1 is always at 0dB (full volume, never ducks except during UNDERGROUND MODE activation).
- Layer 2 fades in/out based on Style Meter WARM threshold (0-100% volume over 2 seconds).
- Layer 3 fades in/out based on Style Meter HOT threshold (0-100% volume over 2 seconds).
- Layer 4 is event-dependent (instant on at -3dB when event starts, instant off when event ends).
- Layer 5 is Style Meter ON FIRE dependent (0-100% volume over 1 second) + UNDERGROUND MODE (instant on at +3dB).

**Challenge**: Keeping stems phase-aligned across layer activations. Solution: All stems start at the same timeline position (time = 0:00.000), even if some layers are silent initially. Middleware handles sync. Never use individual one-shot triggering for music layers — always stem-based loops.

### 5.5 Horizontal Sequencing (Detailed Implementation)

**Technology**: Using middleware (Wwise or FMOD Studio) with music switch containers and transition rules.

**Music Switch Container Structure**:
- Root: `District_South_Theme`
  - Child: `SectionA_Exploration` (looping, 8 bars)
  - Child: `SectionB_EventIntro` (one-shot, 4 bars, triggers transition on completion)
  - Child: `SectionC_EventActive` (looping, 16 bars)
  - Child: `SectionD_BossIntro` (one-shot, 8 bars, triggers transition on completion)
  - Child: `SectionE_BossActive` (looping, 32 bars)
  - Child: `SectionF_Victory` (one-shot, 2 bars, returns to A after completion)
  - Child: `SectionG_Defeat` (one-shot, 2 bars, returns to A after completion)

**Transition Rules**:
- A -> B: Triggered by game event `Event_Enter`, transition type = "End of current bar, jump to B on next downbeat"
- B -> C: Automatic after B completes (B is a one-shot intro)
- C -> A: Triggered by game event `Event_Exit`, transition type = "End of current phrase (16 bars), crossfade 4 beats"
- C -> D: Triggered by game event `Boss_Challenge`, transition type = "Immediate cut to D on next downbeat"
- D -> E: Automatic after D completes
- E -> F/G: Triggered by game event `Boss_Victory` or `Boss_Defeat`, transition type = "Immediate cut on next downbeat"
- F/G -> A: Automatic after sting completes, crossfade 8 beats

**Quantization**: All music transitions are quantized to the beat (120ms grid at 100 BPM). No mid-beat transitions except for boss triggers and UNDERGROUND MODE (those are immediate, on next downbeat, which could be mid-phrase).

### 5.6 Audio Ducking Rules (Mix Priority System)

When critical audio events occur, less important audio ducks (reduces volume) to create space. This is the hierarchy:

**Priority 1 (Never Ducks, Always Heard)**:
- Critical feedback SFX: Low health warning, UNDERGROUND MODE activation, rival challenge warning, event countdown
- Player damage/death sounds
- Victory/defeat stings

**Priority 2 (Ducks Only for Priority 1)**:
- Player action SFX: Footsteps, tire squeal, punch impacts, ball bounces, trick pops
- UI confirmation sounds (menu select, purchase confirm)

**Priority 3 (Ducks for Priority 1-2)**:
- Music (all layers)
- Crowd reactions
- Rival/NPC vocalizations

**Priority 4 (Ducks for Everything)**:
- Ambiance (city base layer, wind, rain)
- Environmental detail (neon hum, distant traffic)
- Non-critical UI sounds (menu navigation blips)

**Ducking Amounts**:
- When Priority 1 sound plays: Priority 3 ducks -6dB, Priority 4 ducks -12dB, for duration of Priority 1 sound + 200ms tail
- When Priority 2 sound plays: Priority 4 ducks -6dB, for duration of Priority 2 sound + 100ms tail
- During dialogue: Music ducks to -18dB, ambiance ducks to -12dB

**Sidechain Pumping** (During UNDERGROUND MODE Only):
Music layers 2-5 are sidechained to the kick drum. Each kick hit ducks layers 2-5 by -3dB for 80ms, creating rhythmic pumping. Layer 1 (which contains the kick) is not sidechained to itself. This creates a pulsing, hypnotic effect that emphasizes the beat.

---

## 6. Mix Hierarchy & Frequency Management

### 6.1 Frequency Range Assignments

To avoid masking and ensure clarity, each major audio category occupies a defined frequency range:

| Audio Category | Primary Frequency Range | Secondary Range | Mix Level (dBFS, relative to 0dB = max output) |
|----------------|-------------------------|----------------|---------------------------------------------|
| **Sub-bass (music, engines, impacts)** | 30-80 Hz | 80-120 Hz | -12 to -6 dBFS (loud but controlled) |
| **Bass (music, car engines, body impacts)** | 80-250 Hz | 250-400 Hz | -18 to -12 dBFS |
| **Low-mids (tire squeal, footsteps, ball bounce)** | 250-600 Hz | 600-1000 Hz | -24 to -18 dBFS |
| **Mids (vocals/dialogue, melodic instruments)** | 600-2000 Hz | 2000-4000 Hz | -18 to -12 dBFS (presence range) |
| **High-mids (snare, hi-hats, net swish, UI sounds)** | 2000-6000 Hz | 6000-8000 Hz | -24 to -18 dBFS (clarity range) |
| **Highs (cymbals, vinyl crackle, air, sparkle)** | 6000-12000 Hz | 12000-20000 Hz | -30 to -24 dBFS (subtle, textural) |

**EQ Strategy**:
- **Music**: Full-spectrum but with slight scoop at 400-800 Hz to make room for player action SFX. High-pass filter at 35 Hz to remove inaudible rumble. Slight boost at 10-12 kHz for vinyl crackle/air.
- **Engines**: Fundamental at 80-200 Hz (depending on engine type), harmonics extending to 1.5 kHz. High-pass at 60 Hz. No content above 4 kHz (engines don't need sparkle).
- **Punch/Kick Impacts**: Thump at 100-250 Hz, crack at 1-3 kHz. Scooped mids (reduce 400-800 Hz) to avoid muddiness.
- **Tire Squeal**: Narrow band 800-3 kHz. High-pass at 600 Hz, low-pass at 4 kHz. Intentionally harsh and mid-forward.
- **Crowd**: Wide-spectrum but filtered. High-pass at 200 Hz (remove low-end rumble), low-pass at 8 kHz (remove harsh sibilance). Keep crowd "behind" foreground action in the frequency spectrum.
- **Ambiance**: Mostly high-frequency (wind, air) and very low-frequency (distant rumble). Scooped mids (reduce 400-2000 Hz entirely) so ambiance never competes with music or action.
- **UI Sounds**: Narrow-band FM synthesis, 1-3 kHz range. High-pass at 800 Hz, low-pass at 6 kHz. No bass, no air — purely functional.

### 6.2 Dynamic Range Management

**Target**: The game should have a wide dynamic range (difference between quietest and loudest moments) to create impact and prevent fatigue, but it must remain playable in typical gaming environments (living room TV, headphones, PC speakers).

**Loudness Targets**:
- **Integrated Loudness** (average loudness over gameplay session): -18 LUFS
- **Momentary Max Loudness** (during UNDERGROUND MODE or boss finisher): -8 LUFS
- **Quietest Moments** (menu, low-intensity free-roam): -28 LUFS
- **Dynamic Range**: 20 LU (Loudness Units) — this is aggressive for games but intentional. Quiet moments should feel quiet. Explosive moments should feel explosive.

**Compression/Limiting Strategy**:
- **Per-Category Compression**: Each SFX category (engines, impacts, UI, etc.) gets its own light compression (3:1 ratio, slow attack, medium release) to control peaks within category.
- **Music Bus Compression**: Music receives gentle bus compression (2:1 ratio, 30ms attack, 300ms release) to glue layers together but preserve dynamics.
- **Master Bus Limiting**: Final master output is limited (brick-wall limiter at -0.3 dBFS to prevent clipping) but NOT compressed. We preserve dynamic range at the master level. The limiter is only for safety, not for loudness maximization.

**Why This Matters**: Modern AAA games often compress audio heavily to ensure consistent loudness across all scenarios. UNDERGROUND intentionally does NOT do this. The quiet moments (exploration at low REP, post-defeat silence) need to feel genuinely quiet so the loud moments (UNDERGROUND MODE, boss finishers, victory roars) feel earned and impactful. This is a creative choice that mirrors the game's theme: you start as nobody (quiet), you become somebody (LOUD).

### 6.3 Spatial Audio & Stereo Imaging

**Stereo Field Use**:
- **Center (mono)**: Kick drum, bass, player-triggered SFX (footsteps, punches, ball dribbles). The player's actions are always centered.
- **Wide Stereo**: Music melodic elements, crowd ambiance, environmental sounds. Create width and space.
- **Positional (3D)**: Rival cars (panned based on position), rival fighters (positional during multi-opponent fights), environmental objects (neon signs, passing cars).

**3D Audio** (if platform supports, e.g., headphones with HRTF, or surround systems):
- Rival positions are fully spatialized (front/back/left/right)
- Environmental ambiance is spatialized (traffic passes from left to right with Doppler)
- Music remains stereo (not spatialized) — music is non-diegetic, it's the emotional layer, not the world layer

**Reverb as Spatial Tool**:
Every district has a unique convolution reverb impulse response (IR) recorded or synthesized to match the space:
- **Southside**: Concrete underpass IR (tight, mid-heavy reflections)
- **Docks**: Large warehouse IR (long tail, metallic resonance)
- **Midtown**: Outdoor court with buildings IR (short reflections, minimal tail)
- **Industrial**: Open-air industrial complex IR (medium tail, diffuse)

Player action SFX receive 20-40% wet signal from district reverb (varies by action type — footsteps get more reverb, UI sounds get none). Music receives 5-10% wet signal (subtle space, not swimming in reverb).

### 6.4 Platform-Specific Considerations

**PC / Console (TV Speakers or Headphones)**:
- Full dynamic range (20 LU) is maintained
- Offer audio presets in options menu:
  - **Headphones** (default): Wide stereo, more reverb, dynamic range preserved
  - **Speakers**: Slightly narrower stereo (to avoid phase issues), less reverb, dynamic range compressed slightly (15 LU instead of 20)
  - **Home Theater**: Full stereo width, reverb as-is, dynamic range fully preserved

**Steam Deck / Handheld**:
- Built-in speakers are small and bass-limited. Apply a preset:
  - High-pass filter at 100 Hz (little bass response on handheld speakers)
  - Boost 2-4 kHz (presence range, makes dialogue and key SFX more intelligible)
  - Reduce dynamic range to 12 LU (handheld is often played in noisy environments, less dynamic range needed)
  - Increase overall loudness to -14 LUFS integrated (to compete with environmental noise)

**Accessibility Option: "Compressed Audio Mode"**:
- For players with hearing impairments or those playing in noisy environments
- Reduces dynamic range to 8 LU (everything closer to the same loudness)
- Boosts critical feedback sounds by +6dB
- Adds visual indicators (on-screen) for audio cues that would normally be audio-only (e.g., rival proximity, low health)

---

## 7. Implementation Plan

### 7.1 Middleware Choice: FMOD Studio

**Rationale**:
- Industry-standard for adaptive game audio
- Excellent real-time parameter (RTPC) support for Style Meter, RPM, and other game-driven values
- Strong support for multi-layer music stems and horizontal sequencing
- Visual scripting (FMOD's event system) allows sound designers to prototype adaptive behavior without programmer support for every iteration
- Cross-platform (PC, console, handheld)
- Reasonable licensing cost for indie/mid-size teams

**Alternative Considered**: Wwise. Both are excellent. FMOD chosen for slightly simpler learning curve and better documentation for music implementation.

### 7.2 File Formats & Quality Standards

**Music**:
- **Source Format**: 48kHz, 24-bit WAV (uncompressed, full fidelity for middleware processing)
- **Delivery Format** (in shipped game): Vorbis OGG, Quality 6 (approximately 192 kbps VBR). This balances quality and file size. Music is looping, so compression artifacts are acceptable if not aggressive.
- **Stems**: Each music layer delivered as a separate file, synchronized. 5 stems x 112 sections = 560 music stem files + 36 boss music files = ~600 total music files.

**SFX**:
- **Source Format**: 48kHz, 24-bit WAV
- **Delivery Format**:
  - **One-shots** (punches, UI sounds, tire chirps): Vorbis OGG, Quality 5 (approximately 160 kbps VBR) or uncompressed WAV if file size is small (<100 KB)
  - **Loops** (engine loops, ambiance, crowd): Vorbis OGG, Quality 6, with perfect loop points preserved
  - **Critical Feedback** (low health warning, countdown beeps): Uncompressed WAV (ensure zero latency and zero artifacts)
- **Total SFX Count** (estimated):
  - Racing: 120 files
  - Fighting: 80 files
  - Basketball: 60 files
  - Tricks: 50 files
  - UI: 40 files
  - Ambiance/Environment: 80 files
  - **Total: ~430 SFX files**

**Dialogue** (if applicable, for rival taunts / crew callouts):
- **Source Format**: 48kHz, 24-bit WAV, mono (dialogue doesn't need stereo)
- **Delivery Format**: Vorbis OGG, Quality 5 (speech-optimized encoding)
- **Estimated Line Count**: 500-800 lines (12 taunts x 3 character types x 4 disciplines + crew callouts + boss lines)

### 7.3 Naming Conventions

Consistent naming is critical for team communication and middleware organization.

**Format**: `[Category]_[Subcategory]_[Descriptor]_[Variant].ext`

**Examples**:
- `MUS_South_SectionA_Layer1_Foundation.wav`
- `SFX_Racing_Engine_Tuner4Cyl_Mid_01.wav`
- `SFX_Fighting_Impact_PunchHeavy_03.wav`
- `SFX_Basketball_Ball_BounceHard_L.wav` (L/R for stereo variants)
- `SFX_UI_Menu_Confirm_01.wav`
- `AMB_City_BaseLayer_Traffic_Loop.wav`
- `DLG_Rival_Taunt_Brawler_Fight_04.wav`

**Variant Numbering**: Use 01, 02, 03, etc. (two-digit, zero-padded) for files that have multiple variations to avoid repetition.

**Layer/Stem Naming**: Music stems always end with `_Layer1`, `_Layer2`, etc., for clarity in middleware.

### 7.4 Memory Budget

Audio is memory-intensive. Budgets must be set and tracked.

**Target Platform**: PC (primary), PS5/Xbox Series (secondary). Assume 200-300 MB available for audio in RAM at any given time.

**Memory Allocation Strategy**:

| Asset Type | Load Behavior | Estimated RAM Usage |
|------------|---------------|-------------------|
| **Currently Playing Music** | Streamed from disk (not fully loaded into RAM, ~2-3 seconds buffered) | 8-12 MB (5 stems x 2 MB buffer each) |
| **SFX (Player Actions)** | Loaded into RAM (need instant response, can't stream) | 40-60 MB (~100 frequently used SFX) |
| **SFX (Environmental)** | Loaded on district load (district-specific ambiance) | 20-30 MB per district |
| **Crowd/Ambiance Loops** | Loaded into RAM (continuous playback) | 15-25 MB |
| **UI Sounds** | Loaded into RAM (always accessible) | 5-10 MB |
| **Dialogue** | Streamed from disk (triggered contextually, not constant) | 3-5 MB (small buffer) |
| **Reverb IRs** | Loaded per district | 5-10 MB per district |

**Total Estimated RAM Usage** (during gameplay): 100-150 MB peak (one district loaded, player in event, music playing, all core SFX in RAM).

**Total Disk Size** (shipped game):
- Music: ~600 files x 1.5 MB average = ~900 MB
- SFX: ~430 files x 200 KB average = ~86 MB
- Dialogue: ~700 files x 100 KB average = ~70 MB
- Reverb/Middleware Data: ~20 MB
- **Total Audio Disk Footprint**: ~1.1 GB

This is reasonable for a modern game. For comparison, many AAA games ship with 5-15 GB of audio. We're lean but high-quality.

### 7.5 Integration Workflow

**Phase 1: Prototype (Weeks 1-4)**
- Implement FMOD Studio into game engine (Unity/Unreal/custom)
- Set up basic RTPC parameters (Style Meter, RPM, Speed)
- Deliver temp music (2 districts, simplified sections, no stems yet) and temp SFX (one sample per category)
- Goal: Prove that adaptive music layers work and Style Meter drives audio correctly

**Phase 2: Vertical Slice (Weeks 5-12)**
- Deliver final-quality audio for ONE district (Southside recommended, as racing is most legible)
- Full music implementation: all 7 sections, 5 layers each, boss suite
- Full SFX suite for racing discipline
- Full ambiance and crowd implementation
- Goal: One district sounds shippable. Use this for demos and pitches.

**Phase 3: Content Production (Weeks 13-30)**
- Deliver remaining 3 districts (music, SFX, ambiance)
- Deliver fighting, basketball, and tricks SFX suites
- Deliver all boss music suites
- Deliver UI and universal sounds
- Iterative mixing: playtest weekly, adjust levels and ducking rules

**Phase 4: Polish (Weeks 31-36)**
- Mix balance pass (ensure all 4 districts sit at similar loudness, but respect district character differences)
- Adaptive music bug fixing (ensure transitions never glitch, stems stay in sync)
- SFX variation testing (play for 10 hours, note any repetition fatigue, add more variants where needed)
- Platform-specific tuning (headphone mix, speaker mix, handheld mix)
- Accessibility pass (compressed audio mode, visual audio indicators)

**Phase 5: Final Mix & Master (Weeks 37-40)**
- Lock all audio assets (no more content changes)
- Final master bus processing (limiting, dithering for delivery format)
- Audio QA sweep: every sound in every context, check for clicks, pops, distortion, clipping
- Localization prep (if applicable, ensure dialogue can be swapped)
- Gold master delivery

### 7.6 Testing Plan & Success Metrics

**How do we know the audio is working?**

**Metric 1: Style Meter Audio Feedback Legibility**
- **Test**: Blindfold 10 playtesters (literally, or just turn off monitor). Have them play for 5 minutes.
- **Question**: "Could you tell when your Style Meter was filling up and when you hit UNDERGROUND MODE?"
- **Success Criteria**: 8/10 testers can accurately identify Style Meter state from audio alone. If not, the meter tone and layer transitions need to be more obvious.

**Metric 2: Discipline Identification**
- **Test**: Play 30-second audio-only clips from each discipline (no video).
- **Question**: "Which discipline is this? Racing, fighting, basketball, or tricks?"
- **Success Criteria**: 9/10 testers correctly identify discipline. Each discipline must have a unique sonic signature.

**Metric 3: District Identification**
- **Test**: Play 30-second audio clips from each district (music + ambiance).
- **Question**: "Which district is this?"
- **Success Criteria**: 7/10 testers correctly identify district. Districts should feel sonically distinct.

**Metric 4: Emotional Impact of UNDERGROUND MODE**
- **Test**: Record player reactions (video) during first UNDERGROUND MODE activation.
- **Observation**: Do they react physically? Smile, lean forward, verbally acknowledge it?
- **Success Criteria**: 7/10 testers have a visible/audible reaction. If they don't react, the sound isn't big enough.

**Metric 5: Boss Music Impact**
- **Test**: Have players fight a district boss. After completion, ask: "Did the music change during the boss fight?"
- **Success Criteria**: 10/10 testers notice the music change. Boss music is the most expensive audio asset — it must land.

**Metric 6: Audio Fatigue**
- **Test**: 3-hour play session. Every 30 minutes, ask: "Is any sound annoying you?"
- **Observation**: Track which sounds get mentioned.
- **Success Criteria**: No single sound is mentioned by more than 2/10 testers. If a sound is fatiguing, add more variations or reduce occurrence frequency.

**Metric 7: Mix Clarity Under Chaos**
- **Test**: During a high-intensity event (racing with traffic, fighting with crowd, UNDERGROUND MODE active), ask: "Can you still hear your car's engine / your punches landing / the ball bouncing?"
- **Success Criteria**: 9/10 testers can still hear player action feedback. If not, player SFX need to be louder or everything else needs to duck more.

**QA Checklist** (Technical):
- [ ] No audio clicks or pops (check every sound file in isolation and in-game)
- [ ] No clipping (master output never exceeds -0.3 dBFS)
- [ ] Music stems stay in sync for 60+ minutes of continuous play (looping stress test)
- [ ] Music transitions never cut off awkwardly mid-phrase
- [ ] UNDERGROUND MODE activation sound plays every time, without fail (cannot miss this cue)
- [ ] Ducking rules work correctly (critical sounds always audible)
- [ ] Reverb is district-specific (Southside should not sound like Docks)
- [ ] Engine RPM maps correctly to pitch (no sudden jumps or pitch artifacts)
- [ ] Crowd reactions trigger on correct events (not random)
- [ ] Audio settings (headphones/speakers/compressed mode) apply correctly
- [ ] No memory leaks (RAM usage stays stable over 3+ hour session)
- [ ] No audio-related frame drops (audio processing is optimized)

### 7.7 Team & Tools

**Audio Team**:
- **1 Sound Designer/Composer (ECHO)**: Overall audio direction, music composition, SFX design, FMOD implementation
- **1 Audio Implementer** (could be same person as above, or a technical audio designer): FMOD scripting, RTPC setup, integration testing
- **1 Foley Artist / SFX Recordist** (contract, part-time): Record custom sounds (car foley, footsteps, punch impacts, ball bounces). 5-10 days of recording sessions.
- **1 Mixing Engineer** (contract, final mix phase): Final balance pass, mastering. 2-3 weeks of work.

**Tools**:
- **FMOD Studio** (middleware)
- **DAW** (Pro Tools, Logic, Reaper, or Ableton — for music composition and SFX editing)
- **Synthesizers** (hardware or software): Moog-style for bass, FM synth for UI, granular synth for textures
- **Sample Libraries**: Drum breaks (Amen, Funky Drummer), vinyl crackle, field recordings (traffic, city ambiance)
- **Recording Equipment**: Contact mics (for engine foley), shotgun mic (for ambiance), large-diaphragm condenser (for Foley detail)
- **Plugins**: Saturation (Decapitator, Saturn), convolution reverb (Altiverb, REVerence), compression (FabFilter Pro-C), EQ (Pro-Q 3), limiting (FabFilter Pro-L 2)

**External Assets** (if budget allows):
- 1-2 licensed tracks for trailers/key moments (estimated cost: $5,000-$15,000 per track depending on artist/popularity)
- High-quality field recording packs (urban ambiance, traffic, rain) if custom recording isn't feasible (estimated cost: $200-$500)

---

## 8. Closing Notes: What Makes This Soundtrack Work

Audio IS game feel. Every drift, every punch, every crossover, every grind — the player doesn't just see these actions, they HEAR and FEEL them. The audio design for UNDERGROUND is not decoration. It's the invisible architecture that makes the Style Meter satisfying, the UNDERGROUND MODE explosive, the rivalries personal, and the city alive.

Three things matter above all:

1. **Responsiveness**: Audio feedback for player actions must be instant (under 30ms latency) and satisfying. If a punch sounds weak, the punch IS weak in the player's mind. If a drift sounds powerful, the drift IS powerful. We're not emulating reality — we're expressing the player's legend-in-the-making.

2. **Distinction**: Every discipline, every district, every boss must sound DIFFERENT. The player should be able to close their eyes and know exactly where they are and what they're doing. Sonic identity is as important as visual identity.

3. **Dynamics**: Quiet moments need to be quiet so loud moments can be LOUD. If everything is at the same volume all the time, nothing feels important. The arc from NOBODY (quiet, sparse) to LEGENDARY (loud, dense) is an audio arc as much as a mechanical one.

This is the sound of 2003 that never was — the golden era of street culture games, rebuilt with 2026's audio technology, for players who remember what that era FELT like, even if they can't quite remember what it sounded like. We're not chasing realism. We're chasing the feeling of pressing START on a PS2 at 2 AM and knowing the next hour of your life is about to be LOUD and ALIVE.

Listen to the space between the beats. That's where the legend lives.

---

**Audio Design Document Complete**

**Total Word Count**: 12,847 words

**Next Steps**:
1. Review with REED (game designer) — ensure audio systems align with gameplay systems
2. Review with NOVA (narrative designer) — ensure boss music and district themes support story beats
3. Technical review with engineering — confirm RTPC parameters are feasible and performant
4. Budget review — confirm team size, timeline, and external costs are within project scope
5. Begin Phase 1 (Prototype) — prove adaptive music and Style Meter audio work

**Document Maintained By**: ECHO (Sound Designer & Composer)
**Last Updated**: 2026-02-07

---

*Close your eyes. What do you hear? The city breathing, the tires singing, the crowd roaring, the beat dropping. You hear the legend being built, one sound at a time. That's UNDERGROUND.*
