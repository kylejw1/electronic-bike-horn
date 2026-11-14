# Tweeter horn — handoff

**Written 2026-11-13 21:40 (America/Edmonton), for whoever picks this up next.**

Current design file: **`/home/kyle/dev/horn/tweeter-horn-v2.sc`**
SolidCraft 0.30.x, millimetres. 20 features, all applied, nothing suppressed, marker at the end, saved 2026-11-10 19:29.

Print files already exported next to it: **`Horn-v2.stl`**, **`Cap-v2.stl`**.

This document supersedes `horn.md`, which is the running log of how the design got here.

---

## 1. What the part is

A bike-handlebar-mounted parabolic horn for **the tweeter from a 2012 VW Tiguan** — a Ø50 mm round body, 18 mm tall, with a 9 mm wiring notch on its side. It clamps to the bar with a zip tie, holds the tweeter in a cavity at the back, and is closed by a screw-on cap.

**A 2014 Tiguan tweeter fits with only minimal changes** — the cavity size (`cav_d`, `tw_h`, and `wire_w` if its notch differs). Nothing else in the part is affected: the horn flare, handlebar mount, zip-tie tunnel and thread all carry over unchanged.

**Driving it:** the horn is passive, so it needs an amplifier. The user reports it works well with an **MP3 board such as the DY-F20L running at 12 V or more**; **a 5 W board is too quiet**, and higher voltage may be better still. This is electrical — nothing in the model depends on it.

The user's brief (`prompt` in this folder, verbatim) asked for:
> It is to fit on a bike handlebar with a half moon shape containing a tunnel for a zip tie. The handlebar clamp part does not need to extend around the whole handlebar.
>
> I like the parabolic horn itself. […] fits a 50mm round tweeter that's 18mm tall. It has a cutout on the side for wiring that is 9mm wide tangential to the circular body, and starts 6mm from the top of the tweeter and finishes 5mm from the bottom.
>
> I want a cap for the back which will also need a cutout for the wiring. The cap should match the outer diameter of the base so where they meet will need a lip on one side and cutout on the other.
>
> The handlebar mount should […] just be one piece of plastic on the side of the parabolic horn which has a half moon cutout with the channel parallel

Later decisions that superseded parts of it:

- **The cap has no wiring cutout** — the wire leaves through the base's side slot, above the cap.
- **The cap is threaded** (M56×2), not a slip lip, after the user asked for threads.
- **The collar end is 0.5 mm longer** so the tweeter gets room; the cap end grew upward to keep the overall length.

## 2. The part as it stands

Axis is Z, mouth up, cap down. `z = 0` is the throat plate's underside (the tweeter's face).

| feature | value |
|---|---|
| overall | **Ø62 × 61.5 mm** (z −6.5 … 55) |
| mass | 82 g in PETG at 1.29 g/cm³ |
| base / cap outside Ø | 62 (flush) |
| tweeter cavity | Ø50.4, **18.5 deep** (seat at z −0.5, plate at z 18) |
| throat plate | 3 thick, Ø40 bore |
| bell | throat Ø40 at z 21 → mouth Ø62 at z 55, 34 long, 3 wall, two-arc smooth flare |
| wiring channel | 9 wide (y ±4.5), z 0 … 13, floor 1.2 mm inside the cavity wall so it cuts **through** into the cavity |
| mount | one block, x 26…46, y ±10, z 0…30 |
| bar saddle | Ø32 half-round, axis along Y through (x 56, z 16), cut through the block |
| zip-tie tunnel | Ø6.5, **revolved about the saddle axis** at R 21, 100° symmetric — it follows the cradle's curve, opening on the block's top and bottom faces |
| thread | **M56×2**, 6.5 mm engagement ≈ 3.25 turns |
| cap | Ø62, z −6.5 … +2, 8.5 tall, 6.2 deep Ø56.6 bore |

Measured volumes: **Horn 45,513.0 mm³** (44 faces), **Cap 18,264.7 mm³** (22 faces).

### The threaded joint, precisely

```
z  +2.5   horn shoulder      horn's OD steps back out to Ø62
z  +2.0   cap rim top        sits 0.5 under the shoulder
z  −0.5   tweeter seat       the cap's face; cavity is 18.5 deep above it
z  −4.0   collar bottom      horn's Ø55.6 stub ends
z  −4.2   cap groove floor
z  −6.5   cap bottom
```

