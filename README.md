<p align="center"><img src="https://github.com/aaskjer/Slot-Machine-Game/blob/main/Assets/logo-small.png?raw=true" alt="SMG banner" width="400" height="400"></p>

Slot Machine Game is a chat game built for streamer.bot, supporting twitch, kick, and youtube.

![Static Badge](https://img.shields.io/badge/https%3A%2F%2Fimg.shields.io%2Fbadge%2Fany_text-Twitch%2C_Kick%2C_YouTube-white?label=supported%20plattform)
![Static Badge](https://img.shields.io/badge/https%3A%2F%2Fimg.shields.io%2Fbadge%2Fany_text-streamer.bot-white?label=tool&color=%230b73ff)
![GitHub License](https://img.shields.io/github/license/aaskjer/Slot-Machine-Game)
![GitHub Release](https://img.shields.io/github/v/release/aaskjer/Slot-Machine-Game)
![GitHub Downloads (all assets, all releases)](https://img.shields.io/github/downloads/aaskjer/Slot-Machine-Game/total)

---

# Overview

- Works on Twitch, YouTube, and Kick.
- Chat spins the slots with a bet — `!slots <amount>`, or an alias like `all`, `half`, `third`, `quarter`, `random`, or nothing at all to use the configured default bet.
- Fully adjustable odds: match chance, jackpot chance, and reroll attempts to control how often accidental matches slip through.
- Configurable payout multipliers per match tier (2- through 6-of-a-kind), plus per-emote weight so rare emotes pay more than common ones.
- Adjustable slot count (3–6 reels), emote pool size, and min/max emote weight eligibility.
- Optional Jackpot Pool that accumulates from every loss and pays out on top of a jackpot win, once a minimum bet threshold is met.
- Optional subscriber and VIP payout boosts, stacking additively.
- Optional "Addicted" list (individual users or whole Streamer.bot groups) with some penalties.
- Exclude specific Streamer.bot groups from playing entirely.
- Free Mode for wager-free spins, either globally or per-trigger.
- Auto-detects [Currency Core by StreamUP](https://streamup.tips/product/currency-core) and [LOYALTY POINTS by tawmae](https://tawmae.xyz/loyalty-points).
- Every chat message is editable directly in the settings GUI, including win, loss, jackpot, free-spin, addicted, invalid-bet, and cooldown messages — with a conditional `{jackpot}...{/jackpot}` syntax so jackpot-pool wording only appears when the pool is actually enabled.
- Persistent daily log file with every spin result, filterable and searchable in the built-in log viewer.
- Built-in WPF settings window with dark/light mode, tab navigation, a live payout preview calculator, and a per-platform emote pool editor.

---

## 🎮 How It Works

Chat spins the slots with `!slots <bet>` (or a bet alias). The game rolls the reels, checks for a match against the configured odds, and settles the payout — win, jackpot, or loss — instantly.

| Event | Trigger | Result |
|---------|---------|---------|
| 🎰 **Spin** | A viewer runs the slots command with a bet | The bet is deducted (unless Free Mode) and the reels are rolled. |
| ✅ **Win** | 2 or more slots match | Payout is calculated from the match tier and emote weight, and credited to the viewer's balance. |
| 🔥 **Jackpot** | All slots match | Maximum payout is awarded, plus the accumulated Jackpot Pool if the bet met the minimum threshold. |
| ❌ **Loss** | No match | The bet is lost and added to the Jackpot Pool (unless Free Mode or the player is on the Addicted list). |
| 🚫 **Blocked / Addicted** | Player is on the Blocked or Addicted list | Blocked players can't play at all; Addicted players play normally but with a payout cut and doubled cooldowns. |
| ⏱️ **Cooldown** | Player spins again too soon | A cooldown message is sent instead of a spin. |

---

## 🎫 Channel Points Mode (Twitch only)

When `Only Channel Points` is enabled, the chat command is effectively disabled — only viewers who redeem the configured Channel Point reward can spin. Four bet modes are available:

| Option | Info |
|---------|---------|
| **Cost** | The reward's point cost is the bet |
| **Input** | The viewer types their bet into the reward's text field |
| **Fixed** | Every redemption bets a fixed configured amount |
| **Free** | All redemptions spin for free regardless of cost |

---

# Get Started

[Setup Guide](https://github.com/aaskjer/Slot-Machine-Game/blob/main/Setup-Guide.md)

[Frequently Asked Questions](https://github.com/aaskjer/Slot-Machine-Game/blob/main/FAQ.md)

[Import String for streamer.bot](https://github.com/aaskjer/Slot-Machine-Game/blob/main/Import-String.md)

[Download](https://github.com/aaskjer/Slot-Machine-Game/releases)

---

# Credits & Links

[aaskjer on Twitch](https://twitch.tv/aaskjer)

[Slot Machine Game on SB Discord](https://discord.com/channels/834650675224248362/1446889756297527530/1446889756297527530)

[Streamer.bot](https://streamer.bot) / [nate1280](https://www.patreon.com/c/nate1280/home)

YOU ♡
