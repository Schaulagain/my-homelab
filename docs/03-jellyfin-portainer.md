# Jellyfin and Portainer

## Jellyfin

1. Set `MEDIA_PATH` in `.env` to the folder with your media. It's mounted read-only.
2. Set `PUID` and `PGID` to your own user (`id -u`, `id -g`). That way Jellyfin can read the files without running as root.
3. `docker compose up -d jellyfin` and go through the setup at `http://<server-ip>:8096`.
4. Add libraries that point at `/media/...` inside the container.

The laptop is old and has no hardware video encoder, so transcoding is slow. Setting the quality on each client to "Maximum" makes them play the file directly instead.

## Portainer

1. `docker compose up -d portainer`
2. Go to `https://<server-ip>:9443` straight away and create the admin user. If you wait too long, Portainer locks the setup page and you have to restart the container.
3. It finds the local Docker install through the mounted Docker socket.

Mounting the Docker socket gives Portainer full control of the host. That's the reason it's only reachable on my home network and over Tailscale.
