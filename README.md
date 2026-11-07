# Empty Hulls

A Stellaris mod (game **4.5.x**): human empires get weaponless ship designs automatically, the
ones many players build by hand at the start of each campaign.

| Design | Hull | When |
|---|---|---|
| `S (empty)` | Corvette | game start (empires without bio ships) |
| `S (empty)` | Mauler | Maulers researched (bio ships, usually at start) |
| `M (empty)` | Weaver | Weavers researched |
| `L (empty)` | Harbinger | Harbingers researched |
| `XL (empty)` | Stinger | Stingers researched |

What they are for:
- **Cheap power projection**, which feeds monthly influence.
- **Early exploration** with single unarmed ships.
- **Bio ships**: build the stage-1 hull and let it grow. Every growth stage of the design is
  empty, so a grown ship stays empty.

The designs carry only the required components, at tier 1 (cheapest); the FTL drive is your
empire's own. Auto-upgrade is off, so the parts stay tier 1. Each design is added once per empire. If you delete one, it stays deleted. AI
empires get none. Adding the mod to a running save works: the designs appear at the next month.

Design names are fixed. A script cannot read or set a design's name, so the mod can't add a
suffix when the name is already taken.

Additive: no vanilla file is overridden. Achievement compatibility: not with any gameplay mod.

## Layout

- `empty_hulls/` — the mod (only this folder ships).
  - `common/global_ship_designs/ehu_designs.txt` — the five designs.
  - `common/scripted_effects/ehu_effects.txt` — `ehu_grant_designs`, one flag per design.
  - `common/on_actions/ehu_on_actions.txt`, `events/ehu_events.txt` — game start, each tech,
    monthly; human empires only.

Unofficial fan project, not affiliated with Paradox Interactive. Stellaris and its game data are
Paradox's.
