<div align="center">

# 🌸 AkariChan AIO
### All-In-One Discord Bot — Music · Economy · Moderation · AntiNuke · Reaction & More

**Developed by [NighxDev](https://github.com/nighxdev) · Maintained by AkiForever**

---

![Version](https://img.shields.io/badge/Version-1.0.0-ff6b9d?style=for-the-badge)
![Discord.js](https://img.shields.io/badge/discord.js-v14-5865F2?style=for-the-badge)
![Node](https://img.shields.io/badge/Node.js-v18+-339933?style=for-the-badge)
![License](https://img.shields.io/badge/License-All%20Rights%20Reserved-red?style=for-the-badge)

</div>

---

## 📌 Overview

**AkariChan AIO** is a powerful, feature-rich Discord bot built on **discord.js v14** with hybrid sharding, SQLite persistence, and Lavalink music playback. Covering 220+ commands across 13 categories — from high-quality music to advanced server security — AkariChan is your server's all-in-one solution.

---

## ✨ Feature Highlights

| Feature | Details |
|---|---|
| 🎵 **Music** | YouTube, Spotify, Apple Music, Deezer, SoundCloud — queue, filters, lyrics, autoplay, 24/7 |
| 💰 **Economy** | Full RPG economy — jobs, dungeons, pets, quests, gambling, shops, prestige, stocks |
| 🛡️ **AntiNuke** | Real-time protection against mass bans, kicks, channel deletes, role deletions |
| ⚔️ **Moderation** | Ban, kick, mute, warn, slowmode, nickname, mass-ban, voice move |
| 🎭 **Reactions** | 29 anime GIF reactions — hug, slap, kill, kiss, punch and more |
| 🎟️ **Tickets** | Full panel-based ticket system with transcripts and staff roles |
| 🎉 **Giveaways** | Start, end, list, reroll giveaways easily |
| ✅ **Verification** | Button-based member verification with custom roles |
| 🔧 **Config** | Per-server prefix, 24/7 mode, music source, ignored channels |
| 📊 **Utility** | User/server/role/channel info, avatar, banner, audit logs, presence |

---

## ⚙️ Requirements

- **Node.js** v18 or higher
- **Lavalink** server v4+ running
- **Discord Bot Token** with the following intents enabled:
  - `GUILDS`, `GUILD_MEMBERS`, `GUILD_MESSAGES`
  - `GUILD_VOICE_STATES`, `MESSAGE_CONTENT`
  - `GUILD_MESSAGE_REACTIONS`
- **Spotify** API credentials (for Spotify support)
- **Last.fm** API key (for artist radio / similar tracks)

---

## 🚀 Installation

### Step 1 — Get the Source Code
AkariChan AIO is **not publicly hosted on GitHub.**
Download the bot source code directly from our Discord support server:

> 📥 **[Join the Support Server to Download](https://discord.gg/tqaQYFezwm)**

Once inside, find the **#bot-download** or **#releases** channel and download the latest `.zip` file.

### Step 2 — Upload & Extract
Upload the `.zip` to your host (VPS, Replit, panel, etc.) and extract it.

### Step 3 — Install Dependencies
```bash
npm install
```

### Step 4 — Configure the Bot
Edit `src/config.json` with your bot token and settings. *(See configuration guide below.)*

### Step 5 — Start the Bot
```bash
npm start
```

---

## 🔧 How to Configure the Bot

All configuration lives in **`src/config.json`**. This is the only file you need to edit to get the bot running.

```json
{
  "token": "YOUR_BOT_TOKEN_HERE",
  "prefix": "-",
  "ownerID": ["YOUR_DISCORD_USER_ID"],

  "SpotifyID": "YOUR_SPOTIFY_CLIENT_ID",
  "SpotifySecret": "YOUR_SPOTIFY_CLIENT_SECRET",
  "LastFmKey": "YOUR_LASTFM_API_KEY",
  "LastFmSecret": "YOUR_LASTFM_SECRET",

  "color": "#00D4FF",
  "logs": "CHANNEL_ID_FOR_LOGS",

  "links": {
    "support": "https://discord.gg/YOUR_SUPPORT_SERVER",
    "invite": "https://discord.com/oauth2/authorize?client_id=YOUR_BOT_ID&permissions=8&scope=bot",
    "guild": "https://discord.gg/YOUR_GUILD"
  },

  "Webhooks": {
    "black": "WEBHOOK_URL",
    "guild_join": "WEBHOOK_URL",
    "guild_leave": "WEBHOOK_URL",
    "cmdrun": "WEBHOOK_URL"
  },

  "nodes": [
    {
      "name": "MainNode",
      "url": "your-lavalink-host:port",
      "auth": "your-lavalink-password",
      "secure": false
    }
  ]
}
```

### 🔑 Field Reference

| Field | What It Does |
|---|---|
| `token` | Your Discord bot token from the [Developer Portal](https://discord.com/developers/applications) |
| `prefix` | Default command prefix (e.g. `-`, `!`, `.`) |
| `ownerID` | Array of Discord user IDs with full bot ownership |
| `SpotifyID / SpotifySecret` | From [Spotify Developer Dashboard](https://developer.spotify.com/dashboard) |
| `LastFmKey / LastFmSecret` | From [Last.fm API](https://www.last.fm/api/account/create) |
| `color` | Accent hex color used in embeds |
| `logs` | Channel ID where bot logs are sent |
| `links.support` | Your support Discord server invite link |
| `links.invite` | Bot invite link (replace `YOUR_BOT_ID`) |
| `nodes` | Lavalink node connection details |
| `Webhooks` | Optional Discord webhook URLs for event logging |

---

## 🛠️ How to Modify the Bot (Easy Guide)

### ➕ Add a New Command

1. Go to `src/commands/<Category>/`
2. Create a new file, e.g. `mycommand.js`
3. Use this template:

```js
const { ContainerBuilder, TextDisplayBuilder, MessageFlags } = require('discord.js');

module.exports = {
  name: 'mycommand',
  aliases: ['mc'],
  category: 'Utility',
  description: 'Does something cool',
  cooldown: 5,
  slashOptions: [],

  async execute(message, args, client) {
    return message.reply({
      components: [
        new ContainerBuilder().addTextDisplayComponents(
          new TextDisplayBuilder().setContent('Hello from mycommand!')
        )
      ],
      flags: MessageFlags.IsComponentsV2
    });
  }
};
```

4. Restart the bot — it auto-loads all commands from the `src/commands/` folder.

---

### ✏️ Change the Prefix

Edit `src/config.json`:
```json
"prefix": "!"
```

Or use the `-setprefix` command in Discord.

---

### 🎨 Change Bot Embed Color

Edit `src/config.json`:
```json
"color": "#FF69B4"
```

---

### 🔇 Add an Ignored Channel

Use the `-ignore` command in any channel to stop the bot from responding there.

---

### 🔗 Add a Lavalink Node

Add to the `nodes` array in `src/config.json`:
```json
{
  "name": "BackupNode",
  "url": "lavalink.example.com:2333",
  "auth": "yourpassword",
  "secure": false
}
```

---

### 🚫 Blacklist a User

Use the `-blacklist add @user` command as a bot owner.

---

### 👑 Add Another Owner

Add their Discord user ID to `ownerID` in `src/config.json`:
```json
"ownerID": ["123456789012345678", "987654321098765432"]
```

---

## 📋 Commands Reference

> **Total: 221 Commands across 13 Categories**
> Prefix: `-` (configurable) · All commands also available as slash commands

---

### 🛡️ AntiNuke — 10 Commands

| Command | Aliases | Description |
|---|---|---|
| `antinuke` | `an`, `nuke`, `security` | AntiNuke security dashboard for your server |
| `anlogs` | `nukelogs`, `antiloggingchannel` | Set or clear the anti-nuke log channel |
| `anstatus` | `nukestatus`, `antistatus` | View the full anti-nuke configuration dashboard |
| `anbypass` | `nukebypass`, `bypass` | Manage trusted users who bypass anti-nuke detection |
| `anlimits` | `nukelimits`, `antilimit` | Set custom action limits for the anti-nuke system |
| `anmodules` | `nukemodules`, `anmod` | Toggle individual anti-nuke protection modules |
| `anpunishment` | `anpunish`, `nukepunish` | Set the punishment applied to nukers |
| `anstrict` | `nukestrictlevel`, `strict` | Set strict level (1=Low → 4=Paranoid) |
| `anwhitelist` | `nukewl`, `anwl` | Add or remove users/roles from the whitelist |
| `anwlchannel` | `nukewlchan` | Whitelist a channel from anti-nuke checks |

---

### ⚙️ Config — 4 Commands

| Command | Aliases | Description |
|---|---|---|
| `setprefix` | `prefix` | Change the server command prefix |
| `247` | `24/7`, `alwayson` | Enable or disable 24/7 voice mode |
| `ignore` | `ig` | Toggle bot ignoring a channel |
| `source` | — | Set preferred music source |

---

### 💰 Economy — 76 Commands

| Command | Aliases | Description |
|---|---|---|
| `balance` | `bal`, `wallet`, `money` | Check your or someone's balance |
| `daily` | `claim`, `dailyreward` | Claim your daily reward |
| `weekly` | `weeklyclaim` | Claim your weekly reward |
| `monthly` | `monthlyclaim` | Claim your monthly reward |
| `work` | `earn`, `job` | Work and earn coins |
| `beg` | — | Beg for coins |
| `fish` | `fishing`, `cast` | Go fishing and earn coins |
| `mine` | `mining`, `dig` | Mine for ores and earn coins |
| `hunt` | `hunting`, `shoot` | Go hunting and earn coins |
| `crime` | `criminal` | Commit a crime for big rewards (or get caught) |
| `rob` | `steal`, `mug` | Rob someone's wallet |
| `bankrob` | `robbank`, `heistbank` | Rob the Akari Bank (high risk!) |
| `heist` | `bankheist`, `robbery` | Organize a group bank heist |
| `pickpocket` | `pocket`, `filch` | Pickpocket someone (30% success) |
| `deposit` | `dep` | Deposit coins into your bank |
| `withdraw` | `with`, `wd` | Withdraw coins from your bank |
| `pay` | `give`, `transfer` | Transfer coins to another user |
| `donate` | `contribution` | Donate to the server jackpot pool |
| `bank` | `account` | View your bank account details |
| `balance` | `bal`, `wallet` | Check balance |
| `networth` | `nw`, `worth` | View your total net worth |
| `leaderboard` | `lb`, `top`, `richest` | Economy leaderboard |
| `eprofile` | `econprofile`, `ep` | View economy profile |
| `multiplier` | `multi`, `boost` | View active coin multipliers |
| `income` | `passive`, `earnings` | View passive income sources |
| `salary` | `payday` | Collect passive salary |
| `collect` | `hourly` | Collect hourly passive income |
| `invest` | `investment` | Invest coins for returns |
| `stocks` | `stock` | Buy and sell virtual stocks |
| `loan` | `borrow` | Take a loan from Akari Bank |
| `repay` | `payloan` | Repay your loan |
| `vault` | `safebox`, `safe` | Secure vault — safe from robbery |
| `piggybank` | `piggy`, `savings` | View or smash your piggy bank |
| `shop` | `store`, `market` | Browse the server shop |
| `buy` | `purchase` | Buy an item from the shop |
| `sell` | `sellitem` | Sell an item from your inventory |
| `inventory` | `inv`, `bag`, `items` | View your inventory |
| `setshop` | `addshop` | Manage the server shop (Admin) |
| `restock` | `shopstock` | Restock a shop item (Admin) |
| `craft` | `forge`, `make` | Craft items for coin rewards |
| `upgrade` | `upgrades` | Upgrade your tools |
| `pet` | `pets`, `companion` | Manage your pet companion |
| `quest` | `quests` | View and track daily quests |
| `achievements` | `ach`, `badges` | View your achievements |
| `transactions` | `history`, `txns` | View recent transaction history |
| `streak` | `streaks` | View your streak info and bonuses |
| `prestige` | — | Reset economy for prestige bonuses |
| `coinflip` | `cf`, `flip` | Flip a coin — double or lose |
| `gamble` | `bet`, `g` | Gamble coins for a chance to double |
| `betall` | `allin`, `yolo` | Bet your entire wallet |
| `blackjack` | `bj`, `21` | Play blackjack against the dealer |
| `dice` | `diceroll` | Roll dice and bet |
| `highlow` | `hilo`, `hl` | Higher or lower card game |
| `slots` | `slot` | Play the slot machine |
| `spinwheel` | `wheel`, `fortunewheel` | Spin the prize wheel (hourly) |
| `scratch` | `scratchcard` | Scratch a card to win |
| `rps` | `rockpaperscissors` | Rock Paper Scissors for coins |
| `trivia` | `quiz` | Answer trivia to earn coins |
| `guess` | `numbguess` | Guess a number 1-100 (5 tries) |
| `puzzle` | `mathquiz` | Solve a math puzzle for coins |
| `duel` | `battle`, `pvp` | 1v1 coin duel with someone |
| `challenge` | `wager` | Challenge someone to a mini-game |
| `race` | `horserace` | Bet on a horse race |
| `boss` | `bossfight` | Fight a powerful boss (2h cooldown) |
| `dungeon` | — | Enter a dungeon for rewards |
| `explore` | `adventure` | Explore a zone for loot |
| `loot` | `lootbox`, `crate` | Open a loot crate (hourly) |
| `heist` | `bankheist` | Group bank heist |
| `jackpot` | `megapot` | View and enter the server jackpot |
| `lottery` | `lotto`, `ticket` | Buy a lottery ticket |
| `airdrop` | `drop` | Airdrop coins to members (Admin) |
| `addmoney` | `givemoney` | Add coins to a user (Admin) |
| `removemoney` | `takecoins` | Remove coins from a user (Owner) |
| `reseteco` | `ecoreset` | Reset a user's economy (Owner) |
| `marry` | `propose`, `wed` | Propose marriage for bonuses |
| `divorce` | `breakup` | End your marriage |
| `gift` | `present` | Send a gift box of coins |
| `trade` | `barter`, `exchange` | Trade items with another user |

---

### 🎵 Music — 34 Commands

| Command | Aliases | Description |
|---|---|---|
| `play` | `p` | Play a song or playlist |
| `pause` | — | Pause playback |
| `resume` | `r` | Resume playback |
| `skip` | `s` | Skip the current song |
| `forceskip` | `fs` | Force skip (ignores votes) |
| `stop` | — | Stop music and clear queue |
| `queue` | `q` | Show the queue |
| `nowplaying` | `np` | Show current song |
| `volume` | `v`, `vol` | Set playback volume |
| `loop` | — | Toggle loop mode |
| `shuffle` | — | Shuffle the queue |
| `seek` | — | Seek to a position |
| `rewind` | `rw` | Rewind by seconds |
| `forward` | `ff` | Fast forward by seconds |
| `speed` | `tempo` | Change playback speed |
| `move` | `mv` | Move bot to your voice channel |
| `join` | `j` | Join a voice channel |
| `leave` | `dc`, `disconnect` | Leave voice channel |
| `remove` | `rm` | Remove a track from the queue |
| `clearqueue` | `cq` | Clear the entire queue |
| `skipto` | `jump` | Skip to a queue position |
| `previous` | `back`, `prev` | Play previous song |
| `replay` | `restart`, `rp` | Replay current song |
| `search` | `find` | Interactively search for songs |
| `lyrics` | `ly` | Get lyrics for current song |
| `grab` | `save` | Send current song info to DMs |
| `history` | `played` | Recently played songs |
| `autoplay` | `ap` | Toggle autoplay mode |
| `artistradio` | `ar`, `radio` | Start an artist radio via Last.fm |
| `similar` | `sim`, `related` | Find similar songs |
| `mood` | `genre`, `vibe` | Play music by mood or genre |
| `sleep` | `sleeptimer` | Stop music after a duration |
| `leavecleanup` | `lc` | Remove absent users' songs |
| `forcefix` | `fix` | Force-fix a broken music player |

---

### ⭐ Favourite — 5 Commands

| Command | Aliases | Description |
|---|---|---|
| `like` | `fav`, `favourite` | Like the current song |
| `unlike` | `delfav`, `removefav` | Remove a song from favourites |
| `likeall` | `lall` | Like all songs in the queue |
| `showliked` | `liked`, `favorites` | Show your liked songs |
| `playliked` | `pfav`, `playfav` | Play your liked songs |

---

### 🎛️ Filters — 1 Command

| Command | Aliases | Description |
|---|---|---|
| `filter` | `eq`, `filters` | Apply audio filters (bass, 8D, nightcore, etc.) |

---

### 🎉 Giveaway — 4 Commands

| Command | Aliases | Description |
|---|---|---|
| `giveaway` | `gw`, `gstart` | Start a giveaway |
| `gend` | `giveawayend` | End a giveaway early |
| `greroll` | `giveawayreroll` | Reroll giveaway winners |
| `glist` | `giveaways` | List all active giveaways |

---

### ℹ️ Information — 7 Commands

| Command | Aliases | Description |
|---|---|---|
| `help` | `h`, `commands` | Interactive command browser |
| `ping` | `latency`, `pong` | Show bot latency |
| `stats` | `botinfo`, `bi` | Detailed bot statistics |
| `uptime` | `up` | Show bot uptime |
| `invite` | `invitelink` | Get the bot invite link |
| `support` | `supportserver` | Get the support server link |
| `users` | `botusers` | Show total users and servers |

---

### ⚔️ Moderation — 16 Commands

| Command | Aliases | Description |
|---|---|---|
| `ban` | `banish`, `permaban` | Ban a member |
| `unban` | `pardon` | Unban a user |
| `kick` | `boot`, `remove` | Kick a member |
| `mute` | `timeout`, `silence` | Timeout a member |
| `unmute` | `untimeout`, `unsilence` | Remove timeout |
| `warn` | `warning`, `caution` | Issue a warning |
| `warnings` | `warns`, `warnlist` | View warnings for a member |
| `clear` | `purge`, `clean` | Bulk delete messages |
| `lock` | `lockdown` | Lock a channel |
| `unlock` | `unlockchannel` | Unlock a channel |
| `slowmode` | `slow`, `ratelimit` | Set channel slowmode |
| `role` | `giverole`, `addrole` | Add or remove a role |
| `nick` | `nickname`, `setnick` | Change a member's nickname |
| `deafen` | `deaf` | Server deafen a member |
| `massban` | `mban`, `bulkban` | Mass ban by user IDs |
| `movemember` | `moveto`, `vcmove` | Move member to another voice channel |

---

### 🎭 Reaction — 29 Commands

| Command | Aliases | Description |
|---|---|---|
| `hug` | — | Hug someone |
| `kiss` | — | Kiss someone |
| `slap` | — | Slap someone |
| `pat` | — | Give a head pat |
| `punch` | — | Punch someone |
| `kill` | — | Kill someone (anime style) |
| `bite` | — | Bite someone |
| `lick` | — | Lick someone |
| `poke` | — | Poke someone |
| `cuddle` | — | Cuddle with someone |
| `feed` | — | Feed someone |
| `nom` | — | Nom on someone |
| `highfive` | `hifive` | High five someone |
| `wave` | — | Wave at someone |
| `wink` | — | Wink at someone |
| `nod` | — | Nod in agreement |
| `shrug` | — | Shrug |
| `facepalm` | `fp` | Facepalm |
| `stare` | — | Stare intensely |
| `cry` | — | Cry with an anime GIF |
| `laugh` | `lol` | Laugh |
| `blush` | — | Blush |
| `smile` | — | Smile |
| `angry` | `rage` | Show anger |
| `bored` | — | Show boredom |
| `dance` | `animedance` | Dance |
| `yeet` | — | Yeet someone into the void |
| `thumbsup` | `approve` | Thumbs up |
| `rkick` | `animekick` | Anime kick (reaction only) |

---

### 🎟️ Ticket — 1 Command

| Command | Aliases | Description |
|---|---|---|
| `ticket` | `tkt`, `tickets` | Full ticket system management dashboard |

---

### 🛠️ Utility — 15 Commands

| Command | Aliases | Description |
|---|---|---|
| `userinfo` | `ui`, `whois` | Detailed user information |
| `serverinfo` | `si`, `guildinfo` | Detailed server information |
| `avatar` | `av`, `pfp` | View a user's avatar |
| `banner` | `userbanner`, `ub` | View a user's banner |
| `serverbanner` | `sbanner` | View the server banner |
| `servericon` | `sicon` | View the server icon |
| `channelinfo` | `ci`, `channel` | Detailed channel information |
| `roleinfo` | `ri`, `role` | Detailed role information |
| `membercount` | `mc`, `members` | Server member statistics |
| `boostcount` | `bc`, `boosts` | Server boost count |
| `presence` | `activity`, `status` | View a user's status & activity |
| `audit` | `auditlog` | View recent audit log entries |
| `firstmsg` | `fm` | Get the first message in a channel |
| `checkvanity` | `cv` | Check if a vanity URL is available |
| `timer` | `remindme`, `tm` | Set a reminder timer |

---

### ✅ Verification — 3 Commands

| Command | Aliases | Description |
|---|---|---|
| `verification` | `vsetup` | Set up the verification system |
| `vconfig` | `verconfig` | Configure verification settings |
| `verify` | — | Verify yourself in the server |

---

### 🎙️ Voice — 1 Command

| Command | Aliases | Description |
|---|---|---|
| `voice` | `vc` | Voice moderation commands |

---

### 👑 Owner — 15 Commands

| Command | Aliases | Description |
|---|---|---|
| `blacklist` | `bl` | Blacklist a user globally |
| `noprefix` | `nopfx` | Grant no-prefix access |
| `nopaccess` | `nop` | Manage global no-prefix access |
| `serverlist` | `sl`, `servers` | List all servers the bot is in |
| `leaveserver` | `lv` | Force the bot to leave a server |
| `reload` | `rd`, `reloadall` | Reload commands without restart |
| `restart` | `reboot` | Restart the bot |
| `node` | — | Show Lavalink node info |
| `team` | — | Manage the bot team and ranks |
| `badge` | — | Add or remove user badges |
| `branding` | `setprofile` | Customize bot avatar/banner/bio |
| `backup` | — | Create a source code backup |
| `getinv` | `ginv` | Get an invite for any server |
| `mutual` | `mutualservers` | Show mutual servers with a user |
| `active` | `playing` | Show active music players |

---

## 📁 Project Structure

```
akarichan-aio/
├── index.js                  # Main bot entry
├── Shard.js                  # Shard manager
├── src/
│   ├── commands/             # All commands (organized by category)
│   │   ├── AntiNuke/
│   │   ├── Config/
│   │   ├── Economy/
│   │   ├── Favourite/
│   │   ├── Filters/
│   │   ├── Giveaway/
│   │   ├── Information/
│   │   ├── Moderation/
│   │   ├── Music/
│   │   ├── Owner/
│   │   ├── Reaction/
│   │   ├── Ticket/
│   │   ├── Utility/
│   │   ├── Verification/
│   │   └── Voice/
│   ├── events/               # Discord event handlers
│   ├── structures/           # Bot client, database
│   ├── utils/                # Helper utilities
│   ├── emojis.js             # All bot emojis
│   └── config.json           # Bot configuration
├── package.json
└── README.md
```

---

## 🚀 Running the Bot

```bash
# Production (with sharding)
npm start

# Development (auto-restart on changes)
npm run dev
```

---

## 📜 License & Legal

```
Copyright © 2025–2026 NighxDev & AkiForever. All Rights Reserved.

This software and its source code are the exclusive property of NighxDev and AkiForever.
Unauthorized copying, distribution, modification, or commercial use of this software,
in whole or in part, is strictly prohibited without prior written permission from the authors.

AkariChan AIO is provided for personal and community use only.
Redistribution in any form is not permitted.
```

> **All Rights Reserved — NighxDev · AkiForever · AkariChan AIO**

---

<div align="center">

Made with ❤️ by **NighxDev** & **AkiForever**

*AkariChan AIO — Your server's everything bot.*

</div>
