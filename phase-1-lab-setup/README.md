# Phase 1 — Lab Setup

## Objective

Build an isolated virtualized environment for a Mini SOC / Security Monitoring and Detection Lab.

The lab is designed around the workflow:

Attack → Telemetry → Detection → Alert → Investigation → MITRE ATT&CK → Incident Response → Remediation

## Host

- OS: Fedora 43 KDE
- CPU: AMD Ryzen 7 7000-series
- RAM: 16 GB
- GPU: NVIDIA RTX 3050 6 GB
- Virtualization: AMD-V
- Hypervisor: KVM/QEMU
- Management: libvirt + virt-manager

## Virtual Machines

| VM | Purpose | Resources |
|---|---|---|
| Kali Linux | Attacker / adversary simulation | 2 CPU, 3 GB RAM, 30 GB |
| Windows 11 | Primary monitored endpoint | 4 CPU, 6 GB RAM, 70 GB |
| Linux Endpoint | Future monitored endpoint | Planned |
| Wazuh/SOC | SIEM/security monitoring | Planned |

## Network Architecture

The lab uses a dedicated libvirt NAT network:

- Network: `10.10.10.0/24`
- Gateway: `10.10.10.1`
- DHCP range: `10.10.10.100 - 10.10.10.200`

Kali uses two interfaces:

- `eth0` — default libvirt network for optional Internet access
- `eth1` — `soc-lab` network for attack traffic

Windows is connected to:

- `soc-lab`

## Current Addresses

Example addresses observed during setup:

- Kali: `10.10.10.107`
- Windows: `10.10.10.186`
- Gateway: `10.10.10.1`

DHCP addresses may change unless static assignments are configured later.

## Isolation

The monitored endpoints and attack traffic use the dedicated `soc-lab` virtual network rather than the physical home LAN.

This allows attack simulations to be performed against intentionally vulnerable or monitored lab systems without directly exposing them to the host's physical network.

## Phase 1 Status

Completed.

Next phase:

**Phase 2 — SOC Infrastructure**