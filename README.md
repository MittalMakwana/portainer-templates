# Portainer Templates – Home Automation

Custom Portainer templates for Home Assistant and Music Assistant, optimized for both M1 Mac and Linux.

## Templates Included

### macOS/M1 Optimized (Recommended for Mac users)
- **Home Assistant (macOS)** - Port-mapped, Portainer-managed
- **Music Assistant (macOS)** - Port-mapped, Portainer-managed
- **PO Token Generator** - One-shot utility (platform-agnostic)

### Linux (Full Discovery Support)
- **Home Assistant (Linux)** - Host networking, full mDNS/discovery
- **Music Assistant (Linux)** - Host networking, full device discovery

## Setup Instructions

### 1. Docker Desktop Configuration (M1 Mac)

Before deploying, ensure Docker Desktop has proper permissions:

```bash
# Open Docker Desktop → Settings → Resources → File Sharing
# Add: /Users/mittalmak/docker (or your chosen base path)
```

Recommended settings:
- **Memory**: 4GB minimum (8GB recommended)
- **VirtioFS**: Enabled (default)

### 2. Add Templates to Portainer

1. Open Portainer web UI
2. Navigate to **Settings** → **App Templates**
3. Add this single URL:

```
https://raw.githubusercontent.com/<your-username>/portainer-templates/main/templates.json
```

This loads all 5 templates at once! 🎉

### 3. Create Base Directory

```bash
mkdir -p /Users/mittalmak/docker/{homeassistant/config,music-assistant/data}
```

### 4. Deploy Stacks

1. Go to **App Templates** in Portainer
2. Select your desired template:
   - For M1 Mac: Use templates ending with "(macOS)"
   - For Linux: Use templates ending with "(Linux)"
3. Fill in environment variables (or accept defaults)
4. Click **Deploy the stack**

### 5. Access Services

- **Home Assistant**: `http://localhost:8123`
- **Music Assistant**: `http://localhost:8095`

## Defaults

| Setting | Value |
|---------|-------|
| Timezone | `America/Los_Angeles` |
| Base Path | `/Users/mittalmak/docker` |
| HA Port | `8123` |
| MA Port | `8095` |

> ⚠️ Portainer requires absolute paths - `~` is not supported

## M1 Mac Considerations

✅ **What works:**
- All basic functionality
- Web UI access
- Portainer stack management
- Native ARM64 images

⚠️ **Limitations:**
- No mDNS/device discovery (Docker Desktop limitation)
- Use cloud integrations or manual IP addresses
- USB devices not recommended

Use the `-macos` templates for best compatibility on M1 Macs.

## Managing Stacks

All stack management is done through the Portainer UI:

- **Deploy**: App Templates → Select template → Deploy the stack
- **View/Edit**: Stacks → [Stack Name] → Editor → Update the stack
- **Logs**: Stacks → [Stack Name] → Logs
- **Stop/Start/Restart**: Use the stack action buttons
- **Delete**: Stacks → [Stack Name] → Delete this stack

No CLI commands needed! Everything is managed through Portainer. ✨

## Troubleshooting

### Stack won't deploy
- Verify Docker Desktop is running
- Check file sharing permissions in Docker Desktop settings
- Ensure base directory exists: `ls -la /Users/mittalmak/docker/`

### Can't access web UI
- Verify container is running in Portainer
- Check port isn't in use: `lsof -i :8123`
- Use `localhost` (not `127.0.0.1`)

### Device discovery doesn't work (macOS)
- Expected behavior - Docker Desktop on macOS doesn't support mDNS
- Use manual IP addresses or cloud-based integrations
- For full discovery, use Linux templates on a Linux host

## Adding More Templates

Edit `templates.json` and append to the `"templates"` array:

```json
{
  "version": "2",
  "templates": [
    {...existing templates...},
    {
      "type": "stack",
      "title": "Your New Service",
      "description": "Service description",
      "categories": ["Category"],
      "platform": "linux",
      "logo": "https://...",
      "env": [...],
      "stackfile": {...}
    }
  ]
}
```

After pushing changes, Portainer will automatically reload the updated templates.

## Repository Structure

```
portainer-templates/
├── LICENSE
├── README.md
└── templates.json        # All 5 templates in one file
```

## Architecture Support

All images support ARM64 (M1 native):
- ✅ Home Assistant - multi-arch
- ✅ Music Assistant - multi-arch
- ✅ PO Token Generator - multi-arch

## License

MIT
