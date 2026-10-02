# Lotus Hourly Backup

Automated backups for the **Lotus** Minecraft Bedrock Dedicated Server running on AWS EC2.

## Important guarantees
- **Never stops or restarts the server** — backups are online only (file copy / tar while BDS is running).
- Runs as a self-sustaining loop (6 hourly backups, then re-triggers itself).
- Stores backups in this repository under `backups/`.

## Required GitHub Secrets
| Secret | Description |
|--------|-------------|
| `SSH_PRIVATE_KEY` | Private key for the EC2 key pair (`Lotus-Minecraft`) |
| `SERVER_HOST` | Public IP or hostname (e.g. `13.126.209.44`) |
| `SERVER_USER` | SSH user (usually `ubuntu`) |
| `MC_PATH` | Path to BDS folder on the server (e.g. `/home/ubuntu/minecraft`) |
| `GH_PAT` | (Optional) Personal access token with `repo` + `workflow` if default `GITHUB_TOKEN` cannot re-trigger |

## Manual run
Actions → Hourly Backup Loop → Run workflow

## Safety
The workflow only uses `scp` / `rsync` / `tar` over SSH.  
It never runs `systemctl stop`, `shutdown`, `reboot`, or any command that would interrupt the live server.
