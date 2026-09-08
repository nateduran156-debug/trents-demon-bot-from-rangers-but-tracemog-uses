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
- `/raid-start`
- `/raid-point add`, `/raid-point remove`, `/raid-leaderboard`, `/rreset`
- `/ticketpanel`
- `/ticket-close`
- `/verification-config`
- `/snipe add`, `/snipe remove`, `/snipe-channel`
- `/tag <tag> <username>` — assign the matching Roblox group role; choose from `Member`, `sharingan tag`, `rockstar`,
  `dark`, `FaZe`, `fraid`, `tracemog`, `flax`, `x`, `SUKAA`, `Admin`, or `Owner`
- `/tag-manager add`, `/tag-manager remove`
- `/tag-manager grant`, `/tag-manager revoke`
- `/strip`, `/tagwipe`
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

Moderation events and ticket transcripts are sent to `LOG_CHANNEL_ID`, which
defaults to `1456824205545967713` to match the requested log destination. The
same events are also kept in the local SQLite database. Configure a
`QUARANTINE_ROLE_ID` to have the raid safeguard mark members when the join
threshold is reached. The safeguard logs and quarantines; it does not
automatically kick a raid wave.

The `/tag` command replaces the old `/tagp` command and exposes the community
roles above as the tag picker. Only founders and members with the
`TAG_MANAGER_ROLE_NAME` role can use `/tag`; only founders can grant or revoke
that manager role. Each target must already have a linked Roblox account from
the verification flow. The bot uses the `ROBLOX_COOKIE` secret to assign the
matching Roblox group role, then loads the Roblox community name, description,
and icon from `ROBLOX_GROUP_ID` into the original dark-red card. The Roblox
account behind the cookie must own the group or have permission to manage
members, and the Roblox role names must exactly match the tag choices.
`/strip` and `/tagwipe` only remove those managed tag roles, protect
staff/founders, and require `CONFIRM` after a preview. `/kactivity` also
previews first, excludes boosters and protected staff, and requires `CONFIRM`
before kicking.

The bot does not accept Roblox cookies through Discord. A raw `.ROBLOSECURITY`
cookie is a live account credential and must never be pasted into a command or
log channel. Public Roblox avatar and group-logo endpoints already work without
one; if a future authenticated Roblox integration is needed, keep its secret
in the deployment environment rather than in Discord or SQLite.

The raid leaderboard is a live standard bot card. `/raid-point add` and
`/raid-point remove` edit it immediately; `/rreset` clears the points and
refreshes the same card. Set `RAID_LEADERBOARD_CHANNEL_ID` to keep it in a
dedicated channel, or run `/raid-leaderboard` in the channel where it should
first be posted.

Run it from the project root with:

```bash
python main.py
```