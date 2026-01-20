# Hummingbot Discord Bot Development Instructions

Instructions for AI coding assistants working on Hummingbot Discord Bot.

## Project Vision

Hummingbot Discord Bot is a **community management tool** for Discord that fetches and evaluates messages from specified channels, tracking contributions via emoji reactions and exporting data to Excel.

**Current Focus:** Supporting ETCswap community management on Discord.

**Note:** This bot is for community management, not trading. For trading bots, see hummingbot-condor (Telegram) or hummingbot-mcp (AI assistants).

## Tech Stack

**Framework & Runtime:**
- Python: 3.10+
- discord.py: Discord bot framework
- pandas: Data manipulation
- openpyxl: Excel file handling

**Environment:**
- python-dotenv: Environment variable management
- Conda: Package management

## Quick Start

```bash
# Clone and setup
git clone https://github.com/etcswap/hummingbot-discordbot.git
cd hummingbot-discordbot
git checkout etcswap

# Create environment
conda env create -f environment.yml
conda activate discordbot

# Configure
cp .env.example .env
# Edit .env with your Discord tokens and settings

# Run
python main.py
```

> **Note:** This uses the ETCswap fork. Once merged upstream, use `https://github.com/hummingbot/discordbot.git`.

## Core Architecture

### Project Structure

```
hummingbot-discordbot/
├── main.py              # Main bot application
├── environment.yml      # Conda environment
├── .env                 # Configuration (create from example)
├── data/                # Output directory
│   └── discord_messages.xlsx
└── LICENSE
```

### Key Features

1. **Message Fetching** - Fetch messages from specified channels within a date range
2. **Reaction Tracking** - Track emoji reactions from whitelisted evaluators
3. **Points System** - Assign points based on reaction types
4. **Excel Export** - Save collected data to Excel files
5. **Week Numbering** - Track contributions by week (starting Week 71 from 2024-04-16)

### Commands

| Command | Description | Permission |
|---------|-------------|------------|
| `/fetch_and_save` | Fetch messages and save to Excel | hummingbot-admin role |
| `/download_excel` | Download the Excel file | hummingbot-admin role |

## Configuration

### Environment Variables (.env)

```bash
# Main bot credentials
MAIN_DISCORD_TOKEN=your_main_bot_token
MAIN_CHANNEL_IDS=123456789,987654321

# Fetch bot credentials (separate bot for fetching)
FETCH_DISCORD_TOKEN=your_fetch_bot_token
FETCH_CHANNEL_IDS=123456789,987654321

# Evaluation configuration
WHITELISTED_USERS=user1,user2,user3
WHITELISTED_REACTIONS=1️⃣,2️⃣,3️⃣
REACTION_POINTS=1️⃣:1,2️⃣:2,3️⃣:3

# Output
EXCEL_PATH=data/discord_messages.xlsx
```

### Week Numbering

Week numbers start at 71 from April 16, 2024:
- Week 71: April 16-22, 2024
- Week 72: April 23-29, 2024
- etc.

## ETCswap Community Context

This bot can be configured for ETCswap community channels to:

- Track community contributions
- Evaluate trading ideas and strategies
- Monitor engagement in ETCswap discussions
- Export contribution data for rewards/recognition

### Example ETCswap Configuration

```bash
# .env for ETCswap community
MAIN_CHANNEL_IDS=etcswap_general_id,etcswap_trading_id
FETCH_CHANNEL_IDS=etcswap_general_id,etcswap_trading_id
WHITELISTED_USERS=moderator1,moderator2
WHITELISTED_REACTIONS=⭐,🔥,💡
REACTION_POINTS=⭐:1,🔥:2,💡:3
```

## Data Output Format

The Excel file contains:

| Column | Description |
|--------|-------------|
| Date | Message date (DD-Mon-YY) |
| Week No. | Week number (starting from 71) |
| Participants Discord Handle | Author username |
| Points | Total points from reactions |
| Evaluator | Comma-separated evaluator names |
| url | Direct link to message |

## Protected Files

Do not modify without explicit request:
- `main.py` - Core application logic

## Coding Style

- Python 3.10+ compatible
- Async/await for Discord operations
- Clear function documentation
- Environment-based configuration

## Validation Requirements

**Before Any Commit:**
```bash
# Test bot locally
python main.py

# Verify commands work
# Use /fetch_and_save and /download_excel in Discord
```

## Commit Format

```
<scope>: <description>

Co-Authored-By: Claude <noreply@anthropic.com>
```

**Scopes:**
- `feat:` - New features
- `fix:` - Bug fixes
- `config:` - Configuration changes
- `docs:` - Documentation

**Examples:**
```
feat: add ETCswap channel support
config: update reaction points for trading ideas
docs: add community management guide
```

## Common Tasks

### Adding New Reaction Types

1. Update `WHITELISTED_REACTIONS` in `.env`
2. Update `REACTION_POINTS` with point values
3. Restart bot

### Adding New Channels

1. Get channel IDs from Discord (Developer Mode)
2. Add to `MAIN_CHANNEL_IDS` and/or `FETCH_CHANNEL_IDS`
3. Restart bot

### Modifying Week Start

Change `WEEK_71_START_DATE` in `main.py` if needed.

## Ecosystem Context

This is part of the ETCswap/Hummingbot ecosystem:

- **hummingbot-discordbot** (THIS PROJECT): Discord community management
- **hummingbot-condor**: Telegram trading bot
- **hummingbot-api**: REST API backend
- **hummingbot-mcp**: MCP server for AI assistants

**Note:** This bot focuses on community management. For trading functionality, use the other ecosystem components.

**Branch:** This ETCswap integration is on the `etcswap` branch until merged upstream.

---

Last updated: 2025-01-20
