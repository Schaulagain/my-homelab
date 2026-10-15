# Project 2: Network-wide Ad Blocking with Pi-hole

**Goal:** Run Pi-hole in Docker so every device on the network (and on Tailscale) gets ad and tracker blocking through DNS.

**Steps:**
1. Free up port 53 (see the Ubuntu gotcha below).
2. Set `PIHOLE_PASSWORD` in `.env` and start it: `docker compose up -d pihole`.
3. Open the admin page at `http://<server-ip>:8080/admin`.
4. Point devices at the server for DNS, either per device or in the router's DHCP settings.
5. Check it works: `dig doubleclick.net @<server-ip>` should return `0.0.0.0`.

**Ubuntu 24.04 gotcha: port 53 is already taken**

Ubuntu runs `systemd-resolved`, which listens on port 53, so the Pi-hole container can't bind to it.

* **Diagnosis:** `sudo ss -tulpn | grep ':53 '` shows `systemd-resolve` holding the port.
* **Fix:** turn off its stub listener and point the system at the real resolver:

```sh
sudo sed -i 's/^#\?DNSStubListener=.*/DNSStubListener=no/' /etc/systemd/resolved.conf
sudo ln -sf /run/systemd/resolve/resolv.conf /etc/resolv.conf
sudo systemctl restart systemd-resolved
```

**Key Learnings:**
* How DNS resolution works on a Linux host, and why only one process can own a port.
* Publishing container ports to the host, and why the web UI goes on 8080 to keep port 80 free.
