# Portainer Templates – Home Automation

Production-ready Portainer v2 templates for self-hosted home automation and media services.

## Quick Start

### 1. Add Templates to Portainer

1. Open Portainer → **Settings** → **App Templates**
2. Add this URL:

```
https://raw.githubusercontent.com/MittalMakwana/portainer-templates/main/templates.json
```

3. Save

### 2. Deploy a Stack

1. **App Templates** → Choose your template
2. Edit environment variables if needed
3. Click **Deploy the stack**

Done. No compose files. No CLI. No guessing.

## Available Templates

### For macOS (M1/Intel)

- **Home Assistant (macOS)** – Port-mapped, bridge networking
- **Music Assistant (macOS)** – Port-mapped, bridge networking
- **PO Token Generator** – One-shot utility

⚠️ **macOS Limitations**: mDNS/device discovery doesn't work. Use cloud integrations or manual IPs.

### For Linux

- **Home Assistant (Linux)** – Host networking, full discovery
- **Music Assistant (Linux)** – Host networking, full discovery

✅ **Linux Benefits**: Full mDNS, device discovery, USB support.

## Configuration

All templates use environment variables. Defaults are pre-configured but customizable in Portainer UI.

| Variable | Default (macOS) | Default (Linux) | Purpose |
|----------|-----------------|-----------------|---------|
| `BASE_PATH` | `/Users/mittalmak/docker` | `/opt/docker` | Volume mount base |
| `TZ` | `America/Los_Angeles` | `America/Los_Angeles` | Container timezone |
| `HA_PORT` | `8123` | N/A (host mode) | Home Assistant port |
| `MA_PORT` | `8095` | N/A (host mode) | Music Assistant port |

> ⚠️ Use **absolute paths** only. `~` doesn't work in Portainer.

## Prerequisites

### macOS

```bash
# Create base directory
mkdir -p /Users/mittalmak/docker/{homeassistant/config,music-assistant/data}

# Docker Desktop → Settings → Resources → File Sharing
# Add: /Users/mittalmak/docker
```

### Linux

```bash
# Create base directory
mkdir -p /opt/docker/{homeassistant/config,music-assistant/data}

# For USB devices (Zigbee/Z-Wave)
sudo usermod -aG dialout $USER
```

## Stack Management

All operations through Portainer UI:

- **Deploy**: App Templates → Select → Deploy
- **Edit**: Stacks → [Stack] → Editor → Update the stack
- **Logs**: Stacks → [Stack] → Logs
- **Restart**: Stack action buttons
- **Delete**: Stacks → [Stack] → Delete

No CLI needed.

## Troubleshooting

**Stack won't deploy**
- Check Docker is running
- Verify file sharing permissions (macOS: Docker Desktop settings)
- Ensure base directory exists

**Can't access web UI**
- Verify container is running (Portainer → Containers)
- Check port conflicts: `lsof -i :8123`
- Use `localhost` not `127.0.0.1` (macOS)

**Device discovery doesn't work (macOS)**
- Expected behavior – use cloud integrations or manual IPs
- For full discovery, use Linux templates on a Linux host

## Repository Structure

```
portainer-templates/
├── templates.json                            # Portainer consumes this
├── README.md
└── templates/
    ├── homeassistant-macos/
    │   ├── docker-compose.yml
    │   ├── .env.example
    │   └── README.md
    ├── homeassistant-linux/
    │   ├── docker-compose.yml
    │   ├── .env.example
    │   └── README.md
    ├── music-assistant-macos/
    │   ├── docker-compose.yml
    │   ├── .env.example
    │   └── README.md
    ├── music-assistant-linux/
    │   ├── docker-compose.yml
    │   ├── .env.example
    │   └── README.md
    └── po-token/
        ├── docker-compose.yml
        ├── .env.example
        └── README.md
```

Each service is self-contained. Compose files are version-controlled separately.

## Adding New Templates

1. Create new directory: `templates/your-service/`
2. Add `docker-compose.yml`, `.env.example`, `README.md`
3. Update `templates.json`:

```json
{
  "type": "stack",
  "title": "Your Service",
  "description": "Service description",
  "categories": ["Category"],
  "platform": "linux",
  "logo": "https://...",
  "repository": {
    "url": "https://github.com/MittalMakwana/portainer-templates",
    "stackfile": "templates/your-service/docker-compose.yml"
  },
  "env": [
    {
      "name": "BASE_PATH",
      "label": "Base Docker path",
      "default": "/opt/docker"
    }
  ]
}
```

4. Push to GitHub → Portainer auto-reloads

## Best Practices

**Do:**
- ✅ One service per template
- ✅ Use environment variables for all paths
- ✅ Include healthchecks
- ✅ Use specific image tags (not `latest` in production)
- ✅ Document platform-specific limitations

**Don't:**
- ❌ Hardcode paths or IPs
- ❌ Use `~` in paths
- ❌ Mix unrelated services in one stack
- ❌ Commit secrets to git

## Architecture Support

All images are multi-arch (ARM64 + x86_64):

- ✅ Home Assistant
- ✅ Music Assistant
- ✅ PO Token Generator

M1 Macs pull ARM64 natively. No Rosetta needed.

## License

MIT
