# Network architecture and security

## Current design

The OptiPlex hosts self-hosted services. Remote administration uses Tailscale and SSH tunnels. The D-Link DIR-X3000Z was last documented as a standalone network intended for authorised security exercises; current isolation is unverified.

## Earlier experiments
I explored using the OptiPlex as a gateway to the D-Link, including static addressing, forwarding, NAT and firewall chains. This is historical experimentation, not the current topology.

## Controls
- No public forwarding reported; independent exposure verification pending
- Key-based SSH configured; enforcing key-only access remains planned
- Selected administrative dashboards restricted to localhost; Immich and BYTE are exceptions
- Samba restricted to an authenticated user
- Random database credentials and changed Greenbone default credentials
- Sensitive configuration excluded from Git

## Verification and limitations
Network isolation should be tested before deploying vulnerable targets. Review listening sockets, firewall rules, Docker port publishing and VPN access policy. Do not assume UFW alone controls every Docker-published port.

## Next steps
Backups and recovery, SSH hardening, then centralised security logging. No vulnerable targets should be deployed until isolation is verified.

## Observed service bindings — 27 November 2026

| Service | Host binding |
|---|---|
| Pi-hole admin | Loopback:8081 |
| Pi-hole DNS | LAN and Tailscale:53 TCP/UDP |
| Portainer | Loopback:9443 |
| Uptime Kuma | Loopback:3001 |
| Greenbone | Loopback:443 and 9392 |
| Actual Budget | Loopback:5006 |
| Immich | All interfaces:2283 |
| BYTE | LAN interface:8765 and 8890 |

Listening addresses alone do not establish internet reachability. No firewall changes were made during evidence collection.
