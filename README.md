# Roblox Discord Moderation Bot

This bot provides professional moderation records, Roblox verification tickets,
and Roblox game-server monitoring.

## Commands

- `/whitelist add`, `/whitelist remove`, `/whitelist list`
- `/groupcheck`
- `/hb`, `/unhb`
- `/strike add`, `/strike3`, `/revoke @user <strike number>`, `/strike status`,
  `/strike history`, `/strike proof`, `/strike expire`,
  `/strike boost-forgive`
- `/revokeall`
- `/set-channel`
- `/raid-start <text>` — DM each non-bot member using plain text and mention
  that recipient
- `/raid-point add`, `/raid-point remove`, `/raid-leaderboard`, `/rreset`
- `/ticketpanel`
- `/ticket-close`
- `/verification-config`
- `/snipe add`, `/snipe remove`, `/snipe-channel`
- `/kactivity`

## Configuration

Set `DISCORD_TOKEN` and `FOUNDER_IDS`. `GUILD_ID` is optional; setting it makes
command synchronization immediate for that server. Without it, commands sync
globally and may take longer to appear.

Because the bot records message edits/deletions and ticket transcripts, enable
the **Message Content** and **Server Members** privileged intents in the
Discord Developer Portal.

For verification, configure `VERIFICATION_GROUP_IDS`,
`BLACKLIST_GROUP_IDS`, `BLACKLIST_ROLE_IDS`, `VERIFIED_ROLE_ID`,
`TICKET_CATEGORY_ID`, and `TOP5TH_ROLE_ID`. The Top 5th role and every role
above it are granted access to verification tickets and pinged when automatic
verification cannot complete; blacklist groups are shown as groups the user
must leave. Use `/snipe-channel` to choose where exact
Roblox server links are announced.

When a tracked Roblox account enters a game or joins a different server, the
bot keeps the existing alert card and mentions the member who added that
account with `/snipe add`.

Moderation events and ticket transcripts are sent to `LOG_CHANNEL_ID`, which
defaults to `1456824205545967713` to match the requested log destination. The
same events are also kept in the local SQLite database. Configure a
`QUARANTINE_ROLE_ID` to have the raid safeguard mark members when the join
threshold is reached. The safeguard logs and quarantines; it does not
automatically kick a raid wave.

`/raid-start <text>` sends a plain-text direct message to every non-bot member
and mentions the recipient. Members who have disabled server DMs may not
receive it. `/kactivity` previews first, excludes boosters and protected staff,
and requires `CONFIRM` before kicking.

The raid leaderboard is a live standard bot card. `/raid-point add` and
`/raid-point remove` edit it immediately; `/rreset` clears the points and
refreshes the same card. Set `RAID_LEADERBOARD_CHANNEL_ID` to keep it in a
dedicated channel, or run `/raid-leaderboard` in the channel where it should
first be posted.

Run it from the project root with:

```bash
python main.py
```