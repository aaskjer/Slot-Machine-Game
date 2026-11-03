# Changelog

Releases are in the [release notes](https://github.com/aaskjer/Slot-Machine-Game/releases).
The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/).

## [16.0.0] - 2026-11-03

The settings window moved into [UIFramework for streamer.bot](https://github.com/aaskjer/UIFramework-Streamer.bot),
one window shared by all of these chat games. The spin plays exactly as before; what changed is how the settings
are shown and stored.

### Changed

- **One DLL, downloaded on first open.** `[SMG] - Settings` is now a small stub. The first time you open the window
  it asks whether to download `UIFramework.dll` from GitHub (about 200 KB, checked against its published SHA-256)
  or to show the folder it belongs in, `UIFramework\lib\<version>\` next to Streamer.bot. Nothing is fetched
  without that click. When a newer UIFramework is published, opening the window offers it once: *Yes* downloads,
  *No* asks again next time and shows a pill in the header, *Cancel* skips that version.
- **The window is built from the game's own settings table.** The game declares every setting once and answers the
  window's request with it, so the window and the game can never disagree about a key, a default or a range again.
- **The test spin comes out of the game's own engine.** *Try a spin* on the Game page plays one round with the very
  code that spins in chat, from the values as they stand in the window, saved or not: the slots as pictures, and the
  exact chat message. The platform whose emotes spin is picked right there, since a Twitch emote only exists on
  Twitch and a Kick emote only on Kick.
- **The emotes are three lists.** Twitch, YouTube and Kick sit one under the other on the Emotes page, each row an
  emote with its picture, its weight and a name, with *Add row* and *Restore defaults*. Kick emotes are typed as
  `[emote:ID:name]`; Twitch pictures come from Twitch, 7TV, BTTV and FFZ as before.
- **Customise mode.** The pencil at the bottom left lets you rename, reorder, hide and move pages and fields by drag
  and drop or from the context menu, and pick the accent colour. It lives in `uiframework.layout.json` next to
  `SMG-Settings.json` and survives every import of the game.
- `SMG-Settings.json` keys are camelCase now (`useBot`, `minBet`, `matchChance`, `emotesTwitch`), the chances and
  the Addicted cut are stored in percent, and the emotes moved from `PlatformEmotes` to `emotesTwitch`,
  `emotesYoutube` and `emotesKick`. An existing file keeps working: the old names are read through aliases, and the
  first save writes the new ones.
- The cooldown messages use `{seconds}` and `{user}` instead of `{0}` and `{1}`; a text that still has the numbers
  keeps working.
- Light/dark and the rainbow mode live in `uiframework.layout.json` and are shared with every other window built on
  UIFramework. An existing `DarkMode` is taken over on the first open.
- Values typed out of range are pulled back into range when the game reads them, not only when the window saves.
- The footer counts what is unsaved; *Reset page* puts the defaults back on the page in front only; closing the
  window with unsaved changes asks first, from Cancel and from the title bar's X alike; a recompile or shutdown in
  Streamer.bot closes it without asking.
- A save that would not do what it looks like - a minimum bet above the maximum, Free mode off without a points
  variable, the jackpot pool on with a bet of 0 to win it, a smallest emote weight above the largest, channel
  points without a reward ID or with a fixed bet of 0 - lists the problem and asks before saving.
- Payout tiers that cannot come up with the chosen number of slots are greyed out, and the fixed bet only while
  channel points bet a fixed amount.
- A fresh install no longer writes `SMG-Settings.json` on the first spin; the game plays on the defaults until the
  window saves.

### Removed

- The window's own WPF code and update check (about 4,500 lines) left the import; the DLL carries them now.

## [15.0.1] - 2026-10-25

See the [release notes](https://github.com/aaskjer/Slot-Machine-Game/releases/tag/v15.0.1).
