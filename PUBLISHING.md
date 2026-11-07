# Publishing

Store copy and checklist for **Empty Hulls**. Both stores are uploaded through the **Paradox
Launcher** (Mod Tools → Upload Mod). Only `empty_hulls/` ships. `assets/` holds the thumbnail
source (`thumbnail.svg`, our own art, rendered with
`rsvg-convert -w 512 -h 512 assets/thumbnail.svg -o empty_hulls/thumbnail.png`) and the
store screenshot `designer-corvette.png`: the only one, cropped from the game's own F12 shot
`2026_11_07_3.png` to the ship designer (`magick <shot> -crop 1275x635+38+50 +repage <out>`).

## Checklist (first release, 1.0.0)

- [x] At game start, `S (empty)` appears for a regular empire (corvette) and a bio empire
      (Mauler); a bio origin that starts with Weavers gets the Weaver design too.
- [x] Auto-upgrade unticked; the corvette costs 60 alloys against 110 for the auto-generated one
      (`assets/designer-corvette.png`).
- [ ] Not yet seen in game: `M`/`L (empty)` after `research_technology tech_harbingers` /
      `tech_stingers`; a grown Mauler stays empty; a deleted design doesn't come back; a save
      from before the mod gets the designs at the next month (`AGENTS.md`, "open checks").
- [x] Discord forum `empty-hulls`, invite `ufKQUpgAPx` (2026-11-07), in the store texts below and
      in `README.md`.
- [x] `picture="thumbnail.png"` (512×512, our own art), tags, `version="1.0.0"`.
- [ ] `ls -A empty_hulls` lists only `common/ descriptor.mod events/ localisation/ thumbnail.png`
      (the launcher uploads everything, including a stray `.claude/`).
- [ ] Launcher closed → `scripts/link-mod.sh stellaris-mod-EmptyHulls/empty_hulls` → launcher
      open. On Linux the upload dialog may not see a **symlinked** mod: then copy the folder into
      `<user dir>/mod/` and upload the copy.
- [ ] Upload to **Steam Workshop** (description: BBCode below, then the "More from me" block from
      `../docs/store-more-from-me.md` without this mod's line). Add `assets/designer-corvette.png` on the
      item's page (both stores). A first upload starts **Hidden**: set it Public. The launcher writes
      `remote_file_id` into `descriptor.mod`: commit it.
- [ ] Upload to **Paradox Mods** (plain text below; format headings, lists and links with the
      website editor, then check the saved page).
- [ ] IDs into the table below and into `../docs/store-more-from-me.md`; re-paste the "More from
      me" blocks into every listed mod.
- [ ] GitHub repo public (`gh repo edit mkoester/stellaris-mod-EmptyHulls --visibility public
      --accept-visibility-change-consequences`); the store texts don't link it, the README does
      no harm.

## Published IDs

| Store | Item ID | URL |
|---|---|---|
| Steam Workshop | – | – |
| Paradox Mods | – | – |

---

## Store description — Steam Workshop (BBCode)

```bbcode
[h1]Empty Hulls[/h1]

Weaponless ship designs, ready from day one, so you don't have to build them by hand in every
campaign.

An empty hull is the cheapest ship you can build. It's good for:
[list]
[*][b]Power projection.[/b] It takes the same naval capacity as an armed ship, and the naval capacity you use counts toward power projection and your monthly influence. At a fraction of the price.
[*][b]Early exploration.[/b] Send single ships out to look around, without paying for guns.
[*][b]Bio ships.[/b] Build the young hull and let it grow, instead of paying for a grown one. Every growth stage of the design is empty, so it stays empty as it grows.
[/list]

[h2]What you get[/h2]
[list]
[*][b]S (empty)[/b]: a Corvette, or a Mauler if your empire uses bio ships. At game start.
[*][b]W (empty)[/b]: Weaver, once Weavers are available.
[*][b]M (empty)[/b]: Harbinger, once Harbingers are available.
[*][b]L (empty)[/b]: Stinger, once Stingers are available.
[/list]
Only the parts every ship must carry (reactor, thrusters, sensors, FTL, combat computer), at
their first tier, with your empire's own FTL. Auto-upgrade is off, so they stay cheap: the
corvette costs 60 alloys, against 110 for the game's starting corvette. Switch auto-upgrade on
in the designer if you prefer.

[h2]Good to know[/h2]
[list]
[*]Each design is added once. Delete it and it stays deleted. Edit it as you like.
[*]Players only: AI empires get nothing.
[*]Works on running saves: the designs appear at the start of the next month.
[*]The names are fixed. A mod can't read or set a design's name, so if you already have a design called "S (empty)", you get a second one.
[/list]

[h2]Compatibility[/h2]
[list]
[*]Built for Stellaris 4.5.x. BioGenesis is needed only for the bio designs.
[*]Changes no vanilla files: it adds five ship designs, one hidden event and three on_action hooks.
[*]Changes the checksum: no achievements or Ironman while it is active.
[/list]

[h2]Bugs & feedback[/h2]
Post them in the [url=https://discord.gg/ufKQUpgAPx]empty-hulls forum on Discord[/url].

[i]Unofficial fan project, not affiliated with Paradox Interactive.[/i]
```

---

## Store description — Paradox Mods (plain text)

```text
Empty Hulls

Weaponless ship designs, ready from day one, so you don't have to build them by hand in every campaign.

An empty hull is the cheapest ship you can build. It's good for:
• Power projection. It takes the same naval capacity as an armed ship, and the naval capacity you use counts toward power projection and your monthly influence. At a fraction of the price.
• Early exploration. Send single ships out to look around, without paying for guns.
• Bio ships. Build the young hull and let it grow, instead of paying for a grown one. Every growth stage of the design is empty, so it stays empty as it grows.

What you get
• S (empty): a Corvette, or a Mauler if your empire uses bio ships. At game start.
• W (empty): Weaver, once Weavers are available.
• M (empty): Harbinger, once Harbingers are available.
• L (empty): Stinger, once Stingers are available.
Only the parts every ship must carry (reactor, thrusters, sensors, FTL, combat computer), at their first tier, with your empire's own FTL. Auto-upgrade is off, so they stay cheap: the corvette costs 60 alloys, against 110 for the game's starting corvette. Switch auto-upgrade on in the designer if you prefer.

Good to know
• Each design is added once. Delete it and it stays deleted. Edit it as you like.
• Players only: AI empires get nothing.
• Works on running saves: the designs appear at the start of the next month.
• The names are fixed. A mod can't read or set a design's name, so if you already have a design called "S (empty)", you get a second one.

Compatibility
• Built for Stellaris 4.5.x. BioGenesis is needed only for the bio designs.
• Changes no vanilla files: it adds five ship designs, one hidden event and three on_action hooks.
• Changes the checksum: no achievements or Ironman while it is active.

Bugs & feedback
Post them in the empty-hulls forum on Discord: https://discord.gg/ufKQUpgAPx

Unofficial fan project, not affiliated with Paradox Interactive.
```
