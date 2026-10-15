# Project 4: Remote Access with Tailscale

**Goal:** Reach the homelab from anywhere without opening ports on the router.

**Steps:**
1. Install Tailscale on the server (on the host, not in Docker):

```sh
curl -fsSL https://tailscale.com/install.sh | sh
sudo tailscale up
```

2. Install the Tailscale app on my laptop and phone and sign in with the same account.
3. Reach services by the server's Tailscale IP or MagicDNS name, e.g. `http://homelab:8096` for Jellyfin.

**Why Tailscale instead of port forwarding:**
* No ports exposed to the internet, so Pi-hole, Portainer and SSH are never publicly reachable.
* It works behind CGNAT, which many home ISPs use.
* Traffic is end-to-end encrypted with WireGuard.

**Key Learnings:**
* VPN basics: mesh networking, NAT traversal, and why a zero-trust overlay network beats opening ports.
