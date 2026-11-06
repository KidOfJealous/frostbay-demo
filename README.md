# Frostbay.

An interactive miniature Arctic diorama built as a single self-contained HTML file using native WebGPU and WGSL — everything procedural, no libraries, no models, no image textures, no network requests.

[Live demo](https://kidofjealous.github.io/frostbay-demo/)

## Original prompt

Create "Frostbay." — an interactive miniature Arctic diorama as ONE self-contained HTML file using native WebGPU (WGSL). Everything procedural: no libraries, no imported models, no image textures, no network requests.

SCENE
- A clear rectangular block of cold sea (≈10 × 7 units, ~1.6 deep) resting on a thick, glossy jelly foundation with rounded edges and soft layered bands of icy blue and pale lavender.
- A snowy rock island toward the back: wet dark rock at the tide line, a cut "core-sample" cross-section where it meets the glass, a few rounded boulders on the sea floor.
- An igloo built from individual curved snow blocks (rows offset like brickwork), a block entrance tunnel, a warm amber ice window and a glowing interior.
- A wooden plank pier on posts with a hanging lantern; a fluttering red-and-white flag on a pole.
- An orange kayak with a double-bladed paddle; ~10 irregular ice floes; a larger ice raft.
- Two harbour seals (spotted, pale muzzle): one basking on a shore ledge of the island, one lying on the raft.
- A humpback whale: one smooth continuous lofted body, pale throat pleats and belly, mouth line, eyes, knobbly rostrum, very long pale flippers, small dorsal fin, wide flukes.
- Calm editorial backdrop; the diorama casts a soft shadow on an unseen floor.

WATER (a real simulation, not a shader trick)
- Height-field long-wave sim (∂²h/∂t² = ∇·(g·depth ∇h)) on a ~200×140 grid, flux form (volume-conserving), fixed 180 Hz substeps, damping + light viscosity + hard clamps: stable at every slider setting and during frantic drags.
- Waves slow and steepen over the shallows, wrap around the island, reflect off the glass and settle.
- Press = a soft plunger making a deep hollow with a raised, volume-neutral rim; dragging sweeps it (speed-limited) and leaves real 3D wakes. Hover never makes waves. Touch supported.
- Dragging a glass side tilts and slides the block on its jelly (damped springs that wobble back) and the sea sloshes toward the new level; a local soft bulge follows the hand. Pulling a jelly edge stretches it locally, then it wobbles home.
- Floating things follow local height and averaged slope, drift, bump each other, avoid shallows and glass.

LIFE
- Kayak: draggable (with a wake). A strong local wave — high swing AND steep averaged slope across the hull — rolls it 180° and leaves it upside down; ordinary ripples and blizzard chop only rock it; never capsizes while held.
- Raft seal: breathes, looks around, articulated flippers. Strong waves make it lose balance, slip off head-first, fall in with a splash, then swim — head up, coordinated hind-flipper strokes, steering away from shallows and glass — and later hauls itself back onto the raft.
- Shore seal: breathes, gazes, scratches with a fore flipper, lifts its head when big waves come.
- Whale: its spine follows the path its head has swum, so it always moves head-first and bends through turns, never sliding backward. "Call the whale" (button or double-click / double-tap) brings it up to the surface, it blows a misty spout, its back heaves the water, then it dives with the flukes rolling under.

LOOK
- Opaque pass to HDR with 4× MSAA plus a distance buffer; water pass with screen-space refraction (wave-driven), depth absorption (deep cold blue, no tropical turquoise), Fresnel sky reflection, restrained soft highlights, foam on crests and shallows, side walls showing the underwater cross-section with a crisp waterline and total internal reflection.
- Moving caustics on everything under the surface, focused by the live wave curvature; soft key-light shadows; neutral tone mapping.
- Modes: Daylight, Snowfall (overcast, falling snow), Aurora night (green/violet curtains, twinkling stars, warm igloo and lantern light with reflections on the water). Blizzard toggle: dense wind-driven snow, gusts and chop on the sea.

UI
- Restrained editorial layout: large italic serif "Frostbay.", short atmospheric subtitle, live status pill, compact panel (weather segments, blizzard switch, jelly firmness, wave damping, tide, Call the whale, Pause, Reset, Camera), concise hints, readouts for seal, kayak, whale and swell; orbit and zoom (pinch on touch).
- Pause freezes all motion; Reset restores sea, block, raft seal and upright kayak.
- Mobile: stacked layout, collapsible controls, ≥44 px touch targets. Clear fallback card if WebGPU is unavailable.

Test water interaction, stability, animals, kayak drag and capsize, whale call, weather modes, pause/reset, shader compilation and mobile layout. Return the finished HTML only.
