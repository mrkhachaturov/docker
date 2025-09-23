# Docker Compose Stack 

## Automated Dependency Updates with Renovate

This repository uses [Renovate](https://renovatebot.com/) to automatically monitor and update Docker image versions in all compose files.

### Configuration

- **Config file**: `.renovaterc.json5` - Contains all Renovate settings
- **Schedule**: Updates run every Monday at 6 AM Moscow time
- **Auto-merge**: Security updates are automatically merged, other updates require manual review
- **GitHub App**: Uses self-hosted Renovate with GitHub App authentication

### What Gets Updated

Renovate monitors and updates:
- Docker images in all `docker-compose*.yml` files
- Individual service files in `compose/` directory
- Dockerfile base images (if any)

### Grouping Strategy

Updates are intelligently grouped by:
- **Docker Compose files** - All main compose files together
- **Docker services** - Individual service files together
- **Traefik** - All Traefik-related updates
- **Portainer** - Portainer updates
- **MinIO** - MinIO and MinIO Console updates
- **Monitoring tools** - Matomo, Uptime Kuma, Grafana, etc.
- **Database tools** - phpMyAdmin, pgAdmin, MySQL, etc.
- **Development tools** - n8n, Obsidian, VSCode, GitLab
- **Security tools** - Authelia, CrowdSec, OAuth

### Ignored Files

The following are excluded from updates:
- `secrets/` directory
- `secrets_example/` directory
- `*.example` files
- `appdata/` directory
- `shared/` directory
- `scripts/` directory

### Manual Override

To disable updates for specific images, add them to the `ignoreDeps` array in `.renovaterc.json5`:

```json5
{
  "ignoreDeps": [
    "socket-proxy",
    "custom-image:latest"
  ]
}
```

### Security Updates

Security vulnerabilities are automatically detected and updates are:
- Labeled with `security` and `vulnerability` labels
- Automatically merged (if configured)
- Prioritized over regular updates

