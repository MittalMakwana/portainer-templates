# Home Assistant (macOS)

Home Assistant optimized for macOS/M1 with port mappings.

## Platform

macOS / Docker Desktop (M1/Intel)

## Limitations

⚠️ **mDNS/device discovery does not work on macOS Docker Desktop**
- Use manual IP addresses for devices
- Use cloud-based integrations (Nest, Hue, etc.)
- For full discovery support, deploy on Linux

## Prerequisites

```bash
# Create required directories
mkdir -p /Users/mittalmak/docker/homeassistant/config

# Ensure Docker Desktop has file sharing enabled
# Docker Desktop → Settings → Resources → File Sharing → Add path
```

## Configuration

Copy `.env.example` to `.env` and adjust:

```bash
TZ=America/Los_Angeles
BASE_PATH=/Users/mittalmak/docker
HA_PORT=8123
```

## Access

After deployment: `http://localhost:8123`

## Notes

- Uses bridge networking (host networking doesn't work on macOS)
- Healthcheck included for monitoring
- Config persisted to `${BASE_PATH}/homeassistant/config`
