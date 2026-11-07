# Empty Hulls

Stellaris mod (game **4.5.x**): weaponless "S/W/M/L (empty)" designs given to human empires
(behaviour and layout: `README.md`). Workspace context: `../AGENTS.md`. Private until it works.

Conventions, as in the sibling mods:
- Only `empty_hulls/` ships (symlinked into the game, uploaded to the stores); the top level is
  dev material. Register it with `scripts/link-mod.sh stellaris-mod-EmptyHulls/empty_hulls` from
  the workspace root, launcher closed.
- Prefix every key, id, flag and loc key with `ehu_` / `EHU_`. Additive, no vanilla overrides.
- Test in game on Linux (native build) only. Invalid triggers and effects show up only in
  `error.log`; check names against the game's `logs/script_documentation/`.
- General modding findings go to `../stellaris-modding-insights`: propose them, don't write them
  silently.

## How it works (from the 4.5.x script docs and vanilla files)

- `create_ship_design = { design = <global design name> ftl = <country> }` then
  `add_ship_design = last_created_design` gives an empire a design defined in
  `common/global_ship_designs/` (vanilla: `biogenesis_effects.txt`, `NAME_Starlit_Starbase`).
- **Design names can't be scripted:** `set_name` doesn't apply to designs, and no trigger compares
  a design's name, so a clash can't be detected (the suffix idea was dropped). The name is the
  global design's `name` loc key.
- Components needing no tech: `SENSOR_1`, `BIOSHIP_SENSOR_1`, the `*_COMBAT_COMPUTER_*_DEFAULT`
  family, and the bio unique slot's `<HULL>_STAGE_<n>_GROWTH_EMPTY` (stages 1–2) /
  `GROWTH_EMPTY` (stage 3). Thrusters, hyperdrive and fission reactors are start techs. Vanilla's
  `NAME_CHARGER_1` uses `MAULER_PURSUIT_1` there, which needs `tech_mauler_growth_1`.
- Combat computers are role-gated (`ship_uses_<role>_role`): Mauler swarm, Weaver buffer,
  Harbinger and Stinger artillery, matching the section template chosen.
- Reactor size by hull (`ship_uses_<size>_reactors`): Mauler corvette, Weaver destroyer,
  Harbinger cruiser, Stinger battleship.

## Prior art (searched 2026-11-07)

None found: `docs/prior-art.md` (the nearest mods, what they lack, and what wasn't searched).

## Test run 1 (2026-11-07, Earth start, 2200.01.01–02.01): no design

`error.log`: `Unexpected token: ftl = this } …` at game start, then at the monthly pulse
`invalid design for create_ship_design effect`. Cause: `design = "$DESIGN$"`. **A quoted
`$PARAM$` breaks the substitution even without a `|`**: the string runs on to the end of the
effect body. Fixed: unquoted, as vanilla writes it (`design = $GLOBAL_DESIGN$`,
`grand_archive_effects.txt`). No flag was set, so the same save should pick the designs up at its next month. The
design files themselves loaded without errors.

## Test run 2 (2026-11-07): designs present at game start

`S (empty)` appeared at game start for a regular empire and for a bio empire. Then the bio
designs were renamed `M/L/XL` → `W/M/L` (Weaver `W`, so that `M` and `L` fall to Harbinger and
Stinger), keys included. Only the `S` designs (keys unchanged) had been tested; `W/M/L` not yet.

## Status (2026-11-07): open checks

To check in game (new game; console `research_technology tech_weavers` etc. for the bio hulls):
1. Do the designs appear in the ship designer and build list with their names, valid and
   buildable?
2. Auto-upgrade is switched off (`set_auto_upgrade_components = no` on `last_created_design`):
   is the designer's auto-upgrade box unticked, and do the parts stay tier 1 after new techs?
3. Does an `S (empty)` Mauler grow to stage 2/3 and stay empty?
4. Can the player edit, copy and delete them? Once deleted, a design must not come back.
5. A save from before the mod: the designs appear once, at the next month.
6. Does building one raise power projection (influence tooltip)?
Then `error.log` must have no `ehu_` / `EHU_` lines. Copy `logs/` before restarting the game: it
is rewritten at each launch.
