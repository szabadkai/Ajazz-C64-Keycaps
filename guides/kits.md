---
title: Keycap kits: what to print for each board
summary: Which keycap groups and parts make up each legend option (C64, plain, blank) and each ANSI board size (60%, 65%, 75%, TKL, full size, tsangan).
keywords: kit, layout, 60%, 65%, 75%, tkl, full size, tsangan, print files, which keys
always: true
---

# Keycap kits: what to print for each board

All caps are SA profile with MX stems. Rows: **R1** = F row and number row, **R2** = Q row,
**R3** = home row (also the spacebars and the upright numpad + / Enter), **R4** = shift and bottom rows.
Every legend cap prints together with its inlay (`ink_<part>`, set with printWith), so it is one object
in the 3MF. Blanks have no inlay.

## Legend options (assembly groups)

| Option | What to print | Caps |
|---|---|---|
| C64 | the original Ajazz 75% set (the parts in no group: `k_*`, `key_*`) + group `c64_addon` | 75% set + 37 add-on |
| Plain | groups `plain_full` + `plain_extras` | 104 + 15 |
| Blank | groups `blank_full` + `blank_extras` | 104 + 13 |

`c64_addon` = TKL nav (PrtSc, ScrLk, Pause, Ins, Home, PgUp R1, Del/End/PgDn R2), the 17-key numpad,
full-size right mods (2.75u Shift, 1.25u Alt / Win / Menu / Ctrl) and tsangan mods (1.5u Ctrl ×2,
1.5u Alt ×2, 1u C=, 7u space).
`plain_extras` / `blank_extras` = tsangan row (1.5u Ctrl ×2, 1u Win, 1.5u Alt ×2, 1u Fn, 7u space) and
the 65%/75% row (1.75u right Shift, 1u Alt / Fn / Ctrl, Del R1, PgUp R2, PgDn R3, End R4).

## Per board (ANSI)

| Board | From the full-size group | Plus |
|---|---|---|
| 60% | number row with 2u Backspace, Q row, home row, shift row (2.25u + 2.75u Shift), bottom row (1.25u ×7, 6.25u space) | Esc instead of ` if the board puts Esc there |
| 65% | 60% without the 2.75u Shift and the right 1.25u mods; arrows ↑ ← ↓ → | extras: 1.75u Shift, 1u Alt / Fn / Ctrl, Del R1, PgUp R2, PgDn R3, End R4 |
| 75% | 65% + Esc and F1–F12 | one more R1 key top right (Del, Ins or Home from the full set) |
| TKL | everything except the 17 numpad keys | — |
| Full size | everything in the full-size group | — |
| Tsangan bottom row | instead of the 1.25u bottom row | extras: 1.5u Ctrl ×2, 1u Win, 1.5u Alt ×2, 1u Fn, 7u space |

C64 option: the original set already is a 75%. For a 65% leave out the F row; for a 60% add the
2.75u Shift and 1.25u right mods from `c64_addon`; for TKL and full size add its nav cluster and numpad;
tsangan mods are in it too.

## Stabilizers

Every cap 2u and wider has stab stems at Cherry spacing: 23.8 mm on 2u, 2.25u and 2.75u
(`stab_2u`), 100 mm on 6.25u (`stab_625`), 114.3 mm on 7u (`stab_7u`). The numpad + and Enter are
the 2u cap turned upright, for vertical stabilizers.

## Files

- `exports/keycaps-<hash>.3mf`: every part as laid out, one object per cap with its inlay. Delete the
  groups you don't need in the slicer, or export single parts from the app.
- Plain legends currently use the C64 Keyboard font (caps only): the geometry server only loaded that
  font. Switch the plain set to Roboto Bold once it loads.

## Exporting one set at a time

Every part belongs to exactly one set (each set has its own spacebars: brown `k_space_7u` in the C64 add-on, light `p_space_6_25u` / `p_space_7u` in the plain set, `blank_space_*` in the blanks). To export one set as its own STEP and 3MF: in one temporary transaction, mark every part of the other sets `reference: "helper"` (and set their inks' `printWith: null`, since an inlay can't print with a construction body), export the whole design, then undo. Helper parts are left out of STEP and 3MF.

2026-10-25 exports (design before the temporary changes: sha256:72fcac111ec1912e):
- C64 75%: `exports/keycaps-7ce64e81.step` / `.3mf`
- C64 add-on: `exports/keycaps-85627423.step` / `.3mf`
- Blank: `exports/keycaps-e8ff5f65.step` / `.3mf`
- Plain: `exports/keycaps-bfd3f6cf.step` / `.3mf`
- C64 full set (75% + whole add-on: full-size ANSI with nav and numpad, plus tsangan mods and 7u space), 2026-10-29, same design: `exports/keycaps-d537c983.step` / `.3mf`
