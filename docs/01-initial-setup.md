# Project 1: Initial Server Setup & Docker Install

**Goal:** To install Ubuntu Server 24.04 on my old Acer laptop and run the first NGINX container.

**Steps:**
1.  Flashed Ubuntu Server 24.04 LTS to a USB stick using BalenaEtcher.
2.  Installed the OS, ensuring to select "Install OpenSSH server" and "Docker" during setup.
3.  Connected via SSH from my main laptop.
4.  Ran `docker run --name my-first-container -p 8080:80 -d nginx`.

**Problems & Solutions:**
* **Problem:** After installation, I couldn't connect via SSH. The connection was refused.
* **Diagnosis:** I had to connect a monitor and keyboard to the laptop to check the service status with `systemctl status ssh`.
* **Solution:** I realized I had missed the OpenSSH server installation step. I ran `sudo apt install openssh-server` to fix it.

**Key Learnings:**
* Always double-check installation options. A small mistake at the start can cause headaches later.
* SSH is essential for headless server management.