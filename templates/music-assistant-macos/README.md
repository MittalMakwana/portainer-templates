# Music Assistant (macOS)

Music Assistant server optimized for macOS/M1 with port mappings.

## Platform

macOS / Docker Desktop (M1/Intel)

## Limitations

⚠️ **Local device discovery limited on macOS**
- AirPlay/Chromecast discovery may not work
- Use cloud-based music providers (Spotify, YouTube Music, Tidal)
- Use manual IP addresses for local players
- For full discovery, deploy on Linux

## Prerequisites

```bash
# Create required directories
mkdir -p /Users/mittalmak/docker/music-assistant/data
```

## Configuration

Copy `.env.example` to `.env` and adjust:

```bash
TZ=America/Los_Angeles
BASE_PATH=/Users/mittalmak/docker
MA_PORT=8095
```

## Access

After deployment: `http://localhost:8095`

## Recommended Providers

Since local discovery is limited on macOS, use these providers:
- Spotify
- YouTube Music
- Tidal
- Qobuz
- Deezer

## Notes

- Uses bridge networking
- Healthcheck included
- Data persisted to `${BASE_PATH}/music-assistant/data`
