# PUBG Tracker

![PUBG Tracker preview](docs/images/preview-placeholder.svg)

Local web application for exploring recent PUBG matches, team statistics and
telemetry-backed movement history on an interactive tactical map.

Built with Python, the official PUBG API and a focused browser UI. Keep the
API key on your machine, inspect a player's recent matches, then drill into
squad performance and in-game movement.

## Features

- Search a player by nickname and platform.
- Load the latest 1–20 matches.
- Review placement, kills, team damage and distance.
- Render movement, kills, knockdowns, zones and telemetry events.
- Pan, zoom and inspect event details on the tactical map.
- Cache map assets locally after the first request.
- Keep the PUBG API key outside source control.

## Screenshots

Safe placeholders are included until real screenshots are available:

| View | Preview |
|---|---|
| Start screen | ![Start screen](docs/images/start-placeholder.svg) |
| Tactical map | ![Tactical map](docs/images/map-placeholder.svg) |
| Match details | ![Match details](docs/images/details-placeholder.svg) |

## Requirements

- Python 3.10+
- A PUBG Developer API key
- Internet access for API, telemetry and first-time map downloads

## Get a PUBG API key

1. Open the [official PUBG Developer Portal](https://developer.pubg.com/).
2. Sign in with your PUBG developer account.
3. Create an application and copy its API key.
4. Keep the key private and configure it through the environment variable
   shown below.

The API has rate limits. Use the application responsibly and follow the
current PUBG API terms and documentation.

## Installation and configuration

Install dependencies:

```powershell
python -m pip install -r requirements.txt
```

Configure the key only in the process environment:

```powershell
$env:PUBG_API_KEY = "YOUR_PUBG_API_KEY"
python app.py
```

Open [`http://localhost:8000/start`](http://localhost:8000/start) in your
browser. On Windows, `start.bat` launches the application from its own
directory.

## Usage

1. Enter a PUBG nickname.
2. Select Steam, Kakao, PlayStation, Xbox or Stadia.
3. Choose the number of recent matches.
4. Select a match in the history panel.
5. Select a squad member to inspect movement and events.

## Project structure

```text
PUBG-tracker/
├── app.py                 # Local API proxy and telemetry loader
├── index.html             # Tactical map interface
├── start.html             # Search screen
├── start.bat              # Windows launcher
├── requirements.txt       # Python dependencies
├── docs/images/            # Screenshot placeholders
├── maps/                  # Runtime cache, ignored by Git
└── vers/                  # Local development archives, ignored by Git
```

## Architecture

```text
Browser → Local Python proxy :8000
                       ├── PUBG API: player and match metadata
                       ├── PUBG telemetry: movement and events
                       └── PUBG map assets: local cache in maps/
```

The browser never receives the API key. The local Python process makes
authenticated requests to the PUBG API.

## Security

- `PUBG_API_KEY` is read from the environment only.
- Do not commit `.env` files, API keys, tokens or personal data.
- Large downloaded maps and old ZIP archives are intentionally ignored.
- Revoke and replace a key immediately if it was ever exposed.

## Known limitations

- Data depends on PUBG API availability and rate limits.
- Map assets can be large and are downloaded on first use.
- The current server is intended for local use, not public hosting.

## License

This project is distributed under the [MIT License](LICENSE).

PUBG, PUBG API and related game assets remain subject to their respective
trademarks, copyrights and terms of use.
