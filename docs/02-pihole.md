# Pi-hole

Pi-hole is a DNS server that blocks ad and tracking domains. Any device that uses it for DNS gets blocking without installing anything.

1. Free up port 53 first (see below).
2. Set `PIHOLE_PASSWORD` in `.env`, then `docker compose up -d pihole`.
3. The admin page is at `http://<server-ip>:8080/admin`.
4. Point devices at the server for DNS. You can do it per device, or once in the router's DHCP settings.
5. To check it's working, run `dig doubleclick.net @<server-ip>`. It should come back as `0.0.0.0`.

The web UI is on 8080 so port 80 stays free for a reverse proxy later.

## Port 53 is already in use on Ubuntu

Out of the box, the container can't bind to port 53, because Ubuntu's `systemd-resolved` already listens there. You can see it with:

```sh
sudo ss -tulpn | grep ':53 '
```

To fix it, turn off resolved's stub listener and point `/etc/resolv.conf` at the real resolver file:

```sh
sudo sed -i 's/^#\?DNSStubListener=.*/DNSStubListener=no/' /etc/systemd/resolved.conf
sudo ln -sf /run/systemd/resolve/resolv.conf /etc/resolv.conf
sudo systemctl restart systemd-resolved
```
