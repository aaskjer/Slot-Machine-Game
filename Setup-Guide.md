# Import
<p align="center"><img alt="Import in Streamer.bot" src="https://github.com/user-attachments/assets/2c17f5a0-15f3-4396-a277-a66638017fb3"></p>

In [streamer.bot](https://streamer.bot/), click `Import` and drag the [SlotMachineGame.sb](https://github.com/aaskjer/Slot-Machine-Game/releases) file into the window, or paste the [import string](https://github.com/aaskjer/Slot-Machine-Game/blob/main/Import-String.md).

<p align="center"><img alt="Import window" src="https://github.com/user-attachments/assets/cd761fe1-bc20-4d0e-be24-1b00dc4bc529"></p>

Click `Import`, then `Yes` in both popups that follow.

## Enable the command
<p align="center"><img alt="Enable the command" src="https://github.com/user-attachments/assets/c4d780df-3f55-4215-a485-4b23ff8263be"></p>

The command `[SMG] - Play Slots` arrives switched off. In the `Commands` tab, right-click the group `[SMG] Slot Machine Game` and click `Enable All`.

Viewers play with `!slots` or `!spin`, on Twitch, YouTube and Kick alike. To leave a platform out, open the command and untick its source, for example `Kick Message`.

# Setup
<p align="center"><img alt="Open the settings" src="https://github.com/user-attachments/assets/71ddb888-73fb-47bd-81eb-ec314d5d69f0"></p>

In the `Actions` tab, select `[SMG] - Settings`, right-click `Test` in its trigger list and click `Test Trigger`. The settings window opens.

The first time, a small dialog asks whether to download `UIFramework.dll` — the settings window itself, shared by
all of these chat games and kept at [aaskjer/UIFramework-Streamer.bot](https://github.com/aaskjer/UIFramework-Streamer.bot).
`Yes` fetches it (about 200 KB, checked against its published hash) into `UIFramework\lib\<version>\` next to
Streamer.bot and opens the window. `No` opens that folder instead, for when you would rather drop the file in by
hand from the [releases](https://github.com/aaskjer/UIFramework-Streamer.bot/releases). When a newer window is
released the same dialog comes back once; `Cancel` skips that version.

Hover over an option for a tooltip with the details. `Save` or `Ctrl+S` keeps your changes, `Save & Exit` also closes the window, and `Ctrl+1` to `Ctrl+7` jump between the pages. The buttons at the bottom left switch between dark and light, reset everything or only the page in front, and open the customise mode: rename, reorder, hide or move pages and fields by drag and drop or from their context menu, pick an accent colour, and the window keeps that layout in `uiframework.layout.json` next to the settings — through every update of the game. When a new version of the game is out, a pill shows up in the header.

## Game
<p align="center"><img alt="Game page" src="Assets/setup-guide/game.png"></p>

- **Slots and odds**: how many slots spin (3 to 6), the match and jackpot chances, rerolls, and which emotes play. `What really comes out` shows a bar of how often a spin really ends in a jackpot, a win or a loss, and how much a bet of 100 brings back on average, worked out from the game's own engine with the values as they stand in the window. `Emotes of` picks whose emotes the odds and the test spin use.
- **Bets and points**: default, minimum and maximum bet, Free mode, and the points variable. Currency Core by StreamUP and LOYALTY POINTS by tawmae are found on their own.
- **Payouts**: what 2, 3, 4 and 5 alike and the jackpot pay (tiers the chosen number of slots can't land are greyed out), the Subscriber and VIP boosts, and the Addicted cut.
- **Jackpot pool**: lost bets go into the Jackpool, and a jackpot with a big enough bet wins it on top.
- **Try a spin**: pick a bet and who spins, then click `Spin` to see the slots and exactly what chat would get, with the settings as they stand on the page. Nothing is saved, and nobody's points change.

## Emotes
<p align="center"><img alt="Emotes page" src="Assets/setup-guide/emotes.png"></p>

Each platform has its own list: one row per emote with the emote as chat types it, its weight and a name. A low weight comes up often and pays little, a high one is rare and pays a lot. `Add row` adds an emote, `×` takes one out, and `Restore defaults` brings back the original set of that platform.

Kick shows `[emote:ID:name]` as the emote, so that is what goes into the row; the ID is the number in the address of the emote's picture. On Twitch, emotes from BTTV, 7TV and FFZ work too; the window shows their picture and names the extension in its tooltip, and in chat only viewers with that extension see them as emotes.

## Access
<p align="center"><img alt="Access page" src="Assets/setup-guide/access.png"></p>

- **Blocked groups, addicted viewers and groups**: type a name and press `Enter`; `×` removes it again. Addicted viewers win less and get messages of their own.
- **Channel points (Twitch)**: with the chat command, or on Twitch with a channel point reward.
- **Cooldowns**: one for everyone, one per viewer. Saving writes them straight into the command.

### Twitch Channel Points
<p align="center"><img alt="Channel points" src="Assets/setup-guide/access--channel-points.png"></p>

1. Switch on `Channel points start a spin`. The chat command is then off on Twitch, while YouTube and Kick keep using it.
2. Paste the ID of your reward into `Reward ID`; the tooltip names a page that lists your rewards with their IDs. Without one, no redemption starts a spin.
3. Pick what is bet: `Reward cost`, `Typed amount`, `Fixed` or `Free`.

A redemption that doesn't end in a spin is refunded, as long as the reward doesn't skip the reward requests queue.

WIP - May not work as intended because it was taken from another game and i'm still not an affiliate so i can't properly test it. Please report [here](https://github.com/aaskjer/Slot-Machine-Game/issues) on issues.

## Messages
<p align="center"><img alt="Messages page" src="Assets/setup-guide/messages.png"></p>

Edit any message or translate it into your language. Pick one from the list and click a placeholder to insert it; the chat preview shows the result the way chat will read it. Words about the Jackpool wrapped in `{jackpot}…{/jackpot}` stay out of chat while the jackpot pool is off. `Numbers` sets how chat writes numbers, like 12.345 or 12,345.

Below the preview you choose the sender, your bot account or your own, and `Send as /me`, which only exists on Twitch. Game messages and cooldown messages are set separately.

## Log
<p align="center"><img alt="Log page" src="Assets/setup-guide/log.png"></p>

Every spin, day by day. Search for names or amounts, filter by result, platform or day, and click a line to read all of it. `Write a log file per day` turns logging on or off.

## About
<p align="center"><img alt="About page" src="Assets/setup-guide/about.png"></p>

The version of the game and of UIFramework, links, and the points systems supported out of the box.

---

[Frequently Asked Questions](https://github.com/aaskjer/Slot-Machine-Game/blob/main/FAQ.md) · [Report an issue](https://github.com/aaskjer/Slot-Machine-Game/issues)
