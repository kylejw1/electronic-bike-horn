# Beeps by K — PCB enclosure

Two-part snap-together box for an audio amp board, an SV5W MP3 board and a
radial reservoir capacitor.

## Files

| file | what it is |
|---|---|
| `PCB enclosure base.sc` | CAD model — SolidCraft timeline, every feature editable |
| `PCB base.stl`, `PCB lid.stl` | print meshes, fine tessellation (24,176 / 4,570 tris) |
| `PCB enclosure.3mf` | both parts in one file, named, mm units |
| `as_built.gcode` | sliced base, OrcaSlicer 2.4.2, 130 layers @ 0.2 mm |

## Size

105 × 80 × 26 mm outer, 29 mm tall with the lid on. 2.5 mm walls and floor,
cavity 100 × 75 × 23.5, R6 outer / R3.5 inner corners.

## Layout

X right, Y back, Z up, origin at the outer front-left corner.

| item | placement |
|---|---|
| Amp board 45 × 53, Ø3.5 holes @ 39 × 46 | bosses (10, 11.5) (49, 11.5) (10, 57.5) (49, 57.5) |
| MP3 board 40 × 40, Ø3.0 holes @ 35 | clipped bosses (60.5, 10.5) (95.5, 10.5) (60.5, 45.5); plain Ø6 support at (95.5, 45.5) — that corner has no hole |
| Cap Ø19 × 31 | two C-clips, axis along X at y = 64, z = 13.25, 8 mm wide, x 60–68 and 83–91 |
| 2 cables | Ø6.5 holes through the front wall, x = 25 and x = 85, z = 15 |
| Lid snap | 4 notches 10 × 1, 0.8 deep, z 22–23, one centred per wall |

Boards rest at z 7.0 — 4.5 mm above the floor for solder joints — tops at 8.6.

## How the clips work

**Board bosses.** Ø6 pad to z 7.0, then a Ø3.3 (amp) / Ø2.8 (mp3) post through
the hole, ending in a ramped head Ø4.3 / Ø3.8 whose underside sits 0.05 mm above
the board's top face. A 1.2 / 1.0 mm slit lets the two halves squeeze ~0.4 mm per
side as the board presses down, then spring back under it. Press on, pry off.

**Cap cradle.** C-clips with a Ø19.6 bore and an 18.4 mm mouth (0.3 mm squeeze
per side), 2 mm ring wall, 8 mm wide, on an 8 × 24 × 4 foot. The arms stop flat
at z 17.5, so the ring ovalises instead of bending thin tips.

**Lid.** 3 mm plate on the rim, 1.8 × 6.5 skirt with 0.15 clearance, four 10 mm
bumps with 0.65 engagement into the notches — square shoulder, 0.35 × 45° lead-in.

## Clearances that matter

- cap top 22.75 vs lid underside 26 → 3.25 mm of headroom
- cap to MP3 board 6.5, to the back wall 4.0, skirt inner face to cradle 1.7
- lid bumps ride 0.65 under the wall face with 0.05 mm vertical play

## Label

"BEEPS BY K" in small caps — B and K at 8 mm, EEPS and BY at 6.2 mm on one
baseline, normal kerning, block 55 mm wide centred on the lid. Debossed 0.4 mm
into the 3 mm plate (leaves 2.6 mm under it).

## Printing

- Base upright, lid outside-face-down, no supports either way.
- 0.2 mm layers, 3 perimeters, 15 % infill.
- Holes print tight? Run a 3.5 / 3.0 mm drill through the clip heads, don't force them.
- The base STL carries ~90 hairline seams from per-face tessellation; slicers
  close them on import and the volumes match the CAD (44.31 / 29.07 cm³).

## Editing

Every feature is a plain timeline entry in the `.sc` — double-click one to change
its numbers. Parameters worth knowing: board thickness assumed 1.6 mm, cable
holes 6.5 mm, cap lying horizontally rather than standing.

## The tunnel

SolidCraft's control channel, tunnelled back to rdev:

    ssh -N -R 27878:localhost:27878 192.168.1.204

The app listens on 27878 by default; its launch token sits beside the app data.
The agent drives it with one JSON object per line (`engine.execute`,
`engine.batch`), or through `solidcraft-cli mcp --connect 127.0.0.1:27878`.