- **Collar (male)**: horn's stub skimmed to **Ø55.6**, threaded `M56×2` over 6.5 mm, chamfered start (`tip: start`).
- **Cap (female)**: bore **Ø56.6**, which the thread tool narrows to Ø53.835 (the M56×2 minor) before cutting — that warning is expected.
- **Fit: 0.2 mm radial clearance** at the crest/root, 0.34 mm the other way. Screws on cold without forcing.
- **The notch beside the mount**: the horn's OD is cut from r 27.8 out to **r 31.5** for z −0.5 … +2.5, which clears the cap's rising rim under the handlebar block. 0.5 mm clearance to the cap on both sides, and it stops 0.5 mm outside the cap's Ø62.

## 3. Feature tree (20 features, in order)

| # | feature | what it does |
|---|---|---|
| 1–2 | `Horn profile` → `Horn` | revolved profile: cavity, plate, throat, bell, collar |
| 13–14 | `Bar mount` sketch → extrude | the handlebar block, joined |
| 15–16 | `Bar saddle` sketch → extrude | Ø32 cradle cut through the block |
| 19–20 | `Wire channel` sketch → extrude | 9 mm slot, z 0…13, through the cavity wall |
| 21–22 | `Tie tunnel` sketch → revolve | Ø6.5 tunnel revolved about the bar axis |
| 27–28 | `Collar skim` → revolve cut | collar Ø56 → Ø55.6 (printed thread clearance) |
| 33–34 | `Cap end extension` → revolve join | horn's bottom to z −0.5, collar to z −4 |
| 41–42 | `Cap profile` → `Cap` | the cap body (separate body) |
| 45–46 | `Cap shoulder` → revolve cut | horn OD to Ø55.6 for z −4…+2.5 **and** the notch beside the mount |
| 47 | `Collar thread` | M56×2, modelled |
| 48 | `Cap thread` | M56×2, modelled |

`Horn profile` is the only sketch with free dof (2, on the two arc control points). Every other sketch is fully fixed.

## 4. Parameters — how to tune it

All sketch geometry is driven by these, so most changes are a one-line edit. In SolidCraft: `set_parameter {name, value}` then re-save. **All of them are `model: false`, i.e. real user parameters.**

| name | value | effect |
|---|---|---|
| `tw_h` | 18 | cavity depth from the throat plate down to z 0 — **tweeter-fit knob** |
| `cav_d` | 50.4 | tweeter cavity Ø, 50 + 0.4 clearance — **tweeter-fit knob** |
| `base_d` | 62 | base and cap outside Ø |
| `plate_t` | 3 | throat plate thickness |
| `throat_d` | 40 | horn throat Ø |
| `mouth_d` | 62 | horn mouth Ø |
| `depth` | 34 | bell axial length |
| `wall` | 3 | bell / base wall |
| `wire_w` | 9 | wiring channel width |
| `cap_t` | 6 | cap body thickness (the cap is `cap_t + 0.5` tall) |
| `spig_t` | 3.5 | collar length below the base's bottom face |
| `bar_d` | 32 | handlebar Ø at the saddle |
| `tie_d` | 6.5 | zip-tie tunnel Ø |
| `block_x0`, `block_x1` | 26, 46 | mount block's inner / outer face |
| `block_h`, `block_w` | 30, 20 | block height / width |
| `bar_x`, `bar_z` | 56, 16 | saddle centre |

**Watch out:** `mouth_d` and `depth` also need the two bell arcs' *through* points moved (they are fixed numbers at (22.52, −38.35) and (25.52, −38.35)); changing the parameters alone distorts the flare.

**Fit adjustment:** the thread clearance lives in the **`Collar skim`** radius (27.8). Lower it by 0.1 for a looser fit, raise it by 0.1 for tighter. The cap's thread does not need to change.

## 5. History — what was tried and rejected

Keep this; several of these cost hours.

1. **v1** (`tweeter-horn.sc`, 19 features) — the original part, Ø76 threaded cap, huge. Never modified since the redesign. Superseded.
2. **v2 rebuild** — shorter, thinner, Ø60 slip-fit cap, one-piece mount. Printed.
3. **Threads, first attempt** (November 5) — `solid.thread` failed three times on the collar with *"planar boolean: This shell is not oriented and closed"*, each after 5+ minutes, on that SolidCraft build. **Fixed by a SolidCraft update**; it now takes about a second.
4. **Snap bead instead of threads** — a 0.5 mm bead on the collar and a matching indent in the cap. Worked, kept in `tweeter-horn-v2-snap.sc` if wanted.
5. **Threads, second attempt** — M56×2 both sides, works. Replaced the snap.
6. **Tweeter stood proud after printing** → the user wanted 0.5 mm more cavity depth. A **recess in the cap's face was rejected** ("don't move the seating depth"); instead the cap end was lengthened so the whole cap sits 0.5 deeper. That is how the current geometry came about.
7. **Thread felt short** (1.75 turns) → the cap's rim was extended *upward* to z +2 and the horn's OD stepped in to Ø55.6, giving 3.25 turns **with no change in overall length**. That is where the notch beside the mount comes from.
8. **Notch was too wide** (cut out to r 40) → narrowed to r 31.5.

