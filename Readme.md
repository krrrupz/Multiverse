<div align="center">

# 🌌 Discord Multiverse Bot

### Cross-Server Message Relay • Anti-Spam • Link Filtering

Connect servers through matching `#multiverse` channels using Discord webhooks, with repetition-spam protection and blacklist commands.

<p>
  <a href="#-features"><img src="https://img.shields.io/badge/✨_Features-Explore-5865F2?style=for-the-badge" alt="Features"></a>
  <a href="#-installation"><img src="https://img.shields.io/badge/🚀_Installation-Get_Started-2EA44F?style=for-the-badge" alt="Installation"></a>
  <a href="#-commands"><img src="https://img.shields.io/badge/⌨️_Commands-Reference-007EC6?style=for-the-badge" alt="Commands"></a>
</p>

<p>
  <img src="https://img.shields.io/badge/Python-3.10%2B-3776AB?style=for-the-badge&logo=python&logoColor=white" alt="Python">
  <img src="https://img.shields.io/badge/discord.py-2.x-5865F2?style=for-the-badge&logo=discord&logoColor=white" alt="discord.py">
  <img src="https://img.shields.io/badge/Webhooks-Cross--Server-2EA44F?style=for-the-badge" alt="Webhooks">
  <img src="https://img.shields.io/badge/Moderation-Anti--Spam-red?style=for-the-badge" alt="Anti-spam">
</p>

</div>

---

## 📚 Contents

