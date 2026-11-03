## Unreleased: v14.0.1 (since v14.0.0)

### Changed
- Channel points work as in Classic Chat Gamble: in Reward cost and Fixed mode the channel points are the stake, so a loss takes no points and adds nothing to the Jackpool, and a win is paid in points. Typed amount bets the viewer's own points.
- Minimum and Maximum bet apply to Typed amount and Fixed mode.
- Without a Reward ID, no redemption starts a spin and other rewards are left alone; saving like that says so.
- Chat calls the jackpot pool the Jackpool; standard texts nobody changed switch over by themselves.
- Channel points Free mode uses the Free messages.
- Cooldown messages fill in `{user}`, round the seconds up and can't fail on a stray brace.
- Each line of a message goes out as a chat message of its own; Twitch and Kick split at 500 characters instead of 200.
- The settings window opens at once; the Update pill appears when GitHub answers.
- Reset keeps the light or dark theme.

### Fixed
- The import works wherever Streamer.bot is installed: every Windows reference is absolute, no more "Find Refs".
- The jackpot message no longer counts the Jackpool twice: `{amount}` is the win without the pool.
- A balance that can't be read stops the spin instead of being overwritten, and a redemption is refunded.
- A redemption that can't spin (no emotes) is refunded instead of fulfilled.
- A damaged settings file: the game plays with the `.bak`, or not at all, instead of silently without emotes.
- A Reward cost redemption without its cost is refunded instead of played for 0.
- Free spins never win the Jackpool.
- The addicted-viewer texts no longer promise a doubled cooldown.
