# Music Assistant (Linux)

Music Assistant server with full host networking and device discovery.

## Platform

Linux (Ubuntu, Debian, Fedora, etc.)

## Features

✅ Full mDNS/Bonjour discovery
✅ AirPlay device detection
✅ Chromecast support
✅ DLNA/UPnP support
✅ Host networking mode

## Prerequisites

```bash
# Create required directories
mkdir -p /opt/docker/music-assistant/data
```

## Configuration

Copy `.env.example` to `.env` and adjust:

```bash
TZ=America/Los_Angeles
BASE_PATH=/opt/docker
```

## Access

After deployment: `http://<server-ip>:8095`

## Supported Players

- AirPlay devices (Apple HomePod, AirPort Express)
- Chromecast devices
- DLNA/UPnP players
- Home Assistant media players
- Snapcast
- Slimproto (Logitech Media Server compatible)

## Notes

- Uses host networking for full discovery
- Healthcheck included
- Data persisted to `${BASE_PATH}/music-assistant/data`
- Syncs with host timezone