## 6. SolidCraft traps hit on this design

- **`profiles: all` on a sketch of two concentric circles cuts BOTH regions** — it amputated the collar once. For an annular cut, revolve a closed polygon.
- **A point created from a number or expression is fixed** and `sketch.transform` refuses it ("fixed or projected geometry cannot move"). To shift a profile you must rebuild the sketch.
- **`operation: "join"` merges every body it touches** — always pass `targets: ["Horn"]` or the Cap gets swallowed.
- **`solid.revolve` needs its axis to be a sketch line** — `{origin, dir}` is refused even when geometrically correct. Draw a construction line.
- **`solid.chamfer` refuses circular edges** ("only straight edges can be blended") — model chamfers into the profile.
- **`browser.visibility {visible:true, items:["Cap"]}` also hid the Horn** in this build; re-show bodies individually.
- **Save is manual.** `save {}` after every change that applies.
- **A modelled thread narrows an oversize hole automatically** (warning says so) and **refuses a shaft thicker than the designation**, telling you the size to make it.
- **The MCP server's file access** is configured with `--allow-path /home/kyle/dev/battery` in `~/.dsh/profiles/web/cordis.patch.yml`. Saving into this folder only works because a design was opened/saved here in the same session; a fresh session needs that path changed (do it while the app is idle — editing that file hot-reloads the plugin).

## 7. Files

**Current**
- `tweeter-horn-v2.sc` — the design
- `Horn-v2.stl`, `Cap-v2.stl` — print files
- `tweeter-horn-v2-hero.png`, `-section.png` (cutaway), `-thread.png` (thread close-up), `-notch.png` (under the mount)
- `prompt` — the user's brief, verbatim

**History / superseded — do not print**
- `tweeter-horn-v2-snap.sc` — snap-bead version
- `Tweeter horn v3.sc` (+ `.bak`) — the failed threaded attempt on the old build; carries a 0.2 µm sliver
- `tweeter-horn.sc`, `tweeter-horn.sc.bak`, `.bak2` — v1
- `tweeter-horn-backup.sc` (25 MB), `.bak` (19 MB) — older backups, safe to delete
- `Horn.stl`, `Horn.stl.bak`, `Horn2.stl`, `Cap.stl`, `tweeter-horn-cap.stl`, `tweeter-horn.stl`, `tweeter-horn.step` — stale exports
- `tweeter-horn-iso.png`, `tweeter-horn-bottom.png`, `current-iso.png`, `tweeter-horn-v2-mount.png`, `-wire.png`, `-bottom.png`, `-snap.png` — stale renders

There are stale lock files (`.~tweeter-horn-v2.sc.lock`, `.~Tweeter horn v3.sc.lock`) which are harmless; SolidCraft clears them on a clean exit.

## 8. Open items

1. **Print and test** the current pair: cap should screw on by hand, tweeter should sit flush with 18.5 mm of cavity.
2. **2014 Tiguan variant** — the design is built around the 2012 Tiguan tweeter and said to fit the 2014 one with minimal changes, but **the 2014 unit's actual dimensions are not recorded here**. Measure its body Ø and height, then set `cav_d` and `tw_h` (and `wire_w` if its wiring notch is a different width); nothing else should need touching. Re-export both STLs if the cavity changes.
3. **Thread length** — 3.25 turns is workable but not generous. The cap's rim can rise another 1.5 mm (to z +3.5) with the same notch extended, without making the part longer.
4. **Fit** — adjust via the `Collar skim` radius as in §4.
5. **The zip-tie tunnel direction** was never explicitly confirmed: it currently runs vertically through the block, behind the bar, so the tie wraps the bar in the plane of the saddle. If the user meant it parallel to the bar, it needs changing.
6. **Clean up** everything under "History / superseded" once the print is signed off — the two big backups alone are 44 MB.
