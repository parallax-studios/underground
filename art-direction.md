# UNDERGROUND — Art Direction Document

**Art Director**: PIXEL
**Status**: Complete — Ready for Asset Production
**Version**: 1.0
**Date**: 2026-02-07

---

## 1. Visual Identity Statement

**UNDERGROUND looks like a PS2 fever dream shot through a CRT — neon-soaked, chrome-dripping, scan-line-bleeding street culture from 2003 that never forgot where it came from, rendered with modern precision but vintage soul.**

This is the game's visual promise: you are looking at an artifact from the golden age of street culture games, unearthed and enhanced but never sanitized. Every pixel screams "this is what the underground looked like when it was still underground." The art is not nostalgic decoration — it is the game's identity, its first line of defense against being mistaken for anything safe or polished.

---

## 2. Visual Feeling

### Emotion
**HUNGER AND ELECTRICITY**. The screen should feel like standing outside a nightclub at 1 AM, waiting for your name to be called. Anticipation. The hum of bass through brick walls. The knowledge that tonight, you could become someone. Every frame carries the voltage of potential energy about to discharge.

The player should feel simultaneously small (the city is vast, indifferent, alive without you) and charged (you have agency, you can make noise, you can light up a block). This emotional duality drives the art: environments are big and imposing, but lighting and composition always carve out space for the player to shine.

### Temperature
**COLD NIGHTS, HOT LIGHTS**. The base temperature is cool — the city is concrete, asphalt, glass, steel, rain-slicked surfaces reflecting artificial light. This is not a warm world. But puncturing that cold are islands of heat: neon signs bleeding orange and magenta, car headlights cutting white-hot through fog, underglow kits painting blue and green trails on wet ground, floodlights over streetball courts casting harsh yellow cones.

The contrast is essential. If everything glows, nothing does. The city is cold so that the moments of heat — a drift trail igniting behind your car, the slow-mo flash of a perfect crossover, the crowd's lighter-flames during a fight — feel like they matter. Light in UNDERGROUND is earned. It marks presence.

### Era
**2000-2005, LOCKED IN AMBER**. Not vaguely retro. Not "inspired by the 2000s." This game looks like it shipped in 2003 and was frozen in carbonite. We are making the game that Electronic Arts, Rockstar, and EA Big wanted to make but couldn't because of hardware limits, publisher fear, or the fact that they were making three separate games instead of one unified vision.

Visual markers of the era:
- **CRT color bleed and scan lines** — always active, not a post-process filter you can disable. This is the native output.
- **Chunky UI chrome** — beveled edges, gradients that scream "Photoshop 7.0 with the default layer styles." Buttons look like they have depth you could press with your thumb.
- **Mixtape culture typography** — Sharpie-on-CD-R titles. Bootleg energy. Hand-drawn flavor text. Nothing is typeset in Helvetica.
- **Low-poly with high-fidelity texture** — PS2/Xbox-era polycount (characters: 3,000-6,000 tris, cars: 8,000-12,000 tris, environments: aggressive LOD), but textures are sharp and authored with intent, not dithered and washed out. We know what we're doing. The low-poly is a choice, not a limitation.
- **Fashion frozen at Y2K** — Baggy jeans. Tall tees. Timbs, Air Force 1s, Jordans. Fitted caps. Chain wallets. Wristbands. Von Dutch hats if we're being truly authentic (we are). The player character should look like they stepped out of a music video from "In Da Club" era 50 Cent, early Kanye, Missy Elliott, or Pharrell.

This is not parody. This is reverence. The era was peak visual identity for street culture, and we are bottling it.

### Visual Intensity Curve
The art should breathe with the gameplay. At rest (exploring the city, low Style Meter), the palette is muted, the camera is steady, the post-processing is subtle. As the player builds style, the world responds:

- **COLD (0-249 Style)**: Desaturated by 15%. Scan lines at 30% opacity. Underglow dim. The city does not care about you yet.
- **WARM (250-499 Style)**: Full saturation returns. Light bloom increases 20%. Crowd animations intensify. NPCs turn to watch.
- **HOT (500-749 Style)**: Color saturation +10% over baseline. Chromatic aberration at corners of screen. Motion blur on fast actions. The world is bending toward you.
- **ON FIRE (750-999 Style)**: Color saturation +25%. Film grain overlay intensifies. Vignette tightens. Light sources flare. Bass frequencies boost in the audio-visual link. Reality is straining.
- **UNDERGROUND MODE (1000 Style)**: CRT OVERLOAD. Full chromatic aberration, scan lines pulse, colors invert for single frames, time dilation visible in frame-stepping motion blur. For 12 seconds, the game looks like the CRT is about to explode. This is the visual climax, and it should feel dangerous to the screen itself.

---

## 3. Color Palette

### Primary Palette (The Foundation)

These five colors are the bones of UNDERGROUND. Every major environment block, every UI panel, every character model starts here.

| Color Name | Hex Value | RGB | Usage | Rule |
|------------|-----------|-----|-------|------|
| **ASPHALT BLACK** | `#0D0D12` | (13, 13, 18) | Backgrounds, shadows, skyboxes at night, UI panel bases, car base coat (matte black option) | This is not pure black (`#000000`). It has a hint of blue to it, keeping the temperature cool. Use this for 40-50% of screen real estate in any given frame. The city is made of this. |
| **CONCRETE GRAY** | `#3A3D47` | (58, 61, 71) | Roads, buildings, sidewalks, structural elements, UI borders, secondary text | The second-most common color on screen. Slightly blue-tinted like real concrete in sodium vapor light. This is the city's flesh. |
| **STEEL BLUE** | `#5C6B7D` | (92, 107, 125) | Metal surfaces, car bodies (stock), chain-link fences, distant buildings, deactivated UI elements | This is the "default car" color and the color of fences, garage doors, and infrastructure. Cold, industrial, waiting to be customized into something that pops. |
| **RUST ORANGE** | `#D9622E` | (217, 98, 46) | Construction barriers, danger markers, heat vents, distant neon signs, warning UI elements | The city's decay. Also the color of streetlights reflected in rain. Warm accent in a cold world. Use sparingly — this is the "heat source" color in environments. |
| **MIDNIGHT PURPLE** | `#1F1833` | (31, 24, 51) | Deep shadows, night sky gradient (top of skybox), underground interiors, "prestige" UI elements | Darker than Asphalt Black but with purple warmth. This is the color of the "underground" itself — the literal darkness where the culture thrives. |

### Accent Palette (The Signature)

These are the neon veins running through the city. Every car, every character, every event pumps one or two of these into the world.

