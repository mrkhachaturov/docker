# Docker Compose Stack 

## Automated Dependency Updates with Renovate

This repository uses [Renovate](https://renovatebot.com/) to automatically monitor and update Docker image versions in all compose files.

### Configuration

- **Config file**: `.renovaterc.json5` - Contains all Renovate settings following best practices
- **Schedule**: Updates run every Monday at 6 AM Moscow time
- **Auto-merge**: Security updates and patch updates for non-critical tools are automatically merged
- **GitHub App**: Uses self-hosted Renovate with GitHub App authentication
- **Best Practices**: Uses `config:best-practices` preset with optimized Docker settings

### What Gets Updated

Renovate monitors and updates:
- Docker images in all `docker-compose*.yml` files
- Individual service files in `compose/` directory
- Dockerfile base images (if any)

### Grouping Strategy

Updates are intelligently grouped by:
- **Docker Compose files** - All main compose files together
- **Docker services** - Individual service files together
- **Traefik ecosystem** - All Traefik-related updates
- **Portainer** - Portainer updates
- **MinIO** - MinIO and MinIO Console updates
- **LinuxServer.io images** - All LinuxServer.io containers
- **1Password Connect** - 1Password API and Sync services
- **Database engines** - MySQL, PostgreSQL, MariaDB, Valkey
- **Backup & Sync tools** - rclone, Syncthing
- **Monitoring tools** - Matomo, Uptime Kuma, Grafana, etc.
- **Development tools** - n8n, Obsidian, VSCode, GitLab
- **Security tools** - Authelia, CrowdSec, OAuth

### Versioning Strategy

- **SemVer**: Used for standard versioned images (Python, Node.js)
- **PEP440**: Used for Python images
- **Node**: Used for Node.js images  
- **Loose**: Used for non-standard tagged images (MinIO)
- **Pin**: Used for critical infrastructure (Traefik)
- **Latest**: Used for development tools

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

### Best Practices Implemented

This configuration follows Renovate best practices:

- **`config:best-practices`** - Uses the latest recommended preset
- **Digest pinning** - All Docker images are pinned to specific digests for security
- **Smart grouping** - Related updates are grouped to reduce PR noise
- **Version-specific strategies** - Different versioning schemes for different image types
- **Auto-merge for safe updates** - Patch updates for non-critical tools are auto-merged
- **Constraint filtering** - Strict filtering based on Docker version constraints
- **Binary source optimization** - Uses `install` mode for better performance

