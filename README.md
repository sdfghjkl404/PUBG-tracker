# PUBG Tracker

![PUBG Tracker preview](docs/images/preview-placeholder.svg)

Local web application for exploring recent PUBG matches, team statistics and
telemetry-backed movement history on an interactive tactical map.

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

Install dependencies:

```powershell
python -m pip install -r requirements.txt
```

Configure the key only in the process environment:

```powershell
$env:PUBG_API_KEY = "YOUR_PUBG_API_KEY"
python app.py
```

The application opens at `http://localhost:8000/start`.
On Windows, `start.bat` launches the project from its own directory.

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

## Roadmap

- Replace placeholders with real screenshots and a demo recording.
- Add automated tests for API parsing and telemetry rendering.
- Add optional persistent match history.
- Add Docker support for reproducible setup.

## License

Add the license you want to use for distribution. PUBG API and game assets
remain subject to their respective terms.