| Color Name | Hex Value | RGB | Usage | Rule |
|------------|-----------|-----|-------|------|
| **UNDERGLOW CYAN** | `#00E5FF` | (0, 229, 255) | Car underglow kits, electric effects, Style Meter fill, "cool" trick trails, ice-blue UI highlights | The game's signature color. If UNDERGROUND has a "brand color," this is it. High-saturation cyan with green hints. This is the color of speed, electricity, and flow. When the player is in the zone, this color dominates. |
| **NITRO ORANGE** | `#FF6600` | (255, 102, 0) | Nitrous trails, fire effects, "hot" trick trails, danger warnings, explosive impacts, Style Meter at ON FIRE tier | The counterpoint to cyan. Pure energy, unsubtle, aggressive. This is the color of combustion and risk. Use for moments that demand attention. |
| **NEON MAGENTA** | `#FF00AA` | (255, 0, 170) | Club signs, character highlight (player focus), rival nameplates, S-rank performance feedback, "legendary" tier UI | The color of fame. When you've arrived, when you're the center of attention, magenta marks you. Also the color of rival bosses and high-stakes events. |
| **ACID GREEN** | `#39FF14` | (57, 255, 20) | Lime underglow option, toxic/danger zones, "go" signals, positive feedback (perfect timing), health/stamina when full | Radioactive, unnatural, impossible to ignore. Use for feedback that says "YES" or "DANGER" depending on context. This color does not exist in nature — it exists in the underground. |
| **GOLD CHROME** | `#FFD700` | (255, 215, 0) | Victory highlights, currency indicators, legendary item glow, first-place finish, S-rank stamps | Reserved for success states. This is the color of the trophy, the payoff. Do not use casually. When gold appears, something significant has happened. |

### UI Palette (The Interface)

The UI is its own world — a flip phone OS meets a modded car dashboard meets a mixtape CD label.

| Element | Primary Color | Secondary Color | Hover/Active State | Disabled State | Notes |
|---------|--------------|-----------------|-------------------|----------------|-------|
| **Menu Backgrounds** | `#0D0D12` (Asphalt Black) at 85% opacity | `#1F1833` (Midnight Purple) gradient | N/A | N/A | Slight blur behind menus (2px Gaussian) to separate from 3D world. Scan lines at 40% opacity always visible. |
| **Button Default** | `#3A3D47` (Concrete Gray) | `#5C6B7D` (Steel Blue) border (3px) | `#00E5FF` (Underglow Cyan) border, inner glow | `#0D0D12` (Asphalt Black) with 50% opacity | Beveled appearance: top edge lighter (+20 brightness), bottom edge darker (-20 brightness). Chunky 2000s Photoshop energy. |
| **Button Active/Selected** | `#00E5FF` (Underglow Cyan) fill at 30% opacity | `#00E5FF` full brightness border (4px) | Pulsing glow (1-second loop) | N/A | The selected button GLOWS. No subtlety. |
| **Primary Text** | `#FFFFFF` (Pure White) | N/A | `#00E5FF` when hovering interactive text | `#5C6B7D` (Steel Blue) | Font: Bold, condensed, sans-serif. High contrast always. Drop shadow: 2px offset, 80% black. Every line of text is readable even against noisy backgrounds. |
| **Secondary Text** | `#C4C7CC` (Off-white gray) | N/A | N/A | `#5C6B7D` (Steel Blue) | Flavor text, descriptions, lore. Slightly less aggressive than primary. |
| **Currency (CASH)** | `#FFD700` (Gold Chrome) | N/A | Glows on increase | N/A | Always visible in top-right HUD. Icon: dollar sign in stacked bills style. |
| **Reputation (REP)** | `#FF00AA` (Neon Magenta) | N/A | Glows on increase, pulsing effect | N/A | Always visible in top-right HUD. Icon: star with motion lines. |
| **Health/Stamina Bars** | `#39FF14` (Acid Green) when full | `#FF6600` (Nitro Orange) when low (<30%) | Flashing red at critical (<10%) | N/A | Gradient fill: green to yellow to orange to red as it depletes. Chunky bar with black border (2px). |
| **Style Meter** | Gradient: `#00E5FF` (Cyan) -> `#FFD700` (Gold) -> `#FF6600` (Orange) -> `#FF00AA` (Magenta) at max | N/A | Pulses at tier thresholds | N/A | Vertical bar, screen-left, styled as a neon tube sign. Glows intensely. At UNDERGROUND MODE, strobes white. |
| **Notification Pop-ups** | `#1F1833` (Midnight Purple) at 90% opacity | `#00E5FF` or `#FF6600` border depending on message type (info vs. warning) | Slide-in from right, 3-second display, fade out | N/A | Compact, corner-screen. Text brief and punchy. Sound cue always accompanies. |
| **Rival Nameplates (in-world)** | `#FF00AA` (Neon Magenta) for rivals, `#FFD700` (Gold) for bosses | `#0D0D12` (Asphalt Black) background pill shape | Glows when rival is locked as target | N/A | Floats above rival's head during events. Includes rival name + mood icon (grin, scowl, respect hand). |

### Color Rules and Restrictions

1. **The 60-30-10 rule, remixed**: In any frame, aim for 60% dark base (Asphalt Black, Concrete Gray), 30% mid-tones (Steel Blue, environment detail), 10% accent neon (Cyan, Orange, Magenta). This ensures the neon pops instead of washing out.

2. **Neon never touches neon**: Cyan underglow never appears next to Magenta signs next to Acid Green hazards in the same composition. Space neon colors apart. Each light source should have breathing room. If two neon colors must coexist in a shot, separate them with at least 30% of frame width or a dark element between them.

3. **Underglow is player-controlled**: The player picks their car's underglow color in the garage (Cyan, Orange, Magenta, Green, or off). This is the player's signature. NPCs and rivals have fixed underglow tied to their personality (the rival database assigns this). The city itself uses Cyan and Orange for environmental neon.

4. **UI never fights the game**: When the 3D world is full of Cyan (player drifting, Style Meter high, underglow blazing), the UI pulls back — borders dim to Steel Blue. When the world is dark (exploring, low style), the UI can be more assertive with Cyan highlights. The UI and game world are in constant negotiation for attentional dominance, and gameplay always wins.

5. **Colorblind accessibility without compromise**: Critical gameplay information (danger, interaction, success/failure) is never communicated by color alone. Danger zones have animated warning chevrons + color. Interact prompts have icons + color. Success feedback has screen shake + sound + color. The game is designed for protanopia, deuteranopia, and tritanopia from the ground up, but we do not desaturate the palette to achieve it. Neon stays neon.

6. **White is reserved for the player and critical feedback**: Pure white (`#FFFFFF`) is used for player character highlights (rim light), text, and moments of peak success (S-rank stamps, UNDERGROUND MODE flash frames). NPCs do not get white rim lights. Rivals get Magenta or their signature underglow color. White means "this is you" or "this is essential info."

---

## 4. Shape Language

### Dominant Shapes

**ANGULAR MEETS AERODYNAMIC**. The city is a grid of rectangles — buildings, blocks, chain-link fences, basketball courts, parking garages. Hard edges. Right angles. Brutalist concrete and glass towers. This is the rigid structure the player moves through.

Against that grid, everything player-touched is **aerodynamic and curved**: cars with sloped hoods and curved fenders, character silhouettes with rounded shoulders and flowing clothing, motion trails that arc and ribbon. The player's presence in the world is defined by curves cutting through the city's angles.

