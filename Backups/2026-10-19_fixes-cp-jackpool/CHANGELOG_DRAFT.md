## 2026-10-02

### Added
- The Emotes page shows each emote's picture next to its name.
- Kick emotes are found by their ID, and the Twitch default emotes by their Twitch ID.
- Other Twitch emotes are looked up by their chat code: Twitch first, then 7TV, BTTV and FFZ.
- 7TV, BTTV and FFZ emotes are marked with their source, plus a note that only viewers with that extension see them.
- The chat previews (Try a spin, Messages) show emotes as pictures the way chat does: Twitch emote codes, including words in the message, and Kick's `[emote:ID:name]`.
- Saving a Default bet or Fixed bet that can't work (0, below Minimum, above Maximum) saves anyway and says why, once.
- The Messages preview notes when a message can never be sent, e.g. Loss when there are fewer emotes per spin than slots.

### Changed
- Default Twitch emotes are Twitch globals only: NotLikeThis, SeemsGood and Kreygasm replace monkaS, EZ and Clap.
- Opening the settings while they're already open brings that window to the front instead of opening a second one.
- The Update pill only appears for a newer release.
- Whole-number fields accept only the digits 0–9; spaces are ignored, so "1 0" is 10.
- "Unsaved changes" is shown in orange.
- The odds are only recalculated when their inputs change, and previews only refresh while their page is shown.
- Log files and emote pictures load when their page is first opened.

### Fixed
- A very large Rerolls value with fewer emotes than slots no longer freezes the settings window or hangs a spin.
- `half`, `third`, `quarter` and `random` no longer fail with a balance above 2,147,483,647.
- A refund that Twitch refuses is no longer announced in chat; it's logged as a warning instead.
- A settings file that is in use or can't be written is no longer treated as damaged: the window says why and changes nothing.
- Full-width digits and digits from other scripts no longer save as 2,147,483,647.

### Tools
- check-settings now also checks the tags that previews hook up through, including conditional Switch reads.
- check-compile now also catches using aliases that clash with Streamer.bot's own global `Inline` (error CS0576).
- gui-shots builds its compiler via `run-engine-tests.ps1 -HostOnly`.
- `-Damaged` now also covers a locked settings file.
- `-Test -Theme light` passes now.
- Every fix above has new tests, and check-all passes completely.
