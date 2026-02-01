# Music Assistant PO Token Generator

One-shot utility to generate PO tokens for Music Assistant YouTube Music provider.

## Platform

Any (Linux/macOS)

## Purpose

Generates a PO token required for YouTube Music integration in Music Assistant.

## Usage

1. Deploy this stack from Portainer
2. Open container logs in Portainer
3. Follow the interactive prompts
4. Copy the generated token
5. Add token to Music Assistant → Providers → YouTube Music
6. Delete this stack (no longer needed)

## Notes

- No persistent volumes needed
- Container exits after token generation
- `restart: no` - runs once
- Safe to delete after use

## Token Validity

PO tokens typically expire after several weeks. Redeploy this stack when needed.

## Reference

- [Music Assistant Documentation](https://music-assistant.io)
- [PO Token Tool](https://github.com/jim60105/docker-bgutil-pot)