- [Overview](#-overview)
- [Features](#-features)
- [Installation](#-installation)
- [Discord Setup](#-discord-setup)
- [Configuration](#-configuration)
- [Commands](#-commands)
- [How the Relay Works](#-how-the-relay-works)
- [Moderation Behaviour](#-moderation-behaviour)
- [Important Notes](#️-important-notes)
- [Troubleshooting](#-troubleshooting)

## 🌠 Overview

The **Discord Multiverse Bot** is a `discord.py` bot that relays messages between servers using text channels named `multiverse` and webhooks named `Multiverse`. It also detects repeated messages, temporarily blocks users who spam, filters links in the relay channel, and provides owner-restricted permanent blacklist commands.

The bot uses in-memory dictionaries and a set for its moderation state. This means blacklist entries and spam history are not persisted after a restart.

## ✨ Features

<table>
<tr>
<td width="50%">

### 🔗 Cross-Server Relay
- Watches messages in channels named `multiverse`.
- Relays message text to matching channels in other connected servers.
- Uses webhooks to display the sender's display name and avatar.
- Relays attached files by sending their URLs.

</td>
<td width="50%">

### 🚫 Repetition Anti-Spam
- Tracks recent messages per user.
- Detects three matching messages within a 15-second window.
- Temporarily blacklists the user for 30 minutes.
- Attempts to delete messages while the temporary blacklist is active.

</td>
</tr>
<tr>
<td width="50%">

### 🔍 Link Filtering
- Checks messages in `#multiverse` for links matching common patterns.
- Deletes matching messages when permissions allow.
- Sends a short-lived warning.

</td>
<td width="50%">

### 🛡️ Blacklist Management
- `/blacklist` adds a user ID to the in-memory permanent blacklist.
- `/unblacklist` removes a user from both blacklist collections.
- These commands are restricted to the user ID configured in the code.

</td>
</tr>
</table>

### 🧰 Channel setup

The `/setup_multiverse` command checks the caller's permissions, creates a `#multiverse` channel if one does not already exist, and creates a `Multiverse` webhook in it.

## 🚀 Installation

### 1. Create a project folder

```text
discord-multiverse/
└── bot.py
```

Save the bot code as `bot.py` (or use your own filename).

### 2. Install discord.py

On Windows, open CMD in the project directory and run:

```cmd
py -m pip install -U discord.py
```

### 3. Run the bot

```cmd
py bot.py
```

Keep the terminal open to view startup messages and errors.

## ⚙️ Discord Setup

1. Open the [Discord Developer Portal](https://discord.com/developers/applications).
2. Create or select your application and configure its bot user.
3. Enable **Message Content Intent** under **Bot → Privileged Gateway Intents**.
4. Invite the bot with the `bot` and `applications.commands` OAuth2 scopes.
5. Add the bot to every server that should participate in the relay.

The bot needs suitable permissions in each server, including viewing channels, reading message history, sending messages, managing webhooks, and deleting messages. The setup command also requires the caller to have **Manage Channels** and **Manage Webhooks**.

## 🔑 Configuration

### Bot token

Replace the hard-coded token with an environment variable:

```python
import os

token = os.getenv("DISCORD_TOKEN")
if not token:
    raise RuntimeError("Set the DISCORD_TOKEN environment variable.")
```

Windows CMD:

```cmd
set DISCORD_TOKEN=YOUR_BOT_TOKEN
py bot.py
```

PowerShell:

```powershell
$env:DISCORD_TOKEN = "YOUR_BOT_TOKEN"
py bot.py
```

Do not commit your token to GitHub. If it has already been exposed, reset it in the Developer Portal.

### Owner-only commands

The current code authorizes `/blacklist` and `/unblacklist` using a hard-coded Discord user ID:

```python
407913114818969611
```

Replace this value with the intended administrator's ID before using the bot. Only that ID is authorized by the current check.

## ⌨️ Commands

| Command | Description | Access |
|---|---|---|
| `/setup_multiverse` | Creates a `#multiverse` channel and a `Multiverse` webhook if the channel does not already exist. | Manage Channels and Manage Webhooks |
| `/blacklist user_id:<id>` | Adds the supplied user ID to the permanent in-memory blacklist. | Configured owner ID |
| `/unblacklist user_id:<id>` | Removes the user ID from the permanent and temporary blacklist collections. | Configured owner ID |

The `user_id` argument is a Discord user ID, not a username or mention. The command expects it as text and converts it to an integer.

## 🔄 How the Relay Works

```text
Message sent in #multiverse
          ↓
Ignore bot authors
          ↓
Check permanent / temporary blacklist
          ↓
Track repeated messages for spam
          ↓
Check channel name
          ↓
Filter links in #multiverse
          ↓
Find #multiverse channels in other servers
          ↓
Send message and attachments through webhooks
```

Only messages in a channel named `multiverse` are relayed. Repetition-spam tracking runs before the channel-name check, so the current code tracks repeated messages in other channels too.

## 🛡️ Moderation Behaviour

| Setting | Current value | Behaviour |
|---|---:|---|
| `TEMP_BLACKLIST_MINUTES` | `30` minutes | Temporary blacklist duration after repetition spam |
| Repetition window | `15` seconds | Recent messages kept in the user's spam cache |
| Repetition threshold | `3` matching messages | Triggers temporary blacklist |
| Link filter | `http://`, `https://`, `www.`, `discord.gg` | Patterns checked in relay-channel messages |

The spam cache, temporary blacklist, and permanent blacklist exist only in memory. Restarting the bot clears them.

## ⚠️ Important Notes

- **In-memory blacklists:** Despite the name `perma_blacklist`, entries are not saved to disk or a database. A restart clears them.
- **Link filter scope:** Link filtering only applies to messages in channels named `multiverse`.
- **Webhook availability:** The bot needs Manage Webhooks permission in relay channels. The code attempts to create a webhook named `Multiverse` if none is found.
- **Attachments:** The bot relays attachment URLs. It does not upload the original attachment bytes itself.
- **Channel naming:** The relay searches for channels by the exact lowercase name `multiverse`.
- **Bot permissions:** Message deletion and webhook operations may fail if permissions are missing. The code logs relay exceptions to the console.
- **Command processing:** Because the script overrides `on_message`, it calls `bot.process_commands(message)` for prefix commands. The moderation controls described here are primarily slash commands.
- **Link-filter limitations:** The regular expression is a simple pattern filter, not a comprehensive URL parser. Some links may not be caught, and matching text may occasionally be a false positive.

## 🧯 Troubleshooting

| Problem | Check |
|---|---|
| Slash commands do not appear | Confirm the bot has `applications.commands` scope and startup command sync succeeds. |
| Bot cannot read messages | Enable Message Content Intent in the Developer Portal and code. |
| `/setup_multiverse` fails | Check Manage Channels and Manage Webhooks permissions for the caller and bot. |
| Messages do not relay | Confirm the source and destination servers both contain a text channel named `multiverse`. |
| Attachments do not relay | Check webhook permissions and inspect the terminal for logged exceptions. |
| Blacklist resets | This implementation stores blacklist data in memory only. |
| Messages are not deleted | Confirm the bot has Manage Messages in the relevant channel. |

## 🧪 Before Deployment

- [ ] Set the bot token through an environment variable.
- [ ] Replace the hard-coded owner ID with the correct administrator ID.
- [ ] Enable Message Content Intent.
- [ ] Invite the bot to all participating servers.
- [ ] Grant the required channel and webhook permissions.
- [ ] Test relaying, attachment handling, link filtering, and spam detection in private test servers.
- [ ] Remember that blacklist data is cleared when the process restarts.

## 📄 License

No license is specified in the supplied code. If you plan to publish this repository, choose a license and add its full text in a `LICENSE` file. The [MIT License](https://choosealicense.com/licenses/mit/) is a common permissive option.

---

<div align="center">

**Built with Python and discord.py**

[⬆ Back to top](#-discord-multiverse-bot)

</div>
