# Tweeter horn — handoff

Updated 2026-11-10 19:18 (America/Edmonton) by the DSH agent.

**Current design: `/home/kyle/dev/horn/tweeter-horn-v2.sc`** — 18 features, saved 19:15, no errors. **M56×2 thread, 6.5 mm engagement (3.25 turns), overall length unchanged at 61.5 mm.**

| file | status |
|---|---|
| `tweeter-horn-v2.sc` | **current** |
| `tweeter-horn-v2-snap.sc` | the snap-bead version, kept as a fallback |
| `Tweeter horn v3.sc` | obsolete pre-update threaded attempt |
| `tweeter-horn.sc` | v1, the original part — superseded |

---

## 0. TL;DR

| | |
|---|---|
| overall | Ø62 × **61.5** (z −6.5 … 55) — **unchanged** from the last round |
| base / cap OD | 62 |
| cavity | Ø50.4 × **18.5** deep (seat at z −0.5) |
| thread | **M56×2, 6.5 mm ≈ 3.25 turns** (was 3.5 mm ≈ 1.75 turns) |
| volumes | Horn **45,513.0 mm³** (59 g), Cap **18,264.7 mm³** (24 g) |
| mesh | Horn 45 faces, Cap 22 faces — threads are modelled, not cosmetic |

## 1. What the user asked for this round

> the threads dont seem long enough though. Can we give up a little from the collar end to give to the cap, and cut in beside the handlebar mount so we dont have to make it overall longer

Solved by **moving the thread upward instead of making the part longer**:

- **The horn gives up its collar-end diameter.** Above the collar, the horn's wall was Ø62. A `Cap shoulder` cut takes the horn's OD down to **Ø55.6 for z −4 … +2.5**, so the collar is now a 6.5 mm long Ø55.6 stub instead of a 3.5 mm one. Nothing was added to the length — the horn's bottom still ends at z −4.
- **The cap takes it.** The cap's rim now runs from z −6.5 up to **z +2** (8.5 mm tall) with a 6.2 mm deep Ø56.6 bore — the thread has 6.5 mm to work with, and the cap's face (the tweeter's seat) is still at **z −0.5**, so the cavity is unchanged at 18.5 mm.
- **The mount gets a notch, kept tight.** Because the cap's rim now rises 2.5 mm above the base's bottom face, the `Cap shoulder` cut also clears the underside of the handlebar block between **r 27.8 and r 31.5** for z −0.5 … +2.5. That is only **0.5 mm wider than the cap's Ø62 rim**, so the block's underside drops back down to z 0 immediately outside the cap instead of being cut back to r 40. (First cut at r 40 and the user asked for it closer to the cap; narrowed on request.)

The outer silhouette is the same as before: Ø62 from z −6.5 all the way up, with the cap's top edge hidden under the mount's notch.

## 2. How the joint goes together

```
z  +2.0   cap rim top   ── butts nothing, sits 0.5 under the shoulder at +2.5
z  +2.5   horn shoulder ── horn's OD steps back out to Ø62
z  −0.5   tweeter seat  ── cap's face; cavity 18.5 deep to the plate at z 18
z  −4.0   collar bottom ── horn's Ø55.6 stub ends
z  −4.2   cap groove floor
z  −6.5   cap bottom
```

- Collar: Ø55.6 (skimmed from Ø56 for printed clearance), threaded M56×2, 6.5 mm.
- Cap: bore Ø56.6, auto-narrowed to Ø53.835 by the thread tool, then threaded M56×2, 6.2 mm.
- Clearance: **0.2 mm radial** at the crest/root, as before.

## 3. Timeline (18 features)

1. `Horn profile` → 2. `Horn` (revolve)
2. `Bar mount`, `Bar saddle`, `Wire channel`, `Tie tunnel`
3. `Collar skim` — collar Ø56 → Ø55.6
4. `Cap end extension` — horn's bottom face to z −0.5, collar to z −4
5. `Cap shoulder` — horn OD to Ø55.6 for z −4 … +2.5, and the notch (r 27.8 … 31.5) beside the mount
6. `Cap profile` → `Cap` (revolve, rim to z +2)
7. `Collar thread` — M56×2, tip start
8. `Cap thread` — M56×2

## 4. Warnings you will see (both harmless)

- **`Collar thread`**: *"the thread's groove could not be run down to the shoulder here, so it stops clear of it and its last turn is left uncut"* — the horn's shoulder at z +2.5 is where the OD steps back out; the tool eases out before it instead of cutting into it. Correct behaviour.
- **`Cap thread`**: *"narrowed the 56.6 mm hole to 53.834936 mm (the M56x2 thread's minor diameter) so the thread has material to cut into"* — the tool adds material to the bore before cutting. Expected.

## 5. Traps

- **A fixed point cannot be moved** — `sketch.transform` refuses points made from numbers or expressions; rebuild the sketch instead.
- **`profiles: all` on two concentric circles cuts both regions** (it amputates a ring) — revolve a closed polygon for annular cuts.
- **`join`/`cut` with `operation` merges every body it touches** — always pass `targets`.
- **`browser.visibility {visible:true, items:["Cap"]}` hid the Horn** in this build — pass each body explicitly if one disappears.
- **`solid.chamfer` refuses circular edges**; **`solid.revolve` needs its axis to be a sketch line**.
- **Save is manual**; `save {}` after every change.
- **MCP allow-path** is still `/home/kyle/dev/battery` in `cordis.patch.yml`.

## 6. Files

| file | what it is |
|---|---|
| `tweeter-horn-v2.sc` | **current design**, 18 features |
| `Horn-v2.stl`, `Cap-v2.stl` | current exports (1.0 MB / 460 KB) |
| `tweeter-horn-v2-hero.png` | assembled — note the cap's rim tucking under the mount's notch |
| `tweeter-horn-v2-section.png` | cutaway at x = 0 |
| `tweeter-horn-v2-thread.png` | close-up of the 6.5 mm thread |
| `tweeter-horn-v2-snap.sc` | previous snap-bead version |
| `Tweeter horn v3.sc`, v1 files | obsolete — safe to delete |

## 7. Next steps

1. Print both, check the cap screws on and the tweeter sits flush with 18.5 mm of cavity.
2. If the thread is tight or loose, change the collar skim radius (27.8 now): lower = looser, higher = tighter — the cap's thread stays.
3. If 3.25 turns still feels short, the cap's rim can go up another 1.5 mm (to z +3.5) before the cap's rim reaches the horn's shoulder, with the same notch extended.