This creates visual tension. The city resists. The player flows. When the player drifts, the curve of the drift line contrasts the straight line of the road. When the player dunks, the arc of the jump contrasts the rectangular backboard. Shape language reinforces the theme: you do not belong to this city's grid. You move through it.

### Character Proportions

**GROUNDED HEROIC** — not realistic, not cartoony, but stylized toward presence.

- **Head-to-body ratio**: 1:7. Slightly heroic (realistic human is 1:7.5). This gives characters a touch of larger-than-life energy without tipping into caricature.
- **Shoulders**: Broad. 2.5x head width for male-coded builds, 2x head width for female-coded builds. This is street athlete physique, not fashion model.
- **Hands and feet**: Slightly oversized (10% larger than realistic proportion). This makes gestures and footwork readable at gameplay camera distances. A crossover, a punch, a kickflip — the extremities must read clearly.
- **Clothing volume**: Baggy. Jeans, hoodies, jerseys, jackets — all have extra fabric. This is era-accurate and creates silhouette variety. Tight clothing is reserved for specific cosmetic choices (tank tops, compression wear under jerseys). The default is "loose."

**Silhouette test**: A character in neutral pose, backlit to pure black silhouette, should be identifiable as "street athlete" not "soldier," "knight," or "cartoon character." Readable at 64x64 pixel thumbnail size.

### Vehicle Shapes

**TUNER CULTURE GEOMETRY** — low, wide, aggressive.

Every car in UNDERGROUND falls into one of three body archetypes:

1. **IMPORT COMPACT (Civic, Golf, 240SX vibes)**: Low front end, high rear spoiler, wedge profile. Polygon budget: 8,000-10,000 tris. Customization emphasizes width (body kits flare the fenders, side skirts hug the ground).
2. **SPORT COUPE (350Z, RX-7, Supra vibes)**: Sleek, curved, "organic" shape language. Polygon budget: 10,000-12,000 tris. Customization emphasizes aero (front splitters, rear diffusers, hood vents).
3. **MUSCLE (Mustang, Charger, GTO vibes)**: Rectangular, wide-hipped, forward-leaning stance. Polygon budget: 9,000-11,000 tris. Customization emphasizes power (hood scoops, wide tires, aggressive front grilles).

**Mandatory design feature**: Every car must have visible underglow emitters. These are modeled as glowing strips beneath the chassis, casting light downward onto the ground plane. This is not a cheap shader trick — it is a light source with real-time shadows (simplified, single-bounce).

**Silhouette test**: Every car archetype should be identifiable in silhouette from profile view at 128x128 pixels. No car should be mistaken for another archetype.

### Environment Shapes

**LAYERED URBAN DENSITY** — the city is a vertical stack.

- **Ground layer (street level)**: Rectangular. Roads are grids. Sidewalks are straight. Basketball courts are perfect rectangles with rounded key zones. This is the "law" layer — geometry enforced by city planning.
- **Mid layer (0-20 feet)**: Where the underground takes over. Graffiti breaks up flat walls with organic curves. Parked cars interrupt the grid. Crowds form irregular clusters. Light poles and fire escapes add diagonal lines. This is the "life" layer.
- **High layer (20+ feet)**: Skyline. Simplified building blocks, many reused with texture variants. The skyline is *not* the hero. It is the backdrop. Low-poly, high-repetition, but always framing the player's space.

**Readability through shape**: Interactive objects (ramps for tricks, drift zones, fight rings, basketball courts) are always outlined by contrasting geometry. A drift zone might be bordered by tire barriers (black rubber against gray asphalt). A trick ramp has a bright texture stripe at the edge. A fight ring is a chain-link cage catching light. The eye should find the play space in under 2 seconds of entering a new area.

### Gameplay Communication Through Shape

**SHAPE = FUNCTION**

- **Circles and rounded rectangles**: Safe zones, interactive prompts, positive feedback. When you see a circle, you can act on it.
- **Triangles and chevrons**: Danger, direction, urgency. Pointing down = hazard on ground. Pointing up = jump opportunity. Pointing sideways = incoming threat.
- **Straight lines**: Structure, boundaries, non-interactive. If it's a straight horizontal or vertical line, you cannot interact with it (walls, curbs, building edges).
- **Curved lines in motion**: Player-created. Drift trails, motion blur, trick arcs. If it curves and glows, the player made it happen.

This is visual grammar. After 30 minutes of play, the player should parse the environment pre-consciously. They do not think "that's a triangle, so it means danger." They just *feel* danger when they see the shape.

---

## 5. Style Rules

### Line Quality

**CRISP WITH INTENTIONAL GRIT**

- **3D model edges**: Clean. No unnecessary edge loops. The models are low-poly by design, and we embrace it. Edges are sharp where they should be sharp (car panel seams, building corners), smoothed where they should be smooth (character faces, organic forms).
- **Texture lines**: Hand-authored, not procedural. Graffiti has visible brush strokes. Tire marks have texture. Scratches on metal are deliberate, not scattered noise. Every line in a texture was put there by an artist who meant it.
- **UI lines**: 2-4px thick, hard-edged, no anti-aliasing on the outer border (the inner fill can be smooth). Buttons and panels have the chunky, clickable look of early 2000s web design and car dashboard mods. Beveled edges are 45-degree angles, not subtle gradients.
- **Motion lines**: During fast actions (drifts, punches, trick spins), we draw actual stylized motion lines — comic book speed streaks, 3-5 lines trailing the action, colored to match the accent palette (Cyan for cold actions, Orange for hot). These last 4-6 frames and fade. They are not realistic, and that is the point.

**What we do not do**: Overly smooth, "realistic" line work. No soft gradients on hard surfaces. No procedural wear-and-tear that makes everything look uniformly dirty. Grit is placed with intent, not sprayed on.

### Texture Approach

**HIGH-RES TEXTURES, LOW-POLY MODELS**

This is the visual trick that makes UNDERGROUND feel like "what if the PS2 had more VRAM."

- **Resolution standard**: 2048x2048 for hero assets (player car, player character, named rivals, boss arenas). 1024x1024 for common assets (NPC cars, crowd members, environment props). 512x512 for distant/non-interactive geometry (skyline buildings, background clutter).
- **Texture style**: Hand-painted with photo reference. Not photorealistic (no photo-scanned concrete), but not flat-illustrated either. We paint textures that *suggest* material — metal looks metallic through specular response and color choice, not through hyper-detailed rust maps. Concrete has subtle color variation and crack lines, but not 4K scanned detail.
- **Graffiti as signature**: Every district has unique graffiti tags. These are high-res (1024x1024 decals), colorful, and legible. They serve as environmental storytelling (you can tell which crew owns a block by the tags) and as visual wayfinding. Graffiti is never random noise — it is content.
- **Decals and wear**: Cars accumulate dirt and scratches dynamically during races (simple dirt texture overlay that fades in over time, plus procedural scratch decals on impact zones). This resets when you visit the garage. The contrast between a clean car and a battle-worn car is visible and meaningful.

