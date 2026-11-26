# OPTIPLEXLAB roadmap

BLCKBX1 is the public portfolio; OPTIPLEXLAB ACADEMY is the learning programme. One build at a time. All unchecked items are planned, not deployed.

## 1. Foundations
- [ ] Rename repository BLCKBX1 and update local Git remote
- [x] Collect nine service screenshots and publish gallery
- [ ] Collect hardware, BYTE and Samba screenshots
- [x] Record RAM, storage and Docker port bindings snapshot (27 Nov 2026)
- [ ] Complete CPU, firewall, exposure and network isolation audit
- [ ] Restic backups, 3-2-1 strategy and restore test
- [ ] Verify SSH keys, evaluate key-only login and MFA without lockout
- [ ] Verify persistent TCP timestamp remediation and rescan

## 2. Infrastructure
- [ ] Glance or Homepage service dashboard
- [ ] Homelable manual network diagram, inventory and rack planning
- [ ] Grafana and Prometheus monitoring
- [ ] Reusable Compose files, runbooks, notifications
- [ ] Evaluate reverse proxy, TLS and central authentication

## 3. Security
- [ ] TRAP: isolated Cowrie honeypot with controlled test activity
- [ ] SENTINEL: Wazuh log ingestion and Suricata IDS
- [ ] Isolated Juice Shop/DVWA and Active Directory lab
- [ ] Purple-team exercise: simulate, detect, investigate, mitigate, retest
- [ ] GODSEYE: verify exact upstream and evaluate authorised research use

## 4. Original projects
- [ ] BYTE: preserve existing version, modular redesign and authenticated API
- [ ] BYTE MINI: CYD touchscreen
- [ ] ORBIT: ISS and satellite tracking, pass predictions, NASA data, space weather
- [ ] Receive-only SDR experiments
- [ ] Optional tablet OS evaluation, retro cyberdeck, music/MIDI, private AI, LED wall, game server and escape-room CTF

## 5. Expansion and automation
- [ ] Measure capacity before RAM or second server purchase
- [ ] Plan 10-inch rack, managed switch, UPS, backup storage and display
- [ ] Proxmox, VLANs, virtual networks
- [ ] Kubernetes/K3s in disposable lab first
- [ ] Ansible, Terraform/OpenTofu, Argo CD, GitOps, CI/CD, secret scanning and registry
- [ ] Disaster recovery and failover exercises

## 6. Career (parallel)
- [ ] Publish Hack Mac and homelab posts with evidence
- [ ] Document troubleshooting case studies
- [ ] Update CV and LinkedIn; join communities
- [ ] Practise interviews, evaluate certifications and apply for roles

## Documentation standard
Learn → design → build → troubleshoot → verify → explain → document → publish. Record evidence, assumptions, rollback and remaining work. Redact private data and secrets. Track knowledge separately from deployment in [ACADEMY.md](ACADEMY.md).
