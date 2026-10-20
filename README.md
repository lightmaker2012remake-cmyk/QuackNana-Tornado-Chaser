# Tornado Chaser

A storm-chasing simulator for Windows, built from scratch in Godot 4.7 (GDScript + GLSL). Every
chase day is generated from a seed: the sounding and wind profile, the supercell and its
tornadoes, where on the 300-mile map the day happens, and the lighting. The land itself, 300 x 300
miles of it, is generated too and streamed in around you as you drive. The same seed always
reproduces the same day.

## Playing

Run `TornadoChaser.exe` (single file, Windows 10/11 x64, a Vulkan-capable GPU).

* **Play** starts a random storm day. **Settings** has graphics presets (Low, Medium, High,
  Ultra) plus individual options, display, separate audio volumes, mouse sensitivity / invert
  look, multiplayer and a key reference (gamepad is supported).
* **Frame rate**: the volumetric clouds adapt to your GPU. When it cannot hold ~60 fps (a slower
  card, a 4K screen, or the GPU shared with streaming software) they are rendered a little more
  cheaply until there is room again, so the game stays smooth on any preset.
* **Free roam**: no objectives, score or end. You arrive as the day's storms get going: rain
  storms are already falling in several places, and the main storm's tower is just going up. On
  radar it starts as a small dot of rain, grows, and starts to rotate; the tornado warning goes
  out the moment it has a mesocyclone. Drive anywhere, on or off road. The truck (a plain stock
  SUV) takes hail and debris damage but is never written off.
* **First person** throughout: the driver's seat, and your own eyes on foot (look down and you see
  your arms, hands, legs and boots, but never your own head). Mouse looks around, `B` looks back
  (no zoom: only the map zooms). Game time runs at real speed; storms move 10-35 mph.
* **Automatic gearbox**: `W` drives, `S` brakes; hold `S` when stopped to back up. The truck pulls
  hard (0-60 mph in about 6 s, limiter ~116 mph), and gear changes sound like a real automatic.
  Stopped with your foot off the throttle, auto hold keeps it from rolling away on a slope.
  Traction control, ABS and stability control keep it controllable. Off the road (grass, crops,
  dirt, mud) it is nearly as fast as on it; rain and mud only make every surface slippery.
* Rain on the windshield beads up all over the glass and runs down it in streams between the
  (intermittent) wiper sweeps; heavy rain blurs the view behind the drops.
* **The 300-mile map** (483 km square): high plains shortgrass in the west, farmland in the middle,
  tallgrass hills and woodland in the east, sandhills and badland breaks, long rivers about every
  20 miles with cottonwood galleries and creeks every mile or two, a mile-line road grid (gravel,
  dirt, paved county roads, a highway every 24 miles and two interstates), and towns, villages and
  small cities every 15-20 miles with their grain elevators and water towers. Farms, trees, power
  lines, fences, bales and signs are built in 1 km squares around you and freed behind you; wind
  farms, elevators and water towers show from much farther. The world re-centres itself every 10 km
  you travel so it stays precise anywhere on the map. A day's storms are 20-40 miles across and stay
  in their part of the map: you have to drive to them.
* **Fuel**: a full tank lasts about 80 miles (less flat out, more cruising gently). The gauge and the
  range left are under the speed. **Six towns have a gas station** (green GAS squares on the map):
  stop beside a pump and press `Q` to fill up. Run dry and the engine dies; `Q` then calls a
  neighbour who brings a can (a fifth of a tank) after a short wait.
* `P` or `M` opens the storm map: a road atlas of the land (zoom out with the wheel to the whole
  300-mile map; town names and gas stations on it; `B` switches to a satellite view close in), with
  live radar on top, and you as a blue dot with an arrow showing where you are looking. Pick **Base
  Reflectivity**, **Base Velocity** or **Correlation Coeff.** at the bottom right; the bar under
  the map has a dot for every radar frame: press Space to play them all, or drag the handle to any
  frame. The big clock at the top is the time of the radar picture. Zoom with the mouse wheel (all
  the way out is the whole map). Keys: `1` `2` `3`, `0` radar off, PgUp/PgDn tilt, ←/→ step, End
  live, `C` CAPE layer, `B` road map, `V` centre on the truck. Tornado warnings are drawn as red
  polygons; towns inside a tornado warning sound their outdoor sirens. The radar is the nearest
  site of a NEXRAD network spread over the map (about 140 miles apart, like the real one): it
  switches as you travel.
* `F` photograph, `R` release a probe (stopped), `G` raise the mobile radar (stopped), `O` spotter
  report, `I` HUD detail (minimal / detailed / hidden), `F1` help, `Esc` pause menu.
