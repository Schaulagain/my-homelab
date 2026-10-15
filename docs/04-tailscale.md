# Tailscale

I wanted to reach the server from outside the house without forwarding ports on the router.

Tailscale goes on the host, not in Docker:

```sh
curl -fsSL https://tailscale.com/install.sh | sh
sudo tailscale up
```

Then install the Tailscale app on the laptop and phone and log in with the same account. The services are reachable at the server's Tailscale IP or its MagicDNS name, e.g. `http://homelab:8096` for Jellyfin.

Why not just forward ports:

- Nothing is open to the internet, so Pi-hole, Portainer and SSH can't be reached by strangers.
- Many home ISPs use CGNAT, which makes port forwarding impossible anyway. Tailscale still works behind it.
- Connections go over WireGuard, so they're encrypted.
