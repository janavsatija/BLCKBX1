# Build journal

Detailed implementation notes and troubleshooting history for [BLCKBX1](../README.md).

## Journey — November 2026 onwards

### 01. Linux foundations and UGREEN driver troubleshooting
Installed headless Ubuntu Server and configured remote administration from my Mac. Getting the UGREEN AX900 working required identifying the AIC8800D80 chipset, troubleshooting USB mode switching, firmware, kernel modules and DKMS, and configuring Netplan. Wireless connectivity and SSH access now work.

**Topics explored:** Linux hardware compatibility, kernel logs, driver dependencies and systematic troubleshooting.

### 02. Networking and container infrastructure
Explored static addressing, subnetting, DHCP, DNS, NAT, Linux forwarding, iptables and UFW while experimenting with the D-Link router. Investigated Tailscale DNS issues and deployed Docker, Pi-hole, Portainer and Uptime Kuma. The D-Link is operational with internet connectivity when required; isolation remains to be verified.

**Topics explored:** network boundaries, secure remote access, service dependencies and the importance of verifying changes.

### 03. BYTE — my own software project
BYTE is a music player and server monitoring dashboard I built, with Spotify integration and a minimalist interface on a repurposed Fire HD 6 tablet. It combines a self-hosted backend, API integration, Android/ADB experimentation and interface design. BYTE is an ongoing project, not a third-party application.

**Topics explored:** application development, deployment, API integration and debugging.

### 04. Personal cloud and vulnerability management
Expanded storage, deployed personal services and began assessing the security of my own infrastructure. The builds below document this stage.

## Builds

### 1. Storage + Samba share
Added a 2 TB drive and shared it to my Mac and iPhone.
- Partitioned with GPT and formatted as ext4
- Auto-mounted via `/etc/fstab` using the drive's UUID and `nofail`, so the server still boots if the USB drive is unplugged
- Samba share restricted to one user; enabled Apple compatibility (`vfs_fruit`) to fix read-only access on iOS

**Topics explored:** why a 2 TB drive shows as 1.8 TiB in Linux (decimal vs binary units), and why SMB needs locking down (it's been the target of major attacks like WannaCry).

### 2. Immich (photo management)
Self-hosted alternative to Google Photos, running in Docker. Independent backup and restore verification remain pending.
- Database on the fast SSD, photos on the 2 TB drive
- Machine learning disabled to fit in 8 GB of RAM
- Default database password replaced with a random one

**Topics explored:** Docker Compose, splitting storage by speed, and why membership of the `docker` group is effectively root access.

### 3. Greenbone / OpenVAS (vulnerability scanning)
Ran a vulnerability scan against my own server.
- Deployed the Greenbone stack in Docker; 195,084 vulnerability tests were available at capture time
- Scanned the server, triaged the findings by severity
- **Finding:** TCP timestamps enabled, which can leak server uptime (Low severity)
- **Configuration change:** disabled with `net.ipv4.tcp_timestamps = 0` in `sysctl`
- **Verified:** confirmed the setting is off; follow-up scan and persistence verification pending

**Topics explored:** how to read a vulnerability report, tell a real finding from an informational one, and the scan → fix → verify loop that vulnerability management runs on.

### 4. Actual Budget
Self-hosted budgeting app in Docker, locked to localhost and reached over an SSH tunnel.

---

## Troubleshooting journal

| Problem | Resolution / lesson |
|---|---|
| UGREEN Wi-Fi adapter not working | Investigated chipset, USB mode switching, firmware and DKMS; restored connectivity |
| Tailscale DNS issues | Investigated resolver configuration and VPN DNS behaviour |
| Docker permission denied | Configured Docker group membership; learned it is effectively root-equivalent |
| iOS Samba share read-only | Configured Apple-compatible `vfs_fruit` |
| Empty Immich database password | Used `/dev/urandom` to generate credentials when OpenSSL was unavailable |
| Localhost-only dashboards inaccessible remotely | Used SSH tunnels rather than exposing administrative ports |
| Limited RAM | Disabled Immich machine learning |
| Git push blocked by email privacy | Configured GitHub no-reply email and PAT authentication |