* **Multiplayer**: Settings → Multiplayer. The host clicks Host (in a game, "Host this game") and
  shares the join code; friends type it in and click Join, and load the same storm day. The game
  tries UPnP; if your router refuses it, the code works on the same network, or forward UDP port
  24850 for internet play. **Voice chat**: push to talk (`V` by default, changeable) or open mic,
  heard from the other player's position; their mouth moves as they talk.
* Near a tornado its inflow drags you in and its core lifts the truck (or you) into it: inside it
  goes dark with debris, the wind roars and the view shakes harder the deeper you are.
* `E` gets out of the stopped truck and back in at the driver's door. On foot: `W A S D` walk,
  `Shift` run, `Space` jump. Strong wind pushes you around (it never knocks you down); large hail and
  flying debris hurt.
* Optional launch switch: `TornadoChaser.exe -- --autoplay=<seed>` skips the menu.
* **Sound**: every sound is synthesized from physical models (no recordings): a V8 built from its
  firing pulses, exhaust, muffler and cabin resonances (16 RPM bands x pulling/coasting, all in phase
  so they blend smoothly, tuned against a real V8 interior recording), rain from real raindrop sizes
  and counts ringing the roof panel and windscreen, wind gusts that sweep across the stereo field,
  thunder from a simulated lightning channel that rolls on for 10-15 s, a surging "freight train"
  tornado with a deafening close-range roar, tyre and road rumble by surface, wipers, footsteps,
  the truck's own wind noise at speed, rain on your hood when on foot, and the phone's real WEA
  alert cadence.
