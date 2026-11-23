# Empty Hulls

Stellaris mod (game **4.5.x and 4.6.x**): weaponless "S/W/M/L (empty)" designs given to human empires
(behaviour and layout: `README.md`). Workspace context: `../AGENTS.md`. Public since
2026-11-07 (1.0.0); store texts, IDs and release checklist: `PUBLISHING.md`.

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

- `create_ship_design = { design = <global design name> }` then
  `add_ship_design = last_created_design` gives an empire a design defined in
  `common/global_ship_designs/` (vanilla: `biogenesis_effects.txt`, `NAME_Starlit_Starbase`).
  The script docs offer `ftl = <country>`, but 4.5.4 rejects it at load (`Unexpected token:
  ftl`, 5× per game start, seen 2026-11-18); dropped in 1.0.1, the designs keep `HYPER_DRIVE_1`.
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

## Status (2026-11-07): 1.0.0 released on both stores

**1.0.1 (2026-11-18): committed, not uploaded, not yet seen in game** — drops `ftl = this`
("How it works"). Check on the next game start: no `ehu_` line in error.log, designs still granted.

Seen in game (screenshots `2026_11_07_3.png` regular, `_4.png` bio, in the game's own folder):
- The designs appear and are valid. A bio origin that starts with Weavers gets the Weaver
  design on day 1 (still named `M (empty)` then, before the W/M/L rename).
- Auto-upgrade box unticked. The corvette costs 60 alloys, upkeep 1.07 energy and 0.49 alloys,
  against 110 / 1.51 / 0.58 for the auto-generated starting corvette.

Still open (none blocks the release; check when convenient, new game, console
`research_technology tech_harbingers` / `tech_stingers`):
1. `M`/`L (empty)` appear with their new names after the tech.
2. The parts stay tier 1 after new thruster/reactor techs.
3. An `S (empty)` Mauler grows to stage 2/3 and stays empty.
4. A deleted design does not come back.
5. A save from before the mod gets the designs once, at the next month.
6. Building one raises power projection (influence tooltip).
Then `error.log` must have no `ehu_` / `EHU_` lines. Copy `logs/` before restarting the game: it
is rewritten at each launch.

Seen in the user's campaign (Roaming Cybergang, Workshop 1.0.0, read 2026-11-22): `Unexpected
token: ftl` still 5× per load (the 1.0.0 error, so 1.0.1 is still owed to the stores); `S`
corvette, `S` Mauler and `W` Weaver designs held. Point 1 is not answered there: the player got
Harbingers between 2234.10 and 2241 while the game was observed, and the grant is human-only
(`is_ai = no`) — so no `M (empty)` yet. With `play 0`, the next monthly pulse should grant it.

## Releasing an update

Bump `version` in `descriptor.mod` (own `chore:` commit), keep `remote_file_id`, and follow the
checklist in `PUBLISHING.md`: same launcher upload, it updates the existing items.
