# Vulnerability management case study: TCP timestamps

## Finding
An authorised Greenbone/OpenVAS assessment of my own Ubuntu server identified TCP timestamps as a low-severity information disclosure finding. Timing information can assist reconnaissance and uptime estimation in some circumstances.

## Remediation
The kernel setting was changed to disable TCP timestamps.

```bash
sudo sysctl -w net.ipv4.tcp_timestamps=0
sysctl net.ipv4.tcp_timestamps
```

## Verification
The updated kernel setting was confirmed. A follow-up scanner result and persistence after reboot are not yet documented.

## Trade-offs
TCP timestamps also serve legitimate TCP functions. Disabling them is a context-specific hardening choice, not a universal recommendation.

## Next steps
Record a sanitised finding, confirm persistence, perform a follow-up scan and document the outcome.

## Lesson
Scan → assess → remediate → verify → document.