* **Your own sounds and music: `Sound Studio.html`** (next to the EXE; open it in Chrome or Edge).
  Every sound in the game is listed by name ("Raindrops on the roof", "Road step 1", "Engine 2000
  rpm"...): drag an `.mp3`, `.wav` or `.ogg` onto it, then click **Sync to game** and pick the
  game folder (once). The files go into `audio_override` next to the EXE, and a running game picks
  them up within a couple of seconds. You can also add **Main menu music** and **Driving music**
  (volume: Settings → Audio → Music). "Use built-in sound" puts the original back.
* Anti-aliasing defaults to SMAA: sharp edges with no ghosting while driving (TAA is still in
  Settings if you prefer its smoother, softer look).

## What is in it

| Area | Highlights |
| --- | --- |
| World | A procedural 300 x 300 mile (483 km) map: one analytic land function (biomes, relief, rivers and creeks, the road grid, towns, farms, crop fields) evaluated on the GPU for the terrain, grass and maps and mirrored on the CPU; ground colliders baked on the GPU in 1 km squares around the truck; a floating origin; objects streamed in 1 km squares (farmsteads with houses, barns, sheds, bins, silos, windbreaks; town blocks, main-street storefronts, churches; creek and river timber, woodland groves, junipers on the breaks, hedgerows; power lines with sagging wires; fences; bales; stop signs; street and yard lights that switch on at dusk and under storm gloom) and landmarks (wind farms, grain elevators, water towers) streamed farther out; six gas stations; near-camera grass, wheat and corn rows that bend in the wind field |
| Storm | One deterministic storm model (closed-form function of time) drives volumetric clouds, rain shafts, wall cloud, clear slot, shelf cloud on the rear-flank gust front, tornado (rope to wedge to multi-vortex, debris sheath), wind on the truck, sound and radar. A connected, broken layer of cumulus / stratocumulus (cloud streets along the low-level wind, flat bases, cauliflower tops) fills the warm sector, with mid-level cloud aloft; distant storms carry anvils |
| Rendering | Half-resolution compute ray-marcher composited by depth; cloud-shadow map on the ground; lightning; rain and hail particles; lens and windshield rain with wipers; cracked windshield |
| Radar | NEXRAD-style S-band site (14 tilts, 4-min volumes that arrive ~70 s late) and a deployable X-band mobile radar (30 s volumes, 75 m gates, rain attenuation). Products: REF, VEL, SRV, CC, ZDR, SW. Classic supercell structure: hook echo, inflow notch, 65+ dBZ hail core, streaky forward flank, BWER aloft, debris ball with a CC drop (TDS), ZDR arc and column, turbulent velocity texture. Legends, zoom, pan, cursor readout with beam height, mesocyclone / TVS / debris / hail / storm-track algorithms, warning polygons, archive with timeline, loop, step, speed and return to live, HUD mini radar |
| Gameplay | Free roam; photos judged on what is actually visible (rain-wrapped tornadoes don't count), probes that record pressure and wind, spotter reports, automatic mobile-mesonet samples, debris and hail damage, rollovers, tornado damage to trees and buildings with flying debris and an EF damage survey; get out and chase on foot in first person |
| Audio | All procedural (synthesized offline in Python from first principles): wind (rumble, gusty whoosh, howl, grass, and leaves near trees, brighter in the gusts), rain on the roof (distinct taps in light rain, drumming when it pours) and windscreen, hail, thunder from simulated lightning channels (a tearing crack before the boom when it is close), tornado roar and debris, V8 engine by firing order with intake roar under load, tyres by surface (asphalt, gravel, crops/grass, mud, wet), sirens, UI. Every layer fades smoothly; nothing pops in |

## Project layout

```
core/        settings, game flow, utilities, constants
scenarios/   seeded scenario generator and config
weather/     storm model (CPU), GPU field mirrors, volumetric renderer, lightning, precipitation
world/       the land function (land.gd), roads, grass, instancing; world/big: the 300-mile world
             (GPU ground bakes, clipmap terrain, grass classifier, object streaming)
models/      procedural mesh builders: vehicle, buildings, trees, props
vehicle/     chase vehicle physics and camera rig
radar/       radar system (schedules, archive, CPU product mirror, detections), PPI shader, palettes
gameplay/    chase session, visibility, damage system, debris
ui/          menus, HUD, radar panel, map, report, pause/help, overlays and their shaders
audio/       audio director and generated sounds (tools/audio/synth.py)
materials/   shaders and generated textures (tools/textures/*.py)
tests/       automated checks and visual harnesses
docs/        SCIENCE.md (models and approximations)
```

## Building

Godot 4.7.2 with the Windows export templates. From the project folder:

```
Godot_v4.7.2-stable_win64_console.exe --headless --path . --export-release "Windows Desktop" ../tornado-chaser-build/TornadoChaser.exe
```

Generated assets can be rebuilt with `python tools/textures/gen_textures.py`,
`python tools/textures/gen_noise3d.py` and `python tools/audio/synth.py` (numpy + Pillow).

## Tests

Run from the project folder (`Godot` = the console executable):

| Test | Command |
| --- | --- |
| Every script and shader compiles | `Godot --path . res://tests/check_scripts.tscn` |
| Same seed, same day (scenario, storm, roads, terrain, world) | `Godot --headless --path . res://tests/determinism_test.tscn -- --seed=96028` |
| CPU and GPU land function agree (height, roads, towns, crops) | `Godot --path . res://tests/land_consistency.tscn -- --seed=5 --origin=196608,-114688` |
| Ground bake on the GPU matches the land, without frame hitches | `Godot --path . res://tests/land_bake_test.tscn` |
| Storm fields CPU vs GPU | `Godot --path . res://tests/field_consistency.tscn` |
| Streaming test drives | add `--glide=SPEED` (slide the truck over the land), `--shift_test=T` (move the origin and back), `--tor_time=S` (start S s after the first tornado forms, beside its path), `--fuel=F` to a harness run; views `goto_town`, `goto_gas`, `refuel`, `map_far`, `river`, `station` |
| CPU and GPU radar products agree gate by gate | `Godot --path . res://tests/radar_consistency.tscn -- --seed=96028 --time=900` |
| Screenshot harness | `Godot --path . res://scenes/game.tscn -- --seed=N --time=T --shots=6,9 --view=x,chase,storm --out=DIR --quit=10` |
| Record the game mix | add `--audio_rec=FILE.wav` (and `--audio_log` for layer gains) to any harness run |
| Manual gearbox drive (test harness) | `Godot --path . res://scenes/game.tscn -- --seed=N --drive_manual --quit=24` |
| Storm-only visual harness | `Godot --path . res://tests/storm_view_test.tscn -- --seed=N --time=T "--views=tor:1500:200:8:0" --out=DIR` |

## Known limitations

* The storm is a parametric (kinematic) supercell, not a numerical weather model; see
  `docs/SCIENCE.md` for what is and isn't simulated.
* The volumetric renderer is the main GPU cost. On an RTX 4080 SUPER at 1080p (with streaming
  software running) Ultra holds ~60-70 fps with the adaptive clouds (~48 fps if they could not
  adapt), and ~110 fps with clouds off. Lower presets reduce cloud steps and resolution.
* Very distant small cumulus right at the horizon can still look slightly speckled.
* Everything standing can be damaged by tornadoes (EF-scale damage indicators): trees, every
  building type, wind turbines, power poles and their wires, fences, signs, street lights, bales
  and mailboxes. Damage stays when you drive away and come back, and a square that loads after a
  tornado went through it out of sight is found wrecked along its track.
* Rivers run roughly west to east across the map and never join (no tributary networks).
* The procedural audio has been checked numerically (levels, spectra, spectrograms, loops, recorded
  in-game mixes and stems), not by ear.
