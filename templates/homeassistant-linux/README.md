# Home Assistant (Linux)

Home Assistant with full host networking and device discovery support.

## Platform

Linux (Ubuntu, Debian, Fedora, etc.)

## Features

✅ Full mDNS/Bonjour discovery
✅ Host networking mode
✅ USB device support (with proper permissions)
✅ Privileged access for hardware integration

## Prerequisites

```bash
# Create required directories
mkdir -p /opt/docker/homeassistant/config

# For USB devices (Zigbee/Z-Wave)
# Add user to dialout group
sudo usermod -aG dialout $USER
```

## Configuration

Copy `.env.example` to `.env` and adjust:

```bash
TZ=America/Los_Angeles
BASE_PATH=/opt/docker
```

## Access

After deployment: `http://<server-ip>:8123`

## Notes

- Uses host networking for full discovery
- Privileged mode enabled for hardware access
- Config persisted to `${BASE_PATH}/homeassistant/config`
- Syncs with host timezone via `/etc/localtime`
