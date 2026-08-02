# ❓ Slot Machine Game — FAQ

---

## 🛠️ Setup & Configuration

**Q: Where are the config files stored?**

Everything lives under your Streamer.bot base directory:

```
Chat Games/Slot Machine Game/SMG-Settings.json      ← all settings, messages & emote pools
Chat Games/Slot Machine Game/SMG-Settings.json.bak  ← automatic backup, written before every save
Chat Games/Logs/SMG-log-yyyy-MM-dd.txt              ← daily action log (one file per day)
```

You should never need to edit `SMG-Settings.json` by hand — use the built-in Settings GUI instead.

**Q: The Settings GUI won't open / crashes immediately. What do I do?**

- Check the Streamer.bot log for error details and report it [here](https://github.com/aaskjer/Slot-Machine-Game/issues).
- If `SMG-Settings.json` is malformed, delete it (or restore `SMG-Settings.json.bak`) and reopen the GUI — a fresh default file is generated automatically if none exists.

**Q: How do I reset all settings to defaults?**

Open the Settings GUI and click **Reset to Defaults** (red button, bottom-left). After confirming, this rewrites the entire settings file, including the default emote pools for every platform, and re-applies the default cooldown durations to the Streamer.bot command. The GUI then reopens automatically.

**Q: I saved settings but nothing changed in-game. Why?**

**Save** and **Save & Exit** both write immediately to `SMG-Settings.json`. The game script reloads settings fresh on every command execution, so the very next `!slots` (or whatever your trigger is) picks up the change — no Streamer.bot restart needed. **Cancel** discards anything unsaved and just closes the window.

**Q: What's the ☀️/🌙 button in the bottom-left corner?**

Toggles the Settings GUI between light and dark theme. It saves your preference and reopens the window immediately.

---

## 🎮 Starting & Betting

**Q: How does a bet amount get chosen?**

Whatever the player types after the command maps to an amount:

| Input | Result |
|---|---|
| *(nothing)* | Uses **Default Bet** |
| `all` / `alles` / `all in` | Entire balance |
| `half` / `hälfte` / `50%` | Half of balance |
| `third` / `drittel` / `33%` | A third of balance |
| `quarter` / `viertel` / `25%` | A quarter of balance |
| `random` / `zufall` / `rnd` | A random amount between Min Bet and Max Bet (clamped to what the user can afford) |
| any number | That exact amount |

Aliases are matched case-insensitively, and both English and German phrasing work.

**Q: My bet got rejected — why?**

A bet fails validation (and sends the configured error message) if it's non-numeric/negative/has decimals, exceeds your current balance, falls below **Minimum Bet**, or exceeds **Maximum Bet**. Set Minimum/Maximum Bet to `0` to disable that particular ceiling/floor.

**Q: How do I block specific users or groups from playing entirely?**

Set **Blocked Groups** (General tab) to a comma-separated list of Streamer.bot user groups — members are silently blocked from playing at all, with no message sent. This is different from the **Addicted List** (see below), which still lets users play but with penalties.

---

## 💰 Points & Payouts

**Q: What points system does the game use?**

Auto-detected in this priority order:
1. **StreamUP Currency Core** — reads the `currency_ProductSettings` global.
2. **tawmae Loyalty Points** — reads the `tawmae_Settings_LOYALTY POINTS` global.
3. **Config fallback** — uses **Points Var** / **Points Name** from the General tab.

If you're on a custom currency with a different variable name, set Points Var/Points Name yourself.

**Q: How is a win actually calculated?**

```
rawPayout   = bet × MatchPayout% × emoteWeight ÷ 100
basePayout  = max(round(rawPayout), bet)
payout      = basePayout × RoleBoostMultiplier          (Subscriber/VIP, if applicable)
payout     += JackpotPool                                (only on a jackpot win, if eligible)
payout      = round(payout × (1 − AddictedPayoutCut))    (only if the user is on the Addicted list)
```

`MatchPayout%` is whichever tier (2- through 6-Match Payout) matches how many slots came up the same, and higher-weight emotes pay proportionally more per match.

**Q: What determines whether a spin wins at all?**

**Allow Match Chance (%)** is the odds of a spin producing any match, and **Allow Jackpot Chance (%)** is the odds of every slot matching (jackpot). **Reroll Attempts** controls how hard the game tries to avoid an accidental match on a spin that wasn't meant to win — with a small **Emote Pool Size**, accidental matches can still slip through even after all reroll attempts.

---

## 🎰 Slots & Emotes

**Q: What does Emote Weight actually do?**

Weight selection is inverted: low-weight emotes appear more often but pay less per match, high-weight emotes are rarer but pay more. Only emotes whose weight falls within **Min/Max Emote Weight** are eligible to appear at all — you can use this to exclude the cheapest or the most valuable emotes from a spin entirely.

**Q: How do I edit the emote pool?**

Platform Emotes tab → pick a platform sub-tab → fill in the Emote/Weight fields (Kick also needs an ID and Name) and click **Add**. Click an existing entry in the list to edit or remove it. **Reset to Default** replaces the whole pool for that platform with the built-in 10-emote set.

**Q: Why does Kick need an ID *and* a Name?**

Kick emote codes are built from the numeric ID, e.g. `[emote:1730803:emojiRich]`. Open the emote graphic in a new browser tab to find its ID in the URL.

---

## 💎 Jackpot Pool

**Q: How does the Jackpot Pool grow?**

Every losing bet (from a non-addicted, non-Free Mode spin) adds the lost amount to the pool. It's tracked separately per platform. A player only has a *chance* at winning the pool on top of their normal jackpot payout if they hit the jackpot **and** their bet was at least **Min Jackpot Bet** — winning it resets the pool back to 0.

**Q: I disabled the Jackpot Pool but my messages still mention it. Why?**

They shouldn't — wrap any pool-specific wording in your custom message with `{jackpot}...{/jackpot}`. That whole segment is automatically stripped out whenever **Enable Jackpot Pool** is off, so you can write natural sentences without leftover broken text like "got added to the pool of now Points!".

---

## ⭐ Role Boosts (Subscriber / VIP)

**Q: How do Subscriber/VIP boosts stack?**

Additively:

```
RoleBoostMultiplier = 1.0 + (SubBoost% if subscribed) + (VipBoost% if VIP)
```

Example: 10% sub boost + 20% VIP boost on a 500-point win = `500 × 1.30 = 650`. Both are **Twitch only** — there's no subscriber/VIP concept on YouTube or Kick, so they have no effect there.

---

## 🚫 Addicted List

**Q: What does putting someone on the Addicted list actually do?**

Three things, configured on the **Game** tab:
- Their win (including any jackpot pool bonus) is reduced by **Addicted Payout Cut** — default 50%, hard-capped at 99% so a win can never turn into a net loss.
- If a **User Cooldown** is configured, they always wait **twice** as long between spins as everyone else.
- Their losses **never** contribute to the Jackpot Pool, so they can't intentionally grow it hoping to win it back later.

**Q: Individual users or whole groups?**

Both — **Addicted Users** (comma-separated usernames) and **Addicted Groups** (comma-separated Streamer.bot groups) can be set at the same time; matching either flags the user.

**Q: Do addicted users get a different chat message?**

Yes — **Addicted Win**, **Addicted Loss**, and **Addicted Jackpot** (Messages tab) are used instead of the normal ones. The default Win/Jackpot messages include an `{addictedCutPercent}` placeholder to spell out the penalty, e.g. *"Addiction Fee: your win was cut by 50%"*. These only apply outside of Free Mode — the Free Game messages always take priority for free spins, since no real currency changes hands there.

**Q: Can I preview the effect before saving?**

Yes — the **Live Preview** panel at the bottom of the Game tab includes a 🎯 Addicted row that recalculates live as you type, showing the exact payout range an addicted user would receive.

---

## 🆓 Free Mode

**Q: How do I let people play without risking points?**

Enable **Free Mode** globally in the Game tab. No currency changes hands either way, and dedicated **Free Win/Loss/Jackpot** messages are used instead of the normal ones.

---

## 💬 Messages & Customization

**Q: What placeholders are available?**

Placeholders vary per message — hover any field's label in the GUI for a full tooltip listing what it supports (e.g. `{user}`, `{amount}`, `{currency}`, `{newBalance}`, `{jackpotPoolCurrent}`, `{addictedCutPercent}`). Every message is fully rewritable in the Messages tab.

**Q: A number in chat looks like `52467` instead of `52,467` — how do I fix that?**

Set **Number Separator** (General tab) to whatever character you want as a thousands separator, e.g. `.` or `,`.

---

## ⏱️ Cooldowns

**Q: How are cooldowns enforced?**

**Global Cooldown** and **User Cooldown** (Cooldown tab) are written straight into Streamer.bot's own per-command cooldown system when you save — the game script itself doesn't gate anything except reacting with a chat message when Streamer.bot reports an active cooldown. Addicted users get an *additional*, independently tracked wait on top of the normal User Cooldown (see Addicted List above).

---

## 🎟️ Twitch Channel Points

**Q: How do I let a Channel Points reward trigger a spin?**

1. Enable **Only Channel Points** (Other Modules → Twitch Channel Points tab) — this disables the chat command entirely and only accepts reward redemptions.
2. Paste your **Target Reward ID** (leave blank to accept any reward redemption).
3. Pick a **Bet Mode**.

Channel Points redemptions are a Twitch-only concept, so this has no effect on YouTube or Kick.

**Q: What does each Bet Mode do?**

| Mode | Behaviour |
|---|---|
| `cost` | Bet equals the reward's channel point cost |
| `fixed` | Every redemption bets the exact **Fixed Bet Amount** |
| `input` | User types their bet into the reward's text field |
| `free` | Bet is forced to 0 — free play, no points wagered |

Max Bet is only enforced for `input`/`fixed` modes — `cost` is left uncapped since the reward cost is already streamer-controlled.

---

## 📜 Action Log

**Q: Where do I review past spins?**

Other Modules → **Action-Log** tab. It automatically merges every day's log file into one searchable, filterable table (filter by Result or Platform, free-text search, click any row to see the full raw log line at the bottom). Enable/disable logging entirely with **Write Log** (General tab).

---

## 🌐 Multi-Platform

**Q: Which platforms are supported?**

Twitch, YouTube, and Kick — toggle each on in General → **Select Platform(s)**. The platform is auto-detected from the incoming event, and the Jackpot Pool, points balances, and command cooldowns are all tracked independently per platform.

---

## 🔔 Updates

**Q: How do I know if a new version is out?**

Every time you open the Settings GUI, it checks the GitHub releases API (3-second timeout, fails silently if you're offline). If a newer version exists, you'll get a one-time popup asking whether to open the [releases page](https://github.com/aaskjer/Slot-Machine-Game/releases), and the window title shows a 🔔 marker until you update.

---

# Is Slot Machine Game an AI Slop?

Partially it is. This script has been developed with input from the streamer.bot community and is supported by AI.
But I spent a lot of time putting heart and soul into it, and my goal was to create a robust, fair, and easy-to-use gambling minigame for everyone.
I understand that people, especially IT-savvy people, will dislike the project because of the use of AI, and I absolutely understand and support their point of view.
But I had a lot of fun making it, as with all my other projects, so I used it to "learn" coding and used AI for something valuable.

AI can create bugs, and I am not a developer in classical terms. But I spend a reasonable amount of time fixing any bugs that occur while testing.
If you still find bugs or have something to say, please let me hear it :)