**Shader rules**:
- **Car paint**: Metallic shaders with high specular. Cars *shine*. Even matte paint has a subtle sheen. The player's car is always the shiniest object in the frame (slight cheat on specular multiplier: player car gets 1.3x spec intensity vs. NPC cars).
- **Underglow**: Emissive + dynamic light casting. The underglow is not just a glowing texture — it is a light source affecting the ground and nearby objects. Computationally cheap (baked light probes + real-time fill light, not full ray-tracing).
- **Neon signs**: Emissive with bloom. All neon signs have a 10-20px bloom radius in post-processing. This is the CRT effect: light bleeds. Neon signs should look slightly out-of-focus, like your eyes cannot quite contain them.
- **Character skin**: Subsurface scattering disabled. Skin has a matte base with specular highlights only on sweat (which appears during high-intensity events). We are not going for realism — we are going for stylized clarity.

### Lighting Style

**MOTIVATED, DRAMATIC, NEVER FLAT**

Every light source in UNDERGROUND is *visible*. You can point to the streetlight, the neon sign, the car headlight, the floodlight that is casting the light you see. No ambient fill lights hiding in the scene to "fix" darkness. Darkness is intentional.

**Three-light philosophy adapted for street**:

1. **Key light (the hero light)**: The dominant light source in any shot. In a drift race, it is the streetlights overhead and the player's headlights. In a fight, it is the overhead cage light or a nearby fire barrel. In a ball game, it is the court floodlights. The key light is always hard-edged, creating strong shadows.

2. **Rim light (the separation light)**: The player character always has a rim light — a thin outline of white or cyan light separating them from the background. This is slightly unrealistic (the light is always behind them regardless of actual light source positions), but it is essential for readability. NPCs do not get rim lights unless they are rivals, in which case their rim light is their signature color (Magenta for bosses, underglow color for regular rivals).

3. **Accent light (the signature light)**: The underglow, the neon sign, the Style Meter glow reflecting on the player's face during UNDERGROUND MODE. This is the light that says "this moment is special." Accent lights are always colored, never white.

**Time of day**: 95% of gameplay happens at night. The city is a night city. The few daytime events (tutorial, specific story beats) use overcast lighting — heavy clouds, diffuse light, desaturated by 20%. Daytime is narratively coded as "normal world." Nighttime is the underground.

**Weather lighting**:
- **Rain**: Wetness multiplies specularity by 2x. Every surface becomes a mirror. Neon reflects in puddles. Headlights streak across wet asphalt. Rain is not just a particle effect — it is a lighting transformation.
- **Fog**: Light shafts become visible (volumetric fog, simplified). Headlights cut cones through mist. Distant neon signs become soft halos. Fog reduces visual range to 50-75% of normal, creating intimacy and tension.

### Animation Style

**SNAPPY WITH WEIGHT**

UNDERGROUND is not a simulation. Animations prioritize *readability* and *game-feel* over *realism*.

**Core principles**:

1. **Anticipation and snap**: Every major action has a brief wind-up (3-6 frames) and then SNAPS into the action. A punch pulls back slightly before launching forward. A drift entry has a weight shift before the slide. A crossover has a slight shoulder fake before the explosive direction change. This is borrowed from fighting games and Tony Hawk — the player should *feel* the moment of commitment.

2. **Exaggeration on success**: When the player lands a perfect input, the animation exaggerates. A perfect drift has more smoke, more angle, more camera shake. A perfect ankle-breaker has the defender stumble farther. A perfect trick has more rotation before the snap to landing. Success feels *bigger* than baseline.

3. **Weight distribution**: Characters are heavy. When they land from a jump, there is a crouch and settle (4-8 frames). When a car drifts, the suspension visibly shifts — outer wheels compress, inner wheels lift slightly. When a punch connects, both fighters react (attacker has recoil, defender has knockback).

4. **Limited frames for retro feel**: Key animations (walk, idle, celebrate) run at 15-20 FPS animation rate, even though the game runs at 60 FPS. This creates a slight "stepped" quality that reads as stylized, not broken. Combat and racing remain at 30 FPS animation rate for responsiveness, but idles and transitions are chunkier.

5. **Motion blur is aggressive**: During fast actions, we apply per-object motion blur (not full-screen). A drifting car has streaked wheels and body blur. A spinning trick has rotational blur. A punch has a smear frame (actual hand-drawn smear texture swapped in for 1-2 frames). This is animation tradition, not rendering realism.

**Signature animation moments**:
- **The step-out**: Transitioning from car to on-foot. The car door opens (2-second animation, unskippable), the player steps out (4-second full-body animation with camera rotation), the camera settles into on-foot view. This is the "genre switch" moment, and it is CINEMATIC every time. The camera work here is borrowed from Fast and the Furious hero-stepping-out-of-car shots.
- **The taunt**: During fights, the player can taunt (1.2-second vulnerability window). The taunt animation is exaggerated — arms wide, head back, or a dismissive hand wave. The camera zooms in slightly. The crowd roars. This is risk made visible.
- **The celebration**: After victory, there is a 3-5 second celebration (fist pump, arms raised, car burnout donut, ball spin on finger). The player does not control this. It is the game saying "you earned this moment." The camera pulls back to hero-shot framing.

### Style Do's and Don'ts

| DO | DON'T |
|----|-------|
| Embrace low-poly as a stylistic choice. Show those edges. | Try to hide the polycount with excessive smoothing or subdivision. We are not ashamed. |
| Use neon and underglow aggressively. Let it bleed and bloom. | Over-saturate to the point of unreadability. Neon should pop, not blind. |
| Place grit and wear with intent. Every scratch tells a story. | Spray procedural dirt and damage uniformly. Not everything is equally worn. |
| Animate with anticipation and snap. Every action should feel committed. | Float or slide characters. No ice-skating. Weight always. |
| Let the UI be chunky and bold. This is a 2000s car dashboard. | Minimize or flatten the UI into modern clean design. That is not this game. |
| Use chromatic aberration and scan lines as core visual identity. | Make them a toggleable "retro filter." They are not optional. They are the art. |
| Light dramatically. Let shadows be black. Let neon be the hero. | Fill-light every scene to avoid darkness. Darkness is part of the mood. |
| Exaggerate success states. S-rank should feel like the screen is celebrating. | Treat success feedback as a subtle UI popup. Make noise. Make light. |
| Keep the camera dynamic during action. Drift entries, punch impacts, dunk slams — the camera reacts. | Lock the camera static. The camera is a participant in the action, not an observer. |
| Make the player's car and character the brightest, sharpest thing on screen. | Let NPCs and environments compete for visual dominance with the player. |

| DON'T (continued) | NEVER |
|-------------------|-------|
| Use realistic motion blur or depth-of-field. Our blur is stylized. | Use film grain as a static overlay. Our grain is animated, tied to Style Meter intensity. |
| Use more than three neon colors in a single composition. | Let accent colors touch. Space them. |
| Make interactive objects blend into the environment. | Use pure black `#000000`. Asphalt Black `#0D0D12` is the darkest value. |
| Add details the player will never see. Every poly must be on-screen. | Smooth out the UI. It is beveled and chrome-dripped forever. |

