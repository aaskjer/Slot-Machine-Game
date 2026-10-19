# Import
<p align="center"><img alt="Import in Streamer.bot" src="https://github.com/user-attachments/assets/2c17f5a0-15f3-4396-a277-a66638017fb3"></p>

Click on `Import` in [streamer.bot](https://streamer.bot/) and drag the [SlotMachineGame.sb](https://github.com/aaskjer/Slot-Machine-Game/releases) file into the window, or copy and paste the [import string](https://github.com/aaskjer/Slot-Machine-Game/blob/main/Import-String.md).

<p align="center"><img alt="Import window" src="https://github.com/user-attachments/assets/cd761fe1-bc20-4d0e-be24-1b00dc4bc529"></p>

Click on `Import` and `Yes` on both following popup messages.

## Enable the command
<p align="center"><img alt="Enable the command" src="https://github.com/user-attachments/assets/c4d780df-3f55-4215-a485-4b23ff8263be"></p>

The command `[SMG] - Play Slots` arrives switched off. In the `Commands` tab, right-click the group `[SMG] Slot Machine Game` and click `Enable All`.

Viewers play with `!slots` or `!spin`, on Twitch, YouTube and Kick alike. To leave a platform out, open the command and untick its source, for example `Kick Message`.

# Setup
<p align="center"><img alt="Open the settings" src="https://github.com/user-attachments/assets/71ddb888-73fb-47bd-81eb-ec314d5d69f0"></p>

In the `Actions` tab, select `[SMG] - Settings`, right-click `Test` in its trigger section and click `Test Trigger` to open the settings window.

Hover over any option for a tooltip with more details. `Save` (or `Ctrl+S`) keeps your changes, `Save & Exit` closes the window afterwards, and `Ctrl+1` to `Ctrl+6` switch between the pages. The buttons at the bottom left switch between dark and light and reset everything to the defaults. When a new version is out, a red `Update` pill shows at the top.

## Game
<p align="center"><img alt="Game page" src="Assets/setup-guide/game.png"></p>

- **Slots and odds**: how many slots spin (3 to 6), the match and jackpot chances, rerolls, and which emotes play. The bar shows how often a spin really ends in a jackpot, a win or a loss, and how much a bet of 100 brings back on average.
- **Bets and points**: default, minimum and maximum bet, Free mode, and the points variable. Currency Core by StreamUP and LOYALTY POINTS by tawmae are found on their own.
- **Payouts**: what 2, 3, 4 and 5 alike and the jackpot pay, the Subscriber and VIP boosts, and the Addicted cut.
- **Jackpot pool**: lost bets go into the Jackpool, and a jackpot with a big enough bet wins it on top.
- **Try a spin**: pick a bet, who spins and the platform, then click `Spin` to see exactly what chat would get. Nothing is saved, and nobody's points are touched.

## Emotes
<p align="center"><img alt="Emotes page" src="Assets/setup-guide/emotes.png"></p>

Every platform has emotes of its own. Add an emote with a weight: a low weight comes up often and pays little, a high weight is rare and pays a lot. Change a weight right in the list, take an emote out with `×`, or put the defaults back with `Reset to default`.

<p align="center"><img alt="Kick emotes" src="Assets/setup-guide/emotes--kick.png"></p>

Kick emotes need their ID and name; hover over the ID field to see where to find it.

<p align="center"><img alt="Twitch emotes from BTTV, 7TV and FFZ" src="Assets/setup-guide/emotes--twitch-extensions.png"></p>

Emotes from BTTV, 7TV and FFZ can be added on Twitch too. The window shows them with their picture and where they come from; in chat they show as emotes for viewers who use that extension.

## Access
<p align="center"><img alt="Access page" src="Assets/setup-guide/access.png"></p>

- **How viewers play**: with the chat command, or on Twitch with a channel point reward.
- **Cooldown in seconds**: for everyone and per viewer. They're written into the command as soon as you save.
- **Blocked groups, addicted viewers and groups**: type a name and press `Enter`; `×` takes it off again. Addicted viewers win less and get messages of their own.

### Twitch Channel Points
<p align="center"><img alt="Channel points" src="Assets/setup-guide/access--channel-points.png"></p>

1. Pick `Channel points`. The chat command is then off on Twitch, and keeps working on YouTube and Kick.
2. Paste the ID of your reward into `Reward ID`; `Find my reward ID` helps you look it up. Without one, no redemption starts a spin.
3. Pick what is bet: `Reward cost`, `Typed amount`, `Fixed` or `Free`.

Redemptions that don't end in a spin are refunded, as long as the reward doesn't skip the reward requests queue.

WIP - May not work as intended because it was taken from another game and i'm still not an affiliate so i can't properly test it. Please report [here](https://github.com/aaskjer/Slot-Machine-Game/issues) on issues.

## Messages
<p align="center"><img alt="Messages page" src="Assets/setup-guide/messages.png"></p>

Edit any message or translate it into your language. Pick a message from the list and click a placeholder to put it in; the chat preview shows the message the way chat will read it. Words about the Jackpool wrapped in `{jackpot}…{/jackpot}` are left out while the jackpot pool is off. `Numbers` sets how chat writes numbers, like 12.345 or 12,345.

Below the preview you pick the sender: your bot account or your own, and `Send as /me`, which exists on Twitch only. The game's messages and the cooldown messages each have their own.

## Log
<p align="center"><img alt="Log page" src="Assets/setup-guide/log.png"></p>

Every spin, day by day: search for names or amounts, filter by result or date, and click a line to see all of it. `Write a log file per day` switches logging on or off.

## About
<p align="center"><img alt="About page" src="Assets/setup-guide/about.png"></p>

Version, links, and the points systems the game supports out of the box.

---

[Frequently Asked Questions](https://github.com/aaskjer/Slot-Machine-Game/blob/main/FAQ.md) · [Report an issue](https://github.com/aaskjer/Slot-Machine-Game/issues)
