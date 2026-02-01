# Music Assistant (macOS) + BgUtil PO Token Provider

Music Assistant server with integrated BgUtil PO Token provider, optimized for macOS/M1 with host networking.

## Platform

macOS / Docker Desktop (M1/Intel)

## Services Included

1. **Music Assistant** - Music server (default port 8095)
2. **BgUtil PO Token Provider** - HTTP server (default port 4416) for YouTube Music support

## Network Mode

Uses **host networking** for maximum compatibility. On macOS, this provides best-effort device discovery.

⚠️ **Note**: Docker Desktop on macOS has limited host networking support compared to Linux.

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
```

## Access

After deployment:
- **Music Assistant**: `http://localhost:8095`
- **BgUtil PO Token Provider**: `http://localhost:4416` (used internally by Music Assistant)

## Configuring YouTube Music

1. Open Music Assistant at `http://localhost:8095`
2. Go to Settings → Providers → YouTube Music
3. Set **PO Token Provider**:
   - Type: `bgutil:http`
   - Base URL: `http://localhost:4416`
4. Save configuration

With host networking, both services use localhost for communication.

## Recommended Providers

- YouTube Music (with BgUtil provider configured)
- Spotify
- Tidal
- Qobuz
- Deezer
- Apple Music

## Notes

- Uses host networking mode
- No port configuration needed (uses default ports)
- BgUtil provider generates PO tokens on-demand
- Data persisted to `${BASE_PATH}/music-assistant/data`
- Both services run continuously
