# BgUtil PO Token Provider

HTTP server that provides proof-of-origin tokens for yt-dlp and Music Assistant YouTube Music integration.

## Platform

Any (Linux/macOS)

## Purpose

Runs a continuously available HTTP server that generates PO tokens on-demand. This bypasses YouTube's "Sign in to confirm you're not a bot" errors.

## Prerequisites

Music Assistant must be able to reach this service on port 4416 (or your custom port).

## Configuration

Copy `.env.example` to `.env` and adjust:

```bash
PROVIDER_PORT=4416
```

## Usage

### 1. Deploy this stack from Portainer

The server will start and listen on port 4416.

### 2. Configure Music Assistant

In Music Assistant → Providers → YouTube Music:

- **PO Token Provider**: Set to `bgutil:http`
- **Base URL**: `http://bgutil-pot-provider:4416` (if on same Docker network)
  - Or: `http://<server-ip>:4416` (if different host)

### 3. Verify

Check container logs in Portainer to see:
```
Server listening on port 4416
```

## Network Considerations

**Same Portainer/Docker host:**
- Music Assistant can connect to `http://bgutil-pot-provider:4416`
- Ensure both containers are on the same Docker network

**Different hosts:**
- Use `http://<provider-host-ip>:4416`
- Ensure firewall allows port 4416

**Using local proxy:**
- Pass `--net=host` if provider needs to access local proxy server

## Access

The provider HTTP server will be available at:
- `http://localhost:4416` (from host)
- `http://bgutil-pot-provider:4416` (from other containers on same network)

## Token Validity

Tokens are generated on-demand and cached internally. This service should run continuously.

## Troubleshooting

**Music Assistant can't connect:**
- Verify container is running: Check Portainer
- Check network connectivity: `docker exec music-assistant curl http://bgutil-pot-provider:4416/health`
- Ensure same Docker network or use host IP

**Logs show errors:**
- Check Music Assistant version supports `bgutil:http` provider
- Verify yt-dlp version >= 2025.05.22 (used by Music Assistant)

## Reference

- [GitHub Repository](https://github.com/Brainicism/bgutil-ytdlp-pot-provider)
- [yt-dlp PO Token Guide](https://github.com/yt-dlp/yt-dlp/wiki/PO-Token-Guide)
- [Music Assistant Documentation](https://music-assistant.io)
