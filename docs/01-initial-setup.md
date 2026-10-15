# Installing Ubuntu Server and Docker

The plan was to get Ubuntu Server 24.04 onto the old laptop and run one container on it.

1. Wrote the Ubuntu Server 24.04 LTS image to a USB stick with balenaEtcher.
2. Installed it. The installer asks whether to add OpenSSH server and Docker, and you want both.
3. Logged in over SSH from my main laptop.
4. Started a test container: `docker run --name my-first-container -p 8080:80 -d nginx`

## SSH didn't work at first

After the install, SSH connections were refused. I had to plug a monitor and keyboard back into the laptop to find out why. `systemctl status ssh` showed there was no SSH service at all, because I'd skipped the OpenSSH option in the installer. `sudo apt install openssh-server` fixed it.

Lesson: read the installer screens properly. On a machine without a screen, SSH is the only way in.
