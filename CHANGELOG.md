# Changelog

Releases are in the [release notes](https://github.com/aaskjer/Slot-Machine-Game/releases).
The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/).

## [16.4.2] - 2026-11-12

### Added

- **aaskjer on Twitch** is back among the links of the About page.

### Changed

- **The update question says when Streamer.bot needs a restart.** A newer UIFramework can be used at once only
  while none is running in your Streamer.bot; otherwise it takes effect after a restart. The dialog now says which
  of the two it is, and after such a download a note says it again: restart when it suits you, everything goes on
  as before until then.
- **Closing the update question means "not now".** *Yes* takes the new UIFramework, *No* skips that version, and
  *Cancel*, the X and Esc ask again at the next open. Closing the dialog used to skip the version for good.
- **A skipped version is skipped in every game.** It is kept once, in `UIFramework\loader.json` beside
  Streamer.bot, and so is `"autoUpdate": false`. What a game's `uiframework.layout.json` holds is still read.
- The settings action is 0.3.1, the host block UIFramework 1.9.0's. Nothing in your settings changes.

### Fixed

- **A download GitHub does not deliver is tried three times** before the settings action gives up.
- **No answer from the game shows as no answer.** A Try button said "done" and a table showed as empty when the
  game action did not answer.
- **A late answer is not taken for the next one.** Every request to the game has a variable of its own.

## [16.4.1] - 2026-11-12

### Fixed

- **The settings action passes over a UIFramework it is too old for.** Every game in a Streamer.bot shares the
  installed UIFramework.dll. Should a later one need a newer settings action than this game's, the action now
  leaves that file alone and opens the window with an older one that fits, with a line in the log; it used to
  load whatever was newest. (Settings action 0.2.1.)
- **The update notice works with a UIFramework.dll you put in by hand.** A file saved from the browser carries
  Windows' "downloaded from the internet" mark, and the game did not load it: the notice at Streamer.bot's start
  never came. A file damaged since its download is no longer loaded for it.

### Changed

- The host block is UIFramework 1.8.4's. Nothing in your settings changes.

## [16.4.0] - 2026-11-08

### Added

- **Tells you about updates.** Once per Streamer.bot start, about 20 seconds in, one notice names new releases of
  this game, of the other UIFramework games and of UIFramework: in every chat whose broadcaster account is
  connected (Twitch, YouTube, Kick), or as a Windows notification while none is. The links are in Streamer.bot's
  log. *Tell me about updates* on the About page turns it off for this game. The game action is precompiled on
  application start, so the notice starts with Streamer.bot.
- The host block is UIFramework 1.4.0's; the settings window offers the newest UIFramework on its next open.

## [16.3.0] - 2026-11-07

### Added

- **A tour of the settings window.** The first time the window opens, a short tour rings one part after the other
  (the pages, saving, the customise mode) and says what it does; the **?** at the top right shows it again.
- **UIFramework 1.0.0.** Problems the window finds sit behind a red **i** in its header instead of on the About or
  Log page, and *How to play*, *Log* and *About* sit together at the foot of the page list. The settings action
  offers the new framework on its next open.

### Changed

- **Only the fields your setup uses.** *Fixed bet* shows while the channel point bet mode is *Fixed*, and the
  *3 alike*, *4 alike* and *5 alike* payouts only with enough slots to pay them (4, 5, 6); before, they stood
  there greyed out.
- **The settings action is UIFramework's stub 0.2.0.** When the game action hangs, the settings window waits 30
  seconds for its answer, then carries on and can be closed; before, it waited for good. A game that has not
  described itself for a minute no longer locks the settings until Streamer.bot restarts: the next run opens the
  window.
- The host block is UIFramework's current one (1.0.0). It names every type in full, so it no longer depends on the
  action's `using` lines, and it can declare a tour of the window. Nothing changes in the window.

## [16.2.0] - 2026-11-06

### Added

- **Free mode from chat.** `!SetFreeSlots` turns Free mode on and `!EndFreeSlots` turns it off (moderators; two
  new commands in the import, disabled until you enable them). The switch is written into the settings file, so the
  window's pill shows it, and chat gets the new Started and Ended messages (Messages page, Free mode). An action of
  your own can do the same with an Execute C# Method on `StartFreeGame` or `EndFreeGame`.
- **Three more custom triggers.** `SMG: Free Game Start` and `SMG: Free Game End` fire when Free mode is switched;
  `SMG: Spin Free` fires on every free spin, on top of its Win, Loss or Jackpot trigger.

### Changed

- **Emote lists without a name column.** The name of an emote is in its code: a Twitch emote is its name, a Kick
  emote's name follows its ID, a YouTube emoji's name sits between its colons. The weight column is last.
- **YouTube's own emojis.** The YouTube list takes the emojis YouTube's chat has (typed as `:name:`, like
  `:face-purple-rain-drops:`), shows their pictures and starts with ten of them; the fruit emoji of earlier versions
  were only emotes to viewers with BetterTTV. A Unicode emoji still works and shows itself.
- **Kick emotes typed short.** `1730803:emojiRich` is enough; the game sends it as `[emote:1730803:emojiRich]`, the
  form Kick's chat renders (that form still works in the list too). The defaults are the short form.
- Needs UIFramework 0.9.4 or newer for the pictures of YouTube's emojis and of short Kick codes in the window; an
  older DLL shows the lists without those pictures.
- The host block is UIFramework's current one (0.9.10); nothing changes in the window. The window itself, with
  UIFramework 0.9.10, puts the weight column at half width and lets the customise mode place fields side by side.

## [16.1.0] - 2026-11-06

### Added

- **Custom triggers.** Every settled spin fires `SMG: Spin Win`, `SMG: Spin Loss` or `SMG: Spin Jackpot` (Custom >
  Chat Game > Slot Machine Game) with the spin as arguments: `spinOutcome`, `spinUser`, `spinPlatform`, `spinSlots`,
  `spinBet`, `spinAmount`, `spinPreviousPoints`, `spinNewPoints`, `spinCurrency`, `spinJackpotPoolWon`, `spinFree`.
  `GetLastSpinResult`, run with an Execute C# Method sub-action on the game action, hands the same arguments to any
  other action.
- **Stats per viewer, for a leaderboard of your own.** Every spin updates the viewer's user variables on the platform
  it was made on: `smg_spins`, `smg_wins`, `smg_losses`, `smg_jackpots`, `smg_totalBet`, `smg_totalWon`,
  `smg_totalLost`, `smg_netProfit`, `smg_biggestWin`, `smg_biggestBet`, `smg_poolWon`, `smg_currentStreak`,
  `smg_bestStreak`, `smg_userName`, `smg_firstPlayed`, `smg_lastPlayed`. Free spins count as spins, wins and jackpots
  but move no points.
- **German.** With the window's language set to `de` (the pencil, then *Sprache*), every setting, section, page
  and message of the window reads in German. The help and about pages stay English.

### Changed

- **The settings action is UIFramework's generic stub.** `[SMG] - Settings` carries no layout and no copy of the
  engine any more: the game action declares its window (pages, pills, the log, help and about, the `!slots`
  cooldowns) beside its settings table and answers the window itself (the test spin with the very engine that spins
  in chat, the check before saving, the emote pictures' sources). Needs UIFramework 0.9.2 or newer; the stub
  fetches it.

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
