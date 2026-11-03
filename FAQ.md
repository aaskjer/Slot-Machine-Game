# ❓ Slot Machine Game — FAQ

---

## 🛠️ Setup & Configuration

**Q: Where are the config files stored?**

In your Streamer.bot folder:

```
Chat Games/Slot Machine Game/SMG-Settings.json        ← all settings, messages & emotes
Chat Games/Slot Machine Game/SMG-Settings.json.bak    ← automatic backup, written before every save
Chat Games/Slot Machine Game/uiframework.layout.json  ← your layout of the window: theme, renamed or hidden pages and fields
Chat Games/Logs/SMG-log-yyyy-MM-dd.txt                ← action log, one file per day
UIFramework/lib/<version>/UIFramework.dll             ← the settings window, downloaded on first open
```

There's no need to edit any of them by hand; the settings window covers all of it.

**Q: What is UIFramework.dll, and why does the window want to download something?**

The settings window is no longer part of the import. It lives in [UIFramework for streamer.bot](https://github.com/aaskjer/UIFramework-Streamer.bot),
one window shared by all of these chat games, so a fix or a new feature there reaches every game at once. The
`[SMG] - Settings` action only loads that DLL and hands it the game's settings table.

The first open asks before fetching anything. `Yes` downloads the file from the UIFramework releases, checks it
against the SHA-256 published next to it and puts it in `UIFramework\lib\<version>\` under your Streamer.bot
folder. `No` opens that folder so you can place the file yourself. Later releases are offered the same way;
`Cancel` skips one, and `"autoUpdate": false` in `uiframework.layout.json` stops the check altogether. If the log
says `UIFramework.dll was not found`, open the window again and answer `Yes`, or put the DLL from the
[releases](https://github.com/aaskjer/UIFramework-Streamer.bot/releases) into that folder by hand.

**Q: The settings window won't open or closes right away. What do I do?**

- Check the Streamer.bot log for the error and report it [here](https://github.com/aaskjer/Slot-Machine-Game/issues).
- A damaged `SMG-Settings.json` doesn't keep the window shut. It opens with the settings from `SMG-Settings.json.bak`, or with the defaults if there's no readable backup, and keeps the damaged file as `SMG-Settings.json.broken`. Save writes a working file again.

**Q: Can I rearrange the window?**

Yes. The pencil at the bottom left switches to the customise mode: drag a field onto another to reorder it, onto a
page in the rail to move it there, right-click for *Rename*, *Hide* and *Move to page*; pages can be renamed,
reordered, given another icon or hidden the same way. The bar on top picks the accent colour, and *Reset layout*
puts everything back. It all lives in `uiframework.layout.json` next to `SMG-Settings.json`, so an update of the
game never undoes it. A hidden field keeps its value.

**Q: How do I reset all settings to defaults?**

The circular arrow at the bottom left resets every page, the half arrow only the page in front of you; both ask
first and write nothing until you save. A reset of everything puts the default emotes back on every platform and,
once saved, takes the command's cooldowns back to 0. Your theme and your layout of the window stay.

**Q: I saved my settings, but nothing changed in the game. Why?**

**Save** and **Save & Exit** write to `SMG-Settings.json` at once, and the game reads that file fresh on every spin. The very next `!slots` uses the new settings, with no Streamer.bot restart. Cooldowns reach the command the moment you save. **Cancel** closes the window and drops anything unsaved.

**Q: What does the ☀️/🌙 button at the bottom left do?**

It switches the settings window between dark and light. The choice is saved in `uiframework.layout.json` and shared with every other window built on UIFramework; the page is rebuilt in place, and your unsaved changes stay.

---

## 🎮 Starting & Betting

**Q: How is the bet chosen?**

By what the player types after the command:

| Input | Bet |
|---|---|
| *(nothing)* | The **Default bet** |
| `all` / `alles` / `all in` | The whole balance |
| `half` / `hälfte` / `50%` | Half the balance |
| `third` / `drittel` / `33%` | A third of the balance |
| `quarter` / `viertel` / `25%` | A quarter of the balance |
| `random` / `zufall` / `rnd` | A random amount between Minimum and Maximum bet, capped at what the player can afford |
| any number | Exactly that amount |

Upper or lower case doesn't matter, and the German words work just like the English ones.

**Q: My bet got rejected. Why?**

A bet is refused, with the matching error message, if it isn't a whole positive number, is more than the balance, or lies below the **Minimum** or above the **Maximum** bet. Set Minimum or Maximum to `0` to switch that limit off.

**Q: How do I block specific users or groups from playing entirely?**

Add their Streamer.bot user groups under **Blocked groups** on the Access page: type a group name and press Enter. Members can't play and get no message; a channel point redemption of theirs is refunded. That's different from the **Addicted** list (see below), whose members still play, with penalties.

---

## 💰 Points & Payouts

**Q: Which points system does the game use?**

It checks in this order:
1. **StreamUP Currency Core**, through the `currency_ProductSettings` global.
2. **tawmae LOYALTY POINTS**, through the `tawmae_Settings_LOYALTY POINTS` global.
3. **Its own settings**: **Points variable** and **Shown in chat as** on the Game page.

On a custom currency with a different variable name, enter that name there.

**Q: How exactly is a win calculated?**

```
rawPayout   = bet × MatchPayout% × emoteWeight ÷ 100
basePayout  = max(round(rawPayout), bet)
payout      = basePayout × RoleBoostMultiplier          (Subscriber/VIP, if applicable)
payout     += JackpotPool                                (only on a jackpot win, if eligible)
payout      = round(payout × (1 − AddictedPayoutCut))    (only if the user is on the Addicted list)
```

`MatchPayout%` comes from the payout row for the number of matching slots, 2 to 5 alike. When every slot matches, the jackpot row applies instead, whatever the number of slots. Higher-weight emotes pay proportionally more.

**Q: What determines whether a spin wins at all?**

The jackpot comes first: **Jackpot chance %** of all spins land it, every slot alike. Of the other spins, **Match chance %** may land matching slots. Their slots are drawn freely, so a match is likely but not certain. Every remaining spin rerolls repeats to avoid a match, and **Rerolls** sets how hard it tries; with a small **Emote pool**, an accidental match can still slip through after every reroll. Free draws can land all alike too, so jackpots come a little more often than Jackpot chance % says.

So the two chances aren't the win rate itself. **What really comes out** on the Game page works out the real odds of your settings, from 30,000 test spins with the game's own engine and the values as they stand in the window: how often a spin ends in a jackpot, a win or a loss, and what a bet of 100 comes back as on average. It follows every change you type.

---

## 🎰 Slots & Emotes

**Q: What does an emote's weight actually do?**

Weight works in reverse for how often an emote comes up: low-weight emotes appear often and pay less per match, high-weight ones are rarer and pay more. Only emotes with a weight between **Min weight** and **Max weight** can appear at all, which lets you leave out the cheapest or the most valuable ones.

**Q: How do I edit the emotes?**

On the Emotes page, each platform has its own list: one row per emote with the emote as chat types it, its picture beside it once it is known, its weight and a name of your choosing. **Add row** adds one, **×** takes one out, and **Restore defaults** puts the built-in set of 10 back for that platform. Rows without an emote are dropped when you save.

**Q: How do I enter a Kick emote?**

Kick shows `[emote:ID:name]` as the emote, so that is what goes into the row, e.g. `[emote:1730803:emojiRich]`. To find the ID, open the emote's picture in a new browser tab: it's the number in the address (`https://files.kick.com/emotes/1730803/fullsize`).

---

## 💎 Jackpot Pool

**Q: How does the Jackpot Pool grow?**

Every bet lost in points goes in, unless the player is addicted or the spin is free. Channel point redemptions in `cost` or `fixed` mode stake channel points and add nothing. Chat calls the pool the **Jackpool**, and each platform has its own. A player wins it on top of the normal jackpot payout only by hitting the jackpot with a bet of at least **Bet to win the pool**; the pool then starts again at 0.

**Q: I turned the Jackpot Pool off, but my messages still mention it. Why?**

Wrap anything about the pool in `{jackpot}...{/jackpot}` in your own messages. While **Jackpot pool** is off, the game drops that whole part, so chat never sees broken leftovers like "got added to the pool of now Points!".

---

## ⭐ Role Boosts (Subscriber / VIP)

**Q: How do Subscriber and VIP boosts stack?**

They add up:

```
RoleBoostMultiplier = 1.0 + (SubBoost% if subscribed) + (VipBoost% if VIP)
```

With a 10% subscriber and a 20% VIP boost, a 500-point win pays `500 × 1.30 = 650`. Both boosts are **Twitch only**: on YouTube and Kick the game doesn't check for subscribers or VIPs, so they have no effect there.

---

## 🚫 Addicted List

**Q: What does putting someone on the Addicted list actually do?**

Three things:
- Their win, including any Jackpool, shrinks by the **Addicted cut** on the Game page: 50% by default and capped at 99%, so a win always pays something, even if that's less than the bet.
- If a **Per viewer** cooldown is set, it also holds them on channel point redemptions, which Streamer.bot's command cooldown doesn't cover.
- Their losses **never** go into the Jackpot Pool, so they can't grow it on purpose and hope to win it back later.

**Q: Individual users or whole groups?**

Both. Add names under **Addicted viewers** and Streamer.bot groups under **Addicted groups** on the Access page; a match in either one counts.

**Q: Do addicted users get different chat messages?**

Yes. **Addicted Win**, **Addicted Loss** and **Addicted Jackpot** on the Messages page replace the normal ones. The default Addicted Win and Jackpot messages spell out the penalty with `{addictedCutPercent}`, e.g. *"Addiction Fee: your win was cut by 50%"*. Free spins always get the Free messages instead, since no points change hands there.

**Q: Can I preview the effect before saving?**

Yes. Under **Try a spin** on the Game page, pick **Addicted** as the one who spins and click **Spin**: it plays a round with the settings as they stand in the window, saved or not, and shows the slots and the exact message with their cut applied.

---

## 🆓 Free Mode

**Q: How do I let people play without risking points?**

Switch on **Free mode** on the Game page. No points change hands, and the **Free Win**, **Free Loss** and **Free Jackpot** messages replace the normal ones.

---

## 💬 Messages & Customization

**Q: Which placeholders are available?**

That depends on the message. On the Messages page, the placeholders of the selected message sit as buttons below its text: click one to insert it, hover over it to see what it stands for (e.g. `{user}`, `{amount}`, `{currency}`, `{newBalance}`, `{jackpotPoolCurrent}`, `{addictedCutPercent}`). Every message can be rewritten there.

**Q: A number in chat shows as `52467` instead of `52,467`. How do I fix that?**

Pick the format under **Numbers** on the Messages page, e.g. `12.345` or `12,345`.

---

## ⏱️ Cooldowns

**Q: How are cooldowns enforced?**

**Everyone** and **Per viewer** under **Cooldowns** on the Access page go straight into the Streamer.bot command's own cooldowns when you save. The game itself holds nothing up; it only answers in chat when Streamer.bot reports a running cooldown. For addicted players it applies the per-viewer cooldown itself, so it holds them on channel point redemptions too (see Addicted List above).

---

## 🎟️ Twitch Channel Points

**Q: How do I let a Channel Points reward trigger a spin?**

1. Switch on **Channel points start a spin** on the Access page. On Twitch this turns the chat command off, so only the reward starts a spin there.
2. Paste your **Reward ID**. Other rewards are left alone, and without a Reward ID no redemption starts a spin.
3. Pick what is bet: **Reward cost**, **Typed amount**, **Fixed** or **Free**.

The slot machine takes channel point redemptions from Twitch only, so on YouTube and Kick the chat command keeps working in this mode.

**Q: What does each bet mode do?**

| Mode | Behaviour |
|---|---|
| `cost` | The reward's channel point cost is the bet, and the channel points are the stake: a loss doesn't touch the viewer's points, a win is paid in points |
| `fixed` | Every redemption bets the exact **Fixed bet**, staked in channel points like `cost` |
| `input` | The viewer types a bet in their own points into the reward's text field; it's checked against their balance, and a loss takes it off |
| `free` | The bet is 0: free play, nothing wagered, and the Free messages are used |

Minimum and Maximum bet only apply to `input` and `fixed`. `cost` has no cap, since you already set the reward's price.

---

## 📜 Action Log

**Q: Where do I review past spins?**

On the Log page. It merges every day's log file into one table: search it for names, platforms or amounts, filter by result or date, and click a row to see its full log line below. **Write a log file per day**, under the table, switches logging on or off.

---

## 🌐 Multi-Platform

**Q: Which platforms are supported?**

Twitch, YouTube and Kick, all at once: the game plays on every platform its chat command listens to. To leave a platform out, untick it in the command in Streamer.bot (for example **Kick Message**). The platform is detected from the incoming event, and each platform keeps its own Jackpot Pool, points balances and command cooldowns.

**Q: Does "Send as /me" work on YouTube and Kick?**

No, /me exists on Twitch only. On YouTube and Kick the messages always go out as plain chat, whatever the switch says, and the settings window marks both /me switches **Twitch only**.

---

## 🔔 Updates

**Q: How do I know if a new version is out?**

Every time the settings window opens, it asks GitHub's releases API in the background (offline, it stays silent). If a newer version of the game exists, a pill appears in the header; click it to open the [releases page](https://github.com/aaskjer/Slot-Machine-Game/releases). A newer UIFramework is offered in a dialog instead, and shows as a pill only after you answered `No` to it.

---

# Is Slot Machine Game an AI Slop?

Partially it is. This script has been developed with input from the streamer.bot community and is supported by AI.
But I spent a lot of time putting heart and soul into it, and my goal was to create a robust, fair, and easy-to-use gambling minigame for everyone.
I understand that people, especially IT-savvy people, will dislike the project because of the use of AI, and I absolutely understand and support their point of view.
But I had a lot of fun making it, as with all my other projects, so I used it to "learn" coding and used AI for something valuable.

AI can create bugs, and I am not a developer in classical terms. But I spend a reasonable amount of time fixing any bugs that occur while testing.
If you still find bugs or have something to say, please let me hear it :)
