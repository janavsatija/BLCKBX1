# Network architecture and security

## Current design

The OptiPlex hosts self-hosted services. Remote administration uses Tailscale and SSH tunnels. The D-Link DIR-X3000Z is a separate standalone network with no internet uplink, intended for authorised security exercises.

## Earlier experiments
I explored using the OptiPlex as a gateway to the D-Link, including static addressing, forwarding, NAT and firewall chains. This is historical experimentation, not the current topology.

## Controls
- No publicly forwarded inbound service ports
- Key-based SSH configured; enforcing key-only access remains planned
- Administrative dashboards restricted to localhost
- Samba restricted to an authenticated user
- Random database credentials and changed Greenbone default credentials
- Sensitive configuration excluded from Git

## Verification and limitations
Network isolation should be tested before deploying vulnerable targets. Review listening sockets, firewall rules, Docker port publishing and VPN access policy. Do not assume UFW alone controls every Docker-published port.

## Next steps
Backups and recovery, SSH hardening, then centralised security logging. No vulnerable targets should be deployed until isolation is verified.
