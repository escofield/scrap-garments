# Scrap Mechanic — Garment Collection Tracker

A single-file, offline web tool for [Scrap Mechanic](https://store.steampowered.com/app/387990/Scrap_Mechanic/)
that shows which character outfit pieces you've collected and exactly which ones you're still missing — grouped
by category, by where they come from, and by rarity.

**[▶ Open the tracker](https://escofield.github.io/scrap-garments/)** &nbsp;·&nbsp; everything runs locally in your browser; no data is uploaded.

## What it does

- **Load your `unlock` file** and instantly see collected vs. missing — no Steam ID, no game-data file needed; the full
  204-garment list is built in.
- **Filter by source** (Garment Box, Underground balloon chests, quests, Wonk Store, Fan Pack DLC, …) and by
  **rarity** (Common / Rare / Epic / Legendary — the Garment Box drop tiers), shown as a coloured stripe on each item.
- **Generate a new `unlock` file** from any selection — it's re-signed using your loaded file's own signature, so it
  stays valid for your account **without ever entering a Steam ID**.
- **One-click "Prep achievement file"** — a workaround for the *Unlock every cosmetic item* achievement, which can't
  complete normally because **Welder Pants** ships with a broken rarity and never drops from a Garment Box. The tool
  builds a file with everything unlocked except one reliable Common item, so collecting that last item in-game fires
  the achievement.

## Where is the `unlock` file?

It lives in a folder named `User_<STEAMID>` inside Scrap Mechanic's user data:

- **Windows:** `%appdata%\Axolot Games\Scrap Mechanic\User\User_<STEAMID>\unlock`
- **Linux / Steam Deck (Proton):**
  `~/.steam/steam/steamapps/compatdata/387990/pfx/drive_c/users/steamuser/AppData/Roaming/Axolot Games/Scrap Mechanic/User/User_<STEAMID>/unlock`

**Back up the file before changing anything.**

## How it works

The `unlock` file is a small binary format: a magic number, a CRC32 checksum, an item count, then one 16-byte UUID per
unlocked item. The checksum is keyed to your Steam ID, so a hand-made file would normally need it — this tool instead
reuses the signature from the file you load (CRC linearity / `crc32_combine` math) to re-sign new files for the same
account automatically.

Item names, sources, and rarities are cross-referenced from the
[official Scrap Mechanic Wiki](https://scrapmechanic.fandom.com/wiki/Clothing). Note: editing the `unlock` file only
flips the "owned" flags — it does **not** replay the in-game events Steam watches, so collection achievements won't
fire from a hand-made file (hence the achievement workaround above).

## Files

- `index.html` — the tracker (open this).
- `unlock.html` — the original 2022 unlocker this project grew from (kept for reference; it expects the old
  `customization_options.json`, which newer game versions no longer ship).

## Credits

Builds on the original [Scrap Mechanic Character Customisation Tool](https://gist.github.com/wisdom-in-snow/05bcb63c447d77fecc1b83efa7b32f27)
and the [scrapmechanicunlocker](https://scrapmechanicunlocker.pages.dev/) web version. Not affiliated with Axolot Games.
