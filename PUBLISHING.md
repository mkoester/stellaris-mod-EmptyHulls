# Publishing

Store copy and checklist for **Empty Hulls**. Both stores are uploaded through the **Paradox
Launcher** (Mod Tools → Upload Mod). Only `empty_hulls/` ships. `assets/` holds the thumbnail
source (`thumbnail.svg`, our own art, rendered with
`rsvg-convert -w 512 -h 512 assets/thumbnail.svg -o empty_hulls/thumbnail.png`) and the
store screenshot `designer-corvette.png`: the only one, cropped from the game's own F12 shot
`2026_11_07_3.png` to the ship designer (`magick <shot> -crop 1275x635+38+50 +repage <out>`).

## Update 1.0.2 (game 4.6.0, 2026-11-23)

No code change: 4.6 left every component, section template and hull the mod uses as it was.
- [x] `version="1.0.2"`, `supported_version="v4.6.*"`; store copy says 4.5.x and 4.6.x.
- [x] Loaded in the 4.6.0 campaign: nothing of the mod in `error.log`.
- [ ] Upload to both stores. Change note: "Supports Stellaris 4.6 (Willpower). No other change."

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
- [x] `ls -A empty_hulls` lists only `common/ descriptor.mod events/ localisation/ thumbnail.png`
      (the launcher uploads everything, including a stray `.claude/`).
- [x] Launcher closed → `scripts/link-mod.sh stellaris-mod-EmptyHulls/empty_hulls` → launcher
      open. On Linux the upload dialog may not see a **symlinked** mod: then copy the folder into
      `<user dir>/mod/` and upload the copy.
- [x] Upload to **Steam Workshop** (description: BBCode below, then the "More from me" block from
      `../docs/store-more-from-me.md` without this mod's line). Add `assets/designer-corvette.png` on the
      item's page (both stores). A first upload starts **Hidden**: set it Public. The launcher writes
      `remote_file_id` into `descriptor.mod`: commit it.
- [x] Upload to **Paradox Mods** (plain text below; format headings, lists and links with the
      website editor, then check the saved page).
- [x] IDs into the table below and into `../docs/store-more-from-me.md`.
- [x] "More from me" in the other mods' descriptions: appended by `scripts/store_texts.py` since
      2026-11-23, reaching each store with that mod's next upload.
- [ ] GitHub repo public (`gh repo edit mkoester/stellaris-mod-EmptyHulls --visibility public
      --accept-visibility-change-consequences`); the store texts don't link it, the README does
      no harm.

## Published IDs

| Store | Item ID | URL |
|---|---|---|
| Steam Workshop | `3835150872` | https://steamcommunity.com/sharedfiles/filedetails/?id=3835150872 |
| Paradox Mods | `166530` | https://mods.paradoxplaza.com/mods/166530/Any |

`descriptor.mod` carries only the Workshop ID (`remote_file_id`); the launcher keeps the Paradox
one in its own database.

---

## Store description

`store/empty_hulls.bbcode` is the Steam Workshop text (BBCode). `scripts/store_texts.py` in the workspace (run by `slink`, or on its own with the launcher closed) writes it into the launcher's upload form, with the "More from me" block appended, and makes the Paradox Mods HTML and short description from it. Edit the file, never the form.
