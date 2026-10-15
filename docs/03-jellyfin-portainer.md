# Project 3: Media Server and Container Management

**Goal:** Stream my own media with Jellyfin and manage all containers from a web UI with Portainer.

## Jellyfin

1. Put media in the folder set as `MEDIA_PATH` in `.env` (mounted read-only into the container).
2. Set `PUID`/`PGID` to my user (`id -u`, `id -g`) so Jellyfin can read the files without running as root.
3. `docker compose up -d jellyfin`, then finish the setup wizard at `http://<server-ip>:8096`.
4. Add libraries pointing at `/media/...` inside the container.

**Note:** this is an old laptop with no hardware video encoder, so clients should **direct play** instead of transcoding. Setting each client's quality to "Maximum" avoids CPU-heavy transcodes.

## Portainer

1. `docker compose up -d portainer`.
2. Open `https://<server-ip>:9443` within a few minutes and create the admin user (Portainer locks the setup page after a timeout; restart the container if that happens).
3. The local Docker environment is picked up through the mounted Docker socket.

**Key Learnings:**
* Bind mounts vs. named volumes, and running containers as a non-root user.
* Mounting the Docker socket gives a container full control of the host, so Portainer is only reachable on the LAN and over Tailscale.