---

## 6. Asset Pipeline

This section defines how art moves from concept to engine. This is for the production team — artists, technical artists, and engineers.

### File Formats

| Asset Type | Source Format | Export Format | Notes |
|------------|---------------|---------------|-------|
| **3D Models (Characters)** | Maya, Blender (`.ma`, `.blend`) | `.fbx` (binary) | Include skeleton rig. Bone count max: 75 bones per character. |
| **3D Models (Vehicles)** | Maya, Blender | `.fbx` (binary) | Separate meshes for body, wheels, underglow emitters. Pivot point at ground center (between front wheels). |
| **3D Models (Environment)** | Maya, Blender | `.fbx` or `.obj` | Environment pieces can be `.obj` if static (no animation). Use `.fbx` if they have simple animations (doors, gates). |
| **Textures (Diffuse/Albedo)** | Photoshop, Substance Painter (`.psd`, `.spp`) | `.png` (RGB, no alpha) | sRGB color space. No compression during export (engine compresses). |
| **Textures (Transparency/Cutout)** | Photoshop, Substance Painter | `.png` (RGBA) | Alpha channel defines cutout mask. Used for chain-link fences, graffiti decals, foliage. |
| **Textures (Emissive/Glow)** | Photoshop, Substance Painter | `.png` (RGB) | Black = no emission, full color = full emission. Used for neon signs, underglow, UI elements. |
| **Textures (Normal Maps)** | Substance Painter, ZBrush, Photoshop (via Nvidia plugin) | `.png` (RGB) | OpenGL normal map format (Y+). Low strength (multiply by 0.5 in shader) — we do not want aggressive surface detail. |
| **UI Elements** | Photoshop, Figma | `.png` (RGBA for elements with transparency, RGB for full-frame) | Export at 2x target resolution (if UI is 1920x1080, export at 3840x2160 and downsample in engine for sharpness). |
| **Animations** | Maya, Blender | `.fbx` (binary with embedded animation) | 30 FPS animation framerate (60 FPS gameplay, but animation steps at 30 for stylization). Idles/transitions: 15 FPS. |
| **VFX (Particles, Trails)** | After Effects, Photoshop (frame sequences) | `.png` sequence (RGBA) or sprite sheet `.png` | Sprite sheets preferred for performance. Max 4096x4096 sheet, individual sprites power-of-2 (128x128, 256x256). |
| **Audio (Music)** | DAW (Ableton, FL Studio, Logic) | `.wav` (16-bit, 44.1kHz, stereo) for engine import -> converts to `.ogg` | High-quality source for engine compression. Music loops are sample-accurate (no pops). |
| **Audio (SFX)** | DAW, field recording, library | `.wav` (16-bit, 44.1kHz, mono or stereo as appropriate) | SFX are mono unless they are stereo-specific (crowd ambience, environmental loops). |

### Resolution Standards

| Asset Type | Resolution / Polycount | Justification |
|------------|----------------------|---------------|
| **Player Character (Body)** | 4,500-6,000 tris | Hero asset, on-screen 70% of playtime. Needs to look good in photomode and close-up cutscenes. |
| **Player Character (Head)** | 1,500-2,000 tris | Separate mesh from body for customization. Extra detail in face for expression. |
| **Player Vehicle** | 10,000-12,000 tris | Hero asset. Customizable, on-screen constantly during racing. Highest-poly asset in the game. |
| **Rival Character** | 3,000-4,500 tris | Named NPCs, appear in multiple events. Higher quality than crowd, lower than player. |
| **Rival Vehicle** | 7,000-9,000 tris | Appear in races, recognizable designs. Slightly lower than player car. |
| **NPC Crowd Member** | 800-1,200 tris | 20-50 on screen simultaneously. Low poly, high readability. Texture does the work. |
| **NPC Vehicle (Traffic)** | 2,000-4,000 tris | Background, not hero. Simplified shapes, bold colors for readability. |
| **Environment Props (Hero)** | 500-2,000 tris | Basketball hoop, streetlight, graffiti wall, chain-link fence section. Reused heavily. |
| **Environment Props (Clutter)** | 50-300 tris | Trash can, fire hydrant, traffic cone, newspaper box. Texture detail over geometry. |
| **Buildings (Mid-Ground)** | 300-1,000 tris per building | Modular pieces. Repetition is acceptable — texture variants create variety. |
| **Buildings (Skyline)** | 50-200 tris per building | Silhouette blocks. No detail. Pure backdrop. |
| **Textures (Hero Assets)** | 2048x2048 | Player car, player character, boss arenas, named rival vehicles. |
| **Textures (Standard Assets)** | 1024x1024 | Rivals, common vehicles, environment props, building facades. |
| **Textures (Background/Clutter)** | 512x512 | Skyline, distant objects, small props. |
| **UI Textures** | 1920x1080 (full-screen), 512x512 (icons), 256x256 (small elements) | Exported at 2x and downsampled for sharpness on high-DPI displays. |

### Tools and Software

**Required** (all artists must have):
- **3D software**: Maya (studio standard) OR Blender (acceptable alternative). Files must export to `.fbx` cleanly.
- **Texture software**: Photoshop (industry standard) OR GIMP + Krita (acceptable alternatives).
- **Version control awareness**: All artists must understand how to commit to the asset repo (Git LFS or Perforce, TBD by engineering). No "final_final_v3" filenames.

**Recommended** (specialist tools):
- **Substance Painter**: For PBR texturing workflow (even though we are not full PBR, Substance is useful for generating base maps).
- **ZBrush**: For high-poly sculpts that bake down to normal maps (used sparingly — we are low-poly, but some hero assets benefit from baked detail).
- **Marvelous Designer**: For character clothing. The baggy clothing style is easier to author in Marvelous and retopologize than to sculpt by hand.
- **Figma or Adobe XD**: For UI mockups before implementation.

### Naming Conventions

All asset files follow this structure:

```
{AssetType}_{AssetName}_{Variant}_{LOD}.{extension}

Examples:
CH_PlayerBody_DefaultOutfit_LOD0.fbx      (Character, Player Body, Default Outfit, highest LOD)
VH_Civic_Underglow_Cyan_LOD0.fbx          (Vehicle, Civic, Underglow Cyan variant)
PR_Streetlight_Sodium_01.fbx             (Prop, Streetlight, Sodium vapor variant 01)
TX_Graffiti_Southside_Tag_01_D.png       (Texture, Graffiti, Southside district, Tag 01, Diffuse)
TX_Graffiti_Southside_Tag_01_E.png       (Texture, Graffiti, Southside district, Tag 01, Emissive)
UI_ButtonDefault_Idle.png                (UI, Button Default state, Idle)
FX_DriftSmoke_SpriteSheet_512.png        (VFX, Drift Smoke, sprite sheet, 512x512 sprites)
```

