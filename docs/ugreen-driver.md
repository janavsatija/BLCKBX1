# Case study: UGREEN AX900 on Ubuntu Server

## Problem
The USB Wi-Fi adapter did not initially provide reliable connectivity on the headless OptiPlex.

## Investigation
The adapter uses an AIC8800D80 chipset. Troubleshooting involved USB device identification, mode switching, firmware, kernel modules, DKMS and kernel logs. Initial driver attempts produced bus errors.

## Outcome
Working wireless connectivity was established and the server became accessible over SSH. Netplan was used for network configuration.

## What I learned
A USB device being detected does not mean its driver or firmware is working. DKMS helps rebuild compatible modules when kernels change, but does not guarantee compatibility.

## Reproducibility checklist
These are diagnostic commands to use when documenting the setup, not a transcript of the original session:

```bash
lsusb
uname -r
dkms status
lsmod
ip link
journalctl -k -b
```

## Evidence still to add
- Exact working driver revision and installation commands
- Sanitised kernel logs showing failure and recovery
- Cold boot and kernel upgrade verification

Avoid blindly installing third-party kernel drivers; review the source and compatibility first.
