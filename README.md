<p align="center"><img src="https://github.com/aaskjer/Slot-Machine-Game/blob/main/Assets/logo-small.png?raw=true" alt="SMG banner" width="400" height="400"></p>

Slot Machine Game is a chat game for streamer.bot that runs on Twitch, Kick and YouTube.

![Static Badge](https://img.shields.io/badge/https%3A%2F%2Fimg.shields.io%2Fbadge%2Fany_text-Twitch%2C_Kick%2C_YouTube-white?label=supported%20platforms)
![Static Badge](https://img.shields.io/badge/https%3A%2F%2Fimg.shields.io%2Fbadge%2Fany_text-streamer.bot-white?label=tool&color=%230b73ff)
![GitHub License](https://img.shields.io/github/license/aaskjer/Slot-Machine-Game)
![GitHub Release](https://img.shields.io/github/v/release/aaskjer/Slot-Machine-Game)
![GitHub Downloads (all assets, all releases)](https://img.shields.io/github/downloads/aaskjer/Slot-Machine-Game/total)

---

# Overview

- Runs on Twitch, YouTube and Kick.
- Chat spins the slots with a bet: `!slots <amount>`, an alias like `all`, `half`, `third`, `quarter` or `random`, or nothing at all for the default bet.
- Fully adjustable odds: match chance, jackpot chance, and rerolls that control how often accidental matches slip through.
- Configurable payouts per match tier, from 2 alike up to the jackpot, scaled by emote weight so rare emotes pay more than common ones.
- Adjustable slot count (3–6 reels), emote pool size, and which emote weights can come up.
- Optional Jackpot Pool, fed by lost bets, that pays out on top of a jackpot once the bet reaches a minimum.
- Optional subscriber and VIP payout boosts on Twitch; a viewer with both gets the sum.
- Optional "Addicted" list (single users or whole Streamer.bot groups): they still play, but with penalties such as a cut on every win.
- Keep whole Streamer.bot groups from playing.
- Free Mode for spins without a stake, either for everyone or per trigger.
- Detects [Currency Core by StreamUP](https://streamup.tips/product/currency-core) and [LOYALTY POINTS by tawmae](https://tawmae.xyz/loyalty-points) on its own.
- Every chat message can be edited in the settings window: win, loss, jackpot, free spin, addicted, invalid bet and cooldown. Wording about the pool goes inside `{jackpot}...{/jackpot}` and only reaches chat while the pool is on.
- A log file per day with every spin, searchable and filterable in the built-in log viewer.
- A settings window with dark and light mode and six pages: it shows the odds your settings actually give, plays test spins with the exact chat message, and edits the emotes of each platform.

---

## 🎮 How It Works

Chat spins the slots with `!slots <bet>` (or a bet alias). The game rolls the reels, checks for a match against the configured odds and settles the payout on the spot: win, jackpot or loss.

| Event | Trigger | Result |
|---------|---------|---------|
| 🎰 **Spin** | A viewer runs the slots command with a bet | The bet is deducted (unless in Free Mode) and the reels roll. |
| ✅ **Win** | 2 or more slots match | The payout follows from the match tier and the emote's weight, and goes to the viewer's balance. |
| 🔥 **Jackpot** | All slots match | The jackpot payout, plus the Jackpot Pool if the bet reached the minimum for it. |
| ❌ **Loss** | No match | The bet is lost and goes into the Jackpot Pool, the Jackpool in chat (not in Free Mode, not for players on the Addicted list, and not when the bet was channel points). |
| 🚫 **Blocked / Addicted** | Player is on the Blocked or Addicted list | Blocked players can't play at all. Addicted players play normally, but with a payout cut, and the per-viewer cooldown holds them on Channel Points redemptions too. |
| ⏱️ **Cooldown** | Player spins again too soon | A cooldown message goes out instead of a spin. |

---

## 🎫 Channel Points Mode (Twitch only)

With `Channel points` picked, the chat command is off on Twitch: there, only viewers who redeem the configured Channel Point reward can spin. The slot machine takes redemptions from Twitch only, so on YouTube and Kick the chat command keeps working. There are four bet modes:

| Option | Info |
|---------|---------|
| **Cost** | The reward's channel point cost is the bet: a loss takes no points, a win is paid in points |
| **Input** | The viewer types a bet in their own points into the reward's text field |
| **Fixed** | Every redemption bets the same configured amount, staked in channel points like Cost |
| **Free** | Every redemption spins for free, whatever the reward costs |

---

# Get Started

[Setup Guide](https://github.com/aaskjer/Slot-Machine-Game/blob/main/Setup-Guide.md)

[Frequently Asked Questions](https://github.com/aaskjer/Slot-Machine-Game/blob/main/FAQ.md)

[Import String for streamer.bot](https://github.com/aaskjer/Slot-Machine-Game/blob/main/Import-String.md)

[Download](https://github.com/aaskjer/Slot-Machine-Game/releases)

---

# Credits & Links

[aaskjer on Twitch](https://twitch.tv/aaskjer)

[aaskjer.github.io](https://aaskjer.github.io/)

[Slot Machine Game on SB Discord](https://discord.com/channels/834650675224248362/1446889756297527530/1446889756297527530)

[Streamer.bot](https://streamer.bot) / [nate1280](https://www.patreon.com/c/nate1280/home)

YOU ♡
