# Hummingbot Discord Bot

A Discord bot for community management that fetches messages, tracks emoji reactions from evaluators, and exports contribution data to Excel.

## ETCswap Support

This branch is configured for [ETCswap](https://etcswap.org) community management on Ethereum Classic.

See [docs/etcswap/](docs/etcswap/) for community setup guide.

## Features

- **Message Fetching**: Fetch messages from specified channels within a date range
- **Reaction Tracking**: Track emoji reactions from whitelisted evaluators
- **Points System**: Assign points based on reaction types
- **Excel Export**: Save collected data to Excel files
- **Week Numbering**: Track contributions by week

## Quick Start

```bash
git clone https://github.com/etcswap/hummingbot-discordbot.git
cd hummingbot-discordbot
git checkout etcswap

# Create conda environment
conda env create -f environment.yml
conda activate discordbot

# Configure
# Create .env with Discord tokens and settings

# Run
python main.py
```

> **Note:** This uses the ETCswap fork. Once merged upstream, use `https://github.com/hummingbot/discordbot.git`.

## Commands

| Command | Description | Permission |
|---------|-------------|------------|
| `/fetch_and_save` | Fetch messages and save to Excel | hummingbot-admin |
| `/download_excel` | Download the Excel file | hummingbot-admin |

## Configuration

Create a `.env` file:

```bash
# Bot tokens
MAIN_DISCORD_TOKEN=your_main_bot_token
FETCH_DISCORD_TOKEN=your_fetch_bot_token

# Channel IDs
MAIN_CHANNEL_IDS=123456789,987654321
FETCH_CHANNEL_IDS=123456789,987654321

# Evaluators and reactions
WHITELISTED_USERS=user1,user2,user3
WHITELISTED_REACTIONS=1️⃣,2️⃣,3️⃣
REACTION_POINTS=1️⃣:1,2️⃣:2,3️⃣:3

# Output
EXCEL_PATH=data/discord_messages.xlsx
```

## Data Output

The Excel file contains:

| Column | Description |
|--------|-------------|
| Date | Message date |
| Week No. | Week number (from 71) |
| Participants Discord Handle | Author |
| Points | Total points |
| Evaluator | Evaluator names |
| url | Message link |

## Requirements

- Python 3.10+
- discord.py
- pandas
- openpyxl

## License

Apache 2.0
