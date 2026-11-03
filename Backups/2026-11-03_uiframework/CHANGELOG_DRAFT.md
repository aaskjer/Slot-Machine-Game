## Unreleased

### Added
- The footer counts what is unsaved — "No unsaved changes", "1 unsaved change", "4 unsaved changes" — instead of a flag that stayed on once anything was touched. Typing the old value back takes an edit off the count again, and the emote lists count too, one per platform.
- A Reset-page button next to Reset all: it puts the defaults back on the page in front only — the Emotes page gets its default emotes back on every platform — and writes nothing until you save.
- Closing the window with unsaved changes asks "Discard N unsaved changes?" — from Cancel as well as from the title bar's X, which used to drop everything without a word. Switching the theme with unsaved changes offers to save first.
- A save that would not do what it looks like — a minimum bet above the maximum, Free mode off without a points variable, the jackpot pool on with a bet of 0 to win it, a smallest emote weight above the largest — lists the problem and asks before saving.
- Streamer.bot's `Dispose()` on a recompile or shutdown closes an open settings window, instead of leaving it writing `SMG-Settings.json` from a build nothing else uses.

### Changed
- Settings are kept within what the game takes for granted on every save: no negative cooldowns, bets, weights, payouts or boosts, the slider's 3 to 6 slots, chances between 0 and 100%.

### Fixed
- A save that failed outright — the file locked, the folder gone — only said so in the status line. It now says so in a message box too.

## v15.0.1

### Changed
- Saving `SMG-Settings.json` is one swap instead of a copy and a swap: `File.Replace` hands the file it replaces straight to `SMG-Settings.json.bak`, so a save no longer copies the whole file first. The backup is still only taken from a file that parses itself, so a damaged one cannot overwrite the last readable copy.

### Fixed
- A `SMG-Settings.json` that cannot be opened at all — locked by something else, or not readable for want of rights — fell through to the defaults wherever the settings were read outside the window. It now falls back to the backup copy like a damaged file does.
- A settings window that failed while it was being built left its thread running with nothing to show, and the cooldown poll behind it never ended. The dispatcher is now shut down in either case.
