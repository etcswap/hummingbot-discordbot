# ETCswap Community Bot for Discord

This guide explains how to use the Discord bot for ETCswap community management.

## Overview

The Hummingbot Discord Bot is a community management tool that:

- Fetches messages from specified Discord channels
- Tracks emoji reactions from designated evaluators
- Assigns points based on reaction types
- Exports contribution data to Excel

**Note:** This is a community management tool, not a trading bot. For DEX trading, see the hummingbot-condor or hummingbot-mcp projects.

## Use Cases for ETCswap

### Community Contribution Tracking

Track and reward community members for:
- Helpful trading tips and strategies
- Quality educational content
- Bug reports and feedback
- Community engagement

### Evaluation System

Moderators can evaluate contributions using emoji reactions:
- ⭐ Star: Good contribution (1 point)
- 🔥 Fire: Great contribution (2 points)
- 💡 Lightbulb: Excellent contribution (3 points)

### Weekly Reports

Export weekly contribution data for:
- Community rewards programs
- Leaderboards
- Recognition posts

## Setup for ETCswap

### Step 1: Create Discord Bots

1. Go to [Discord Developer Portal](https://discord.com/developers/applications)
2. Create two applications:
   - **Main Bot**: Responds to commands
   - **Fetch Bot**: Fetches messages (can be same bot with different token)
3. Enable required intents (Message Content)
4. Invite bots to your ETCswap Discord server

### Step 2: Configure Environment

Create `.env` file:

```bash
# Bot tokens
MAIN_DISCORD_TOKEN=your_main_bot_token
FETCH_DISCORD_TOKEN=your_fetch_bot_token

# ETCswap channel IDs (get from Discord Developer Mode)
MAIN_CHANNEL_IDS=123456789012345678,234567890123456789
FETCH_CHANNEL_IDS=123456789012345678,234567890123456789

# Moderators who can evaluate
WHITELISTED_USERS=moderator1,moderator2,moderator3

# Reaction configuration
WHITELISTED_REACTIONS=⭐,🔥,💡
REACTION_POINTS=⭐:1,🔥:2,💡:3

# Output file
EXCEL_PATH=data/etcswap_contributions.xlsx
```

### Step 3: Create Role

Create `hummingbot-admin` role in your Discord server and assign to authorized users.

### Step 4: Run Bot

```bash
conda activate discordbot
python main.py
```

## Commands

### /fetch_and_save

Fetch messages and save to Excel:

```
/fetch_and_save start_date:2024-01-01 end_date:2024-01-31
```

**Parameters:**
- `start_date`: Start date (YYYY-MM-DD)
- `end_date`: End date (YYYY-MM-DD)

**Permission:** Requires `hummingbot-admin` role

### /download_excel

Download the Excel file with collected data:

```
/download_excel
```

**Permission:** Requires `hummingbot-admin` role

## Output Format

The Excel file contains:

| Date | Week No. | Participants Discord Handle | Points | Evaluator | url |
|------|----------|---------------------------|--------|-----------|-----|
| 01-Jan-24 | 75 | trader123 | 3 | mod1, mod2 | https://... |
| 02-Jan-24 | 75 | etcfan | 2 | mod1 | https://... |

## Example Workflows

### Weekly Contribution Report

1. At end of week, run `/fetch_and_save` for the week
2. Run `/download_excel` to get the file
3. Create leaderboard from Excel data
4. Post recognition in community channel

### Monthly Rewards

1. Run `/fetch_and_save` for the entire month
2. Download and analyze Excel data
3. Calculate total points per user
4. Distribute rewards to top contributors

## Channel Ideas for ETCswap

Consider tracking these channels:

| Channel | Purpose |
|---------|---------|
| #trading-ideas | Trading strategies and tips |
| #technical-analysis | TA posts and charts |
| #defi-discussion | ETCswap and DeFi discussions |
| #bug-reports | Bug reports and feedback |
| #tutorials | Educational content |

## Reaction Suggestions

| Emoji | Points | Use For |
|-------|--------|---------|
| ⭐ | 1 | Good contribution |
| 🔥 | 2 | Great insight |
| 💡 | 3 | Exceptional idea |
| 📈 | 2 | Good trade call |
| 🎯 | 3 | Accurate prediction |

## Week Numbering

Weeks are numbered starting from Week 71 (April 16, 2024). This provides consistent tracking across time periods.

## Troubleshooting

### Bot not responding

- Check bot token is correct
- Verify bot is invited to server
- Ensure bot has proper permissions

### No messages fetched

- Verify channel IDs are correct
- Check date range is valid
- Ensure Fetch Bot has access to channels

### Permission denied

- User needs `hummingbot-admin` role
- Check role is properly configured

### Excel file not found

- Run `/fetch_and_save` first
- Check `data/` directory exists

## Integration with Other Tools

While this bot handles community management, the ETCswap ecosystem includes:

- **hummingbot-condor**: Telegram bot for DEX trading
- **hummingbot-mcp**: AI assistant integration for trading
- **hummingbot-api**: REST API for programmatic access

## Resources

- [ETCswap Website](https://etcswap.org)
- [ETCswap Discord](https://discord.gg/etcswap)
- [Ethereum Classic](https://ethereumclassic.org)