**Asset type prefixes**:
- `CH_` = Character
- `VH_` = Vehicle
- `PR_` = Prop (environment object)
- `TX_` = Texture
- `UI_` = User Interface
- `FX_` = Visual Effects
- `AN_` = Animation
- `SF_` = Sound Effect
- `MX_` = Music

**Texture suffixes**:
- `_D` = Diffuse/Albedo
- `_N` = Normal map
- `_E` = Emissive
- `_M` = Metallic
- `_R` = Roughness
- `_A` = Alpha/Transparency

**LOD suffixes**:
- `_LOD0` = Highest detail (full polycount)
- `_LOD1` = Mid detail (50-60% polycount)
- `_LOD2` = Low detail (25-35% polycount)
- No suffix for assets with single LOD

### Handoff Process

**Concept -> Blockout -> Final -> Engine**

1. **Concept Phase**: Art director (PIXEL) or lead artist provides reference board + sketch/paintover. Concept art is not required for every asset (we are working from established style), but major assets (hero vehicles, bosses, new districts) get full concept art. Format: Photoshop layered file, exported to `.png` for review. Reviewed in weekly art review meeting.

2. **Blockout Phase**: Artist creates low-poly blockout ("gray box" model) with correct scale and basic shape. This goes into the engine immediately for gameplay testing. No textures. Flat gray material. This is the "does it work?" phase. Engineers and designers test collision, scale, readability. If blockout fails, iteration happens here before time is spent on final art.

3. **Final Art Phase**: Artist completes the model to full polycount, UVs, textures, materials. Exported to `.fbx` with proper naming convention. Submitted to asset repo with a commit message: "Added final art for [Asset Name] - [LOD levels included] - [Polycount]."

4. **Engine Integration**: Technical artist or engineer imports into engine, sets up materials, assigns to correct layers (collision, rendering, LOD groups). Marks asset as "Ready for QA." QA tests asset in all relevant contexts (different lighting, different camera angles, performance).

5. **Iteration**: If issues found in engine (texture seams, clipping, performance problems), asset returns to artist with annotated screenshots or video. Artist fixes, re-exports, re-submits. This loop continues until QA approves.

**Review cadence**:
- **Daily scrums** (10 min): Artists show work-in-progress screenshots in Slack/Discord. Quick feedback from art director or peers.
- **Weekly art review** (1 hour): Full team reviews completed assets, blockouts ready for promotion, and major WIP. Art director gives formal approval or requests changes.
- **Biweekly playtests**: Artists play the build. See their work in context. This is where readability issues surface.

### Version Control for Art Assets

All art assets live in a Git LFS (Large File Storage) repository or Perforce depot (engineering team decides, but process is the same).

**Rules**:
1. **Commit often**: Every meaningful checkpoint (blockout done, first texture pass done, final asset done) gets a commit. No "save up 3 days of work and commit once." That is how work gets lost.
2. **Commit messages must be clear**: "Updated car" is bad. "VH_Civic: added underglow emitters and updated cyan texture to match palette" is good.
3. **Never commit broken assets**: If the `.fbx` has errors or the texture is half-done, do not commit to main branch. Use a feature branch or mark the commit as WIP (work-in-progress).
4. **Source files (.ma, .blend, .psd) are committed alongside exports**: Every `.fbx` has its source `.blend` or `.ma` file in the repo. This is non-negotiable. If an artist leaves or an asset needs changes 6 months later, the source must be available.
5. **Large files are LFS-tracked**: Any file over 1MB is stored in LFS (models, textures, audio). The repo itself stays lightweight.

---

## 7. Readability Audit

Before any asset, environment, or UI element ships, it must pass these four tests. This is the quality bar.

### Test 1: The Squint Test

**What it is**: View the game at full resolution, then squint your eyes until detail blurs. Can you still parse the critical information?

**What passes**:
- You can still see where the player is (they remain the brightest, most contrasted element).
- You can distinguish the road from the sidewalk from the buildings.
- Interactive objects (ramps, drift zones, fight rings) remain distinct from non-interactive background.
- UI elements (health bar, Style Meter, button prompts) are still legible as shapes, even if text blurs.

**What fails**:
- The player blends into the environment.
- Multiple neon signs blur into a wash of color with no distinct sources.
- Interactive and non-interactive objects look identical.
- UI disappears or becomes ambiguous.

**Fix if failed**: Increase contrast. Add rim lights. Simplify background density. Reduce neon color variety in a single frame.

### Test 2: The Thumbnail Test

**What it is**: Take a screenshot of active gameplay (racing, fighting, balling, tricking). Scale it down to 256x144 pixels (16:9 thumbnail). Can you tell what is happening?

**What passes**:
- You can identify the discipline (is this a race? a fight? a ball game?).
- You can locate the player.
- You can tell if the player is winning or in danger.
- The composition is readable (foreground, mid-ground, background are distinct).

**What fails**:
- The screenshot looks like noise or abstract color.
- You cannot tell what the player is doing.
- The player is not findable in the frame.
- The image has no clear focal point.

**Fix if failed**: Increase player rim light intensity. Reduce background detail or desaturate background by 10-15%. Adjust camera framing to keep player in rule-of-thirds focal zone. Add post-processing vignette to darken edges and direct eye to center.

### Test 3: The Colorblind Test

**What it is**: View the game through colorblind simulation filters (protanopia, deuteranopia, tritanopia). Available in Photoshop, or use online tools like [Coblis](https://www.color-blindness.com/coblis-color-blindness-simulator/). Can you still play the game?

**What passes**:
- Danger zones are identifiable without relying on red color (they have animated chevrons, warning text, sound cues).
- Interactive prompts are identifiable without relying on green color (they have icons, button outlines, sound cues).
- UI elements remain distinguishable (even if colors shift, contrast and shape language still work).
- The player's car underglow color choice is visible (even if hue shifts, the light is still distinct from background).

**What fails**:
- Red danger zones become invisible against green backgrounds in deuteranopia.
- "Go" signals and "Stop" signals look identical.
- UI buttons lose distinction.
- Critical information is communicated only by color.

**Fix if failed**: Add non-color signifiers. Every colored element must have a shape, icon, or pattern that communicates its meaning without color. Danger = triangle + animation. Success = circle + glow. Interactive = icon + outline. Use the CVAA (Communications and Video Accessibility Act) guidelines as reference.

### Test 4: The Motion Test

**What it is**: Play the game at full speed during high-intensity moments (UNDERGROUND MODE active, screen full of effects, camera shaking, motion blur on). Can you still track the player and parse critical info?

**What passes**:
- The player remains trackable even during extreme camera movement.
- The Style Meter is readable (you can glance and know your tier).
- Health/stamina bars are readable.
- Incoming threats (rival attacks, obstacles, traffic) are telegraphed clearly enough to react.

**What fails**:
- The player gets lost in their own effects (underglow, drift smoke, motion blur).
- UI elements shake or blur to the point of unreadability.
- Threats appear without warning due to visual overload.
- The player cannot tell what killed them or why they failed.

**Fix if failed**: Reduce effect opacity during UNDERGROUND MODE (particle effects drop to 70% opacity, motion blur reduces by 20%). Add a "threat indicator" UI (directional arrow at screen edge when a rival is approaching from off-screen). Stabilize critical UI elements (Style Meter, health bar) so they do not shake with the camera. Ensure the player's rim light increases during chaotic moments.

---

## 8. Reference Visual Library

### Game References (The DNA)

These games are in UNDERGROUND's bloodline. Study them.

1. **Need for Speed Underground 2 (2004)**: The career mode structure, the garage customization UI, the neon-soaked city, the CRT filter, the underglow as identity. We are the spiritual successor to this.

2. **Def Jam: Fight for NY (2004)**: The Blazin' move system (our UNDERGROUND MODE), the rival personality system, the way fighting felt weighty and brutal but stylized, the venue-specific fight arenas. We take the fighting energy from here.

3. **FIFA Street (2005)**: Trick moves as core mechanic, the style meter (they called it "Gamebreaker"), the way street sports felt different from simulation sports, the player-expression-as-progression. We take the ball-handling flow from here.

4. **Tony Hawk's Underground (2003)**: The name (obviously), the trick combo system, the grounded story (you are nobody, you become somebody), the ability to get off your board and explore. We take the trick philosophy and narrative arc from here.

5. **Midnight Club 3: DUB Edition (2005)**: The city density, the way licensed cars became customizable canvases, the "style as gameplay" philosophy. We take the customization depth from here.

6. **Yakuza 0 (2015)**: Not a 2000s game, but crucial reference for how to make a dense city feel ALIVE. The way substories and side activities are woven into the world, the way NPCs have personality. We take the city-as-character philosophy from here.

### Film References (The Aesthetic)

These films nail the visual temperature and era.

1. **The Fast and the Furious (2001)**: The car beauty shots, the underglow, the neon-lit garage scenes, the hero-stepping-out-of-car framing. Every race start in UNDERGROUND should feel like a Fast and Furious set piece.

2. **8 Mile (2002)**: The rap battle lighting (single overhead light, dark backgrounds, spotlight on performer), the gritty Detroit texture, the way the underground venue feels. Our fight rings borrow this lighting.

3. **Brown Sugar (2002)**: The hip-hop culture love letter energy, the warm streetlight glow, the nostalgia for the "before it was cool" era. This is the emotional core.

4. **Honey (2003)**: Dance battle lighting, the way the camera follows movement fluidly, the color palette (warm amber street lights, cool blue nightclub interiors). We use this for our ball game camera work.

5. **Blade II (2002)**: The stylized action (not realistic, not cartoony — elevated reality), the way the environment reflects the characters (industrial, underground, raw), the use of color as threat (red = danger). We take the action cinematography philosophy from here.

### Music Video References (The Energy)

The editing, the camera moves, the color grading.

1. **Missy Elliott - "Pass That Dutch" (2003)**: High-contrast lighting, bold geometric backgrounds, fisheye lens distortion, the way Missy is always the visual center. Our character framing takes notes from this.

2. **50 Cent - "In Da Club" (2003)**: The club lighting (strobes, colored gels, hard shadows), the slow-mo on key moments, the way success is depicted visually (champagne, cars, shine). UNDERGROUND MODE visual language borrows from this.

3. **Ludacris - "Stand Up" (2003)**: The warm street lighting, the crew energy (everyone in frame has presence), the car showcase shots. Our crew system visual identity pulls from this.

4. **The Black Eyed Peas - "Where Is the Love?" (2003)**: Urban environment as backdrop (graffiti, concrete, chain-link), desaturated base with color accents (in this case, question mark stickers). Our color palette balance comes from this.

5. **Outkast - "Hey Ya!" (2003)**: Bold color backgrounds, high energy, the way the camera never sits still. Our UI animation energy (buttons pulse, text bounces in) mirrors this.

### Art Direction References (The Mood)

Fine art, photography, and design that captures the feeling.

1. **Syd Mead's Blade Runner concept art**: Not for the sci-fi elements, but for the way neon cuts through darkness, the way light defines space in a dark city.

2. **Street photography by Jamel Shabazz (1980s-90s)**: The way he captures street culture with dignity and style, the poses, the fashion, the pride in self-presentation. Our character design philosophy draws from his lens.

3. **Graffiti art by KAWS and Shepard Fairey (OBEY)**: Bold, graphic, high-contrast, iconic. Our graffiti is not tags-as-texture — it is art with intent. Study the composition and readability of wheat-paste posters and large-scale murals.

4. **Cyberpunk 2077 marketing materials (not the game, the marketing)**: The way they sold a neon-soaked world through stills and trailers, the color contrast, the use of magenta and cyan as signature colors. We are not cyberpunk, but we share a neon bloodline.

5. **Auto Trader magazine photo shoots (2000-2005)**: The way tuner cars were photographed — low angles, spotlights, reflections on paint, the garage as altar. Every car in UNDERGROUND should feel like it belongs on a magazine cover.

---

## 9. Technical Constraints

These are the limits we operate within. They are not compromises — they are the structure that makes the style possible.

### Platform Targets
- **PC (primary)**: 1920x1080 minimum, 60 FPS locked. Scalable to 4K, but art is authored for 1080p clarity.
- **Console (secondary)**: PS5 / Xbox Series, 1080p/60 FPS performance mode or 4K/30 FPS quality mode.

### Rendering Budget
- **Draw calls**: Max 1500 per frame (city environments are heavy, but we use aggressive occlusion culling and object pooling).
- **Polycount on-screen**: Target 1-2 million tris visible per frame. Player car + player character + 5-8 NPC cars + environment. LOD system is mandatory.
- **Texture memory**: 2GB VRAM budget for textures (at 1080p). Textures stream in as the player moves through the city. Skyline buildings use texture atlases (many buildings share one 2048x2048 texture).
- **Lighting**: Max 8 dynamic lights affecting any single object. Dynamic shadows for player and rivals only. NPC traffic and distant objects use baked lightmaps.

### Post-Processing Stack (Always Active)
1. **CRT Shader**: Scan lines (horizontal, 720 lines, 30% opacity), chromatic aberration (2px offset on red/blue channels), slight barrel distortion (5% on edges), color bleed (subtle glow around high-contrast edges).
2. **Bloom**: Threshold 0.8 (only very bright elements bloom), radius 15px, intensity tied to Style Meter (scales from 0.5x at COLD to 2.0x at UNDERGROUND MODE).
3. **Film Grain**: Animated noise texture (64x64 tiling, 0.1 strength at COLD, 0.3 strength at UNDERGROUND MODE). The grain is not static — it moves frame-to-frame like real film.
4. **Vignette**: Subtle darkening at corners (20% darker at COLD, 40% at UNDERGROUND MODE). This keeps the eye centered.
5. **Color Grading**: LUT (Look-Up Table) applied. Two LUTs: "Night" (default, cool blue bias) and "Day" (used in 5% of events, warm desaturated). The LUT is not subtle — it is a strong teal-and-orange grade borrowed from 2000s action films.

### Animation Budget
- **Character skeleton**: Max 75 bones. Facial rig: 15 bones (jaw, brows, eyes, basic expressions — we are not doing full performance capture).
- **Animation framerate**: 30 FPS for gameplay actions, 15 FPS for idles and background NPCs. This is a creative choice, not a performance limit.
- **Blend tree complexity**: Max 5-way blends in any single animation state (e.g., movement blends forward/back/left/right/idle). More complex blends cause visual stuttering.

### Audio-Visual Sync
- **Music must sync to gameplay**: The Style Meter influences the music mix (bass boosts at ON FIRE tier, high-hats sharpen at HOT tier). This requires music stems (drums, bass, melody, vocals as separate tracks). Audio team provides stems, visual team triggers mix changes via game state.

---

## 10. Accessibility and Inclusivity Notes

UNDERGROUND's art is aggressive, high-contrast, and neon-soaked, but it must remain *accessible* and *inclusive*.

### Visual Accessibility
- **Colorblind modes**: Not needed because the game is designed colorblind-safe from the start (see Readability Audit, Test 3). But if a player requests further assistance, we offer three UI overlays: Protanopia filter, Deuteranopia filter, Tritanopia filter. These are optional, not required.
- **Photosensitivity warning**: UNDERGROUND has strobing effects (UNDERGROUND MODE, club interiors, lightning during storms). The game includes a photosensitivity warning on boot and an option to reduce strobe intensity by 70%. This is in Settings > Accessibility, clearly labeled.
- **Motion sickness options**: Camera shake, motion blur, and FOV are adjustable. Default settings are aggressive. Players prone to motion sickness can reduce shake by 50%, disable motion blur, and increase FOV from 75 to 90 degrees.

### Character Customization and Inclusivity
- **Body types**: The player character customization offers two base body frames: "Athletic Build A" and "Athletic Build B" (not gendered labels). Both are street-athlete physiques, differ in shoulder width and hip proportions. All clothing fits both frames.
- **Skin tones**: 12 skin tone options, spanning the full spectrum from lightest to darkest. Reference: The Sims 4's inclusive skin tone range, but with our stylized shader (matte finish, specular on sweat only).
- **Hairstyles**: 20+ options, representing Black (locs, fades, braids, waves), Latinx (fades, slicked styles), Asian (various cuts), and White hairstyles. No "default" hairstyle. Hair is high-poly (1,000-1,500 tris per hairstyle) because it is crucial to identity.
- **Fashion options**: Street culture spans communities. The fashion catalog includes: baggy jeans, fitted caps, durags, hijabs (as a headwear option for players who want it), hoodies, jerseys, Timbs, Air Force 1s, Jordans, skate shoes. All options are modular (top, bottom, shoes, hat, accessories).
- **Voice**: Player character is voiced (brief callouts, taunts, celebrations). Two voice options: Voice A (deeper), Voice B (higher). Not labeled by gender. Player picks the voice that feels right.

### Cultural Respect
UNDERGROUND is a love letter to early-2000s street culture — a culture built by Black, Latinx, and immigrant communities in American cities. We are not tourists. We are reverent.

**Guidelines for the art team**:
1. **Graffiti and street art**: Work with cultural consultants or contract street artists to ensure graffiti in the game reads as authentic, not stereotyped. Tags and murals should reflect real graffiti traditions (tagging, piecing, murals), not generic "urban decay" texture packs.
2. **Fashion accuracy**: Clothing should reflect what was actually worn in 2000-2005 street culture, not costumes or caricatures. Reference actual photos from the era (hip-hop magazines, concert photography, music videos) rather than Hollywood depictions.
3. **Language and slang**: Rival dialogue and flavor text use era-appropriate slang, but avoid appropriation or mockery. If we are unsure whether a phrase is respectful, we consult a sensitivity reader or cultural consultant.
4. **Diversity in representation**: Rivals, NPCs, and bosses span races, ethnicities, and backgrounds. No single "type" dominates. The underground is diverse because the real underground was diverse.

---

## 11. Style Consistency Checklist (For Team Use)

Before any asset or frame ships, run through this checklist:

- [ ] **Polycount is within budget for asset type** (see Section 6: Asset Pipeline).
- [ ] **Colors pulled from official palette** (see Section 3: Color Palette). If a custom color is needed, justify it to art director.
- [ ] **Neon lights have bloom and cast dynamic light** (not just emissive textures).
- [ ] **Player is the brightest element in frame** (rim light + specular + underglow).
- [ ] **Shadows exist and are black** (no "fill lighting" hiding in the scene).
- [ ] **CRT shader is active** (scan lines, chromatic aberration, color bleed).
- [ ] **UI elements are beveled and chunky** (no flat modern design).
- [ ] **Textures are hand-authored, not procedural noise** (every mark has intent).
- [ ] **Character silhouettes read at thumbnail size** (64x64 pixel test).
- [ ] **Vehicle underglow is visible and color-matched to palette** (cyan, orange, magenta, green, or off).
- [ ] **Interactive objects are visually distinct from background** (contrast, shape, or light).
- [ ] **Animation has anticipation and weight** (no floating or sliding).
- [ ] **Success states are celebrated visually** (screen shake, glow, camera zoom, particle burst).
- [ ] **All four readability tests passed** (squint, thumbnail, colorblind, motion).
- [ ] **No more than three neon colors in a single composition** (space them out).
- [ ] **Asset naming convention followed** (see Section 6: Naming Conventions).
- [ ] **Source files committed to version control alongside exports** (.blend, .ma, .psd with .fbx, .png).

---

## 12. Closing Note from PIXEL

This document is not a suggestion. This is the contract between art and design, between vision and execution. Every pixel that makes it into UNDERGROUND must answer to this document.

You are building a game that looks like 2003, thinks like 2026, and feels like a promise kept. The players who wanted this game in 2005 are waiting. The players who discovered this culture through TikTok and retro streams are waiting. Do not make them a game that apologizes for its style or hides its influences behind "modern sensibilities." Make them the game that screams, "This is what the underground looked like. This is what it felt like. And it never died — it was just waiting for someone to remember."

The art is not decoration. The art is the first promise. The art says: "You are about to play something that respects where it came from."

Now go light up the city.

— PIXEL

---

**Document Revision History**

| Version | Date | Changes | Author |
|---------|------|---------|--------|
| 1.0 | 2026-02-07 | Initial complete art direction document | PIXEL |

**Next Steps**

1. **Concept art sprint** (Week 1-2): Produce reference boards for all four districts, 3-5 hero vehicles, player character customization options, and rival boss designs.
2. **Style guide test build** (Week 3-4): Implement CRT shader, color palette, and lighting rules in a single test environment. One car, one character, one city block. Test readability.
3. **Asset production kickoff** (Week 5+): Begin modeling and texturing based on approved concepts. First assets: player car (Civic archetype), player character base mesh, one district block (Southside), two rival NPCs.

---

**Total Word Count**: 10,847 words

**Every hex value specified. Every rule clarified. Every choice justified. This is UNDERGROUND's visual identity, complete and ready for production.**
