# Homelab :sparkles:

A living document of my homelab: an old Dell OptiPlex turned into a self-hosted server I use to learn Linux, Docker, networking and security hands-on.

I'm a Bachelor of IT (Cybersecurity) student at Macquarie University, building towards a career in cybersecurity, with interests across **blue team and red team**. This lab is where I practise both sides: running services securely, monitoring them, and finding and fixing vulnerabilities.

> **What is a homelab?**
> A small lab at home for self-hosting apps, testing new tech and practising for certifications, without risking anything in production.

---

## Hardware

### Dell OptiPlex 7050 Micro
| Part | Spec |
|------|------|
| CPU | Intel Core i7-7700T |
| RAM | 8 GB DDR4 |
| Boot drive | 256 GB NVMe SSD |
| Storage | 2 TB Seagate One Touch (USB, ext4) |
| Network | USB Wi-Fi adapter |
| OS | Ubuntu Server 26.04 LTS (headless) |

### D-Link DIR-X3000Z (AX3000 Wi-Fi 6)
A standalone, isolated network with no internet uplink. Used for security testing and for hosting a Wi-Fi CTF challenge.

---

## Architecture

```mermaid
flowchart LR
    Mac[MacBook] -- Tailscale VPN --> Lab
    Phone[iPhone] -- Tailscale VPN --> Lab
    subgraph Lab[OptiPlex - Ubuntu Server]
        Docker[Docker Engine]
        Docker --> Pihole[Pi-hole]
        Docker --> Portainer
        Docker --> Kuma[Uptime Kuma]
        Docker --> Immich
        Docker --> Greenbone
        Samba[Samba share]
    end
    Lab --> HDD[(2 TB storage)]
```

---

## Tech Stack

| Tool | Purpose |
|------|---------|
| ![Ubuntu](https://img.shields.io/badge/Ubuntu_Server-E95420?style=for-the-badge&logo=ubuntu&logoColor=white) | Server OS |
| ![Docker](https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white) | Containers |
| ![Tailscale](https://img.shields.io/badge/Tailscale-242424?style=for-the-badge&logo=tailscale&logoColor=white) | Private remote access (VPN) |
| ![Pi-hole](https://img.shields.io/badge/Pi--hole-96060C?style=for-the-badge&logo=pi-hole&logoColor=white) | DNS sinkhole and ad blocking |
| ![Portainer](https://img.shields.io/badge/Portainer-13BEF9?style=for-the-badge&logo=portainer&logoColor=white) | Docker management UI |
| ![Uptime Kuma](https://img.shields.io/badge/Uptime_Kuma-5CDD8B?style=for-the-badge&logo=uptimekuma&logoColor=white) | Service monitoring |
| ![Immich](https://img.shields.io/badge/Immich-4250AF?style=for-the-badge&logo=immich&logoColor=white) | Self-hosted photo backup |
| ![Samba](https://img.shields.io/badge/Samba-SMB_share-555555?style=for-the-badge) | Network file share |
| ![Greenbone](https://img.shields.io/badge/Greenbone-in_progress-66C430?style=for-the-badge) | Vulnerability scanning |

---

## Security choices

- **No ports open to the internet.** Remote access only through Tailscale.
- **Admin dashboards locked to localhost.** Portainer, Uptime Kuma and the Pi-hole admin page only listen on the server itself; I reach them through an SSH tunnel.
- **Least-privilege file sharing.** The Samba share allows one named user, no guests.
- **No default passwords.** Database passwords are randomly generated.
- **Secrets stay out of Git.** `.env` files are excluded with `.gitignore`.
- **Key-based SSH** from my Mac.

---

## Builds

### 1. Storage + Samba share
Added a 2 TB drive and shared it to my Mac and iPhone.
- Partitioned with GPT and formatted as ext4
- Auto-mounted with `/etc/fstab` using the drive's UUID and `nofail`, so the server still boots if the USB drive is unplugged
- Samba share restricted to one user; enabled Apple compatibility (`vfs_fruit`) to fix read-only access on iOS

**Learned:** why a 2 TB drive shows as 1.8 TiB in Linux (decimal vs binary units), and why SMB needs to be locked down (it's been the target of major attacks like WannaCry).

### 2. Immich (photo backup)
Self-hosted alternative to Google Photos, running in Docker.
- Database on the fast SSD, photos on the 2 TB drive
- Machine learning disabled to fit in 8 GB of RAM
- Default database password replaced with a random one

**Learned:** Docker Compose, splitting storage by speed, and why membership of the `docker` group is effectively root access.

### 3. Greenbone (in progress)
Open-source vulnerability scanner (OpenVAS).
- Plan: **scan → fix → rescan → document before and after**

---

## Roadmap

- [x] Ubuntu Server, Tailscale, Docker
- [x] Pi-hole, Portainer, Uptime Kuma
- [x] 2 TB storage + Samba
- [x] Immich
- [ ] Greenbone vulnerability scan + report
- [ ] Automated backups (restic, 3-2-1 rule)
- [ ] Isolated lab network with vulnerable targets (Juice Shop, DVWA)
- [ ] Wazuh SIEM for log monitoring
- [ ] Disable SSH password login

---

## Acknowledgements
- [awesome-selfhosted](https://awesome-selfhosted.net/)
- [Markdown Badges](https://github.com/Ileriayo/markdown-badges)
- [r/homelab](https://www.reddit.com/r/homelab/wiki/introduction)
