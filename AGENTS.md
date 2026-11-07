# Empty Hulls

Stellaris mod (game **4.5.x**): weaponless "S/M/L/XL (empty)" designs given to human empires
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

## Status (2026-11-07): written, not yet run in game

To check in game (new game; console `research_technology tech_weavers` etc. for the bio hulls):
1. Do the designs appear in the ship designer and build list with their names, valid and
   buildable?
2. Does the game auto-upgrade their components or mark them obsolete? Either is fine; note which.
3. Does an `S (empty)` Mauler grow to stage 2/3 and stay empty?
4. Can the player edit, copy and delete them? Once deleted, a design must not come back.
5. A save from before the mod: the designs appear once, at the next month.
6. Does building one raise power projection (influence tooltip)?
Then `error.log` must have no `ehu_` / `EHU_` lines. Copy `logs/` before restarting the game: it
is rewritten at each launch.
