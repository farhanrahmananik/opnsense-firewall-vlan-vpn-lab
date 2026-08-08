# OPNsense Firewall, VLAN and VPN Lab

> **Status:** Scope 0 - Planning, Boundaries, and Architecture. Implementation has not started.

This repository will document a safe, local-only homelab built around OPNsense and Hyper-V. It is intended for learning, architecture design, controlled testing, and sanitized documentation - not for exposing lab services to the public internet. OPNsense management must not be exposed publicly.

## Planned architecture

The planned Hyper-V environment will place OPNsense between a WAN-side virtual network and segmented internal networks. The design phase covers virtual switching, interface assignments, trust boundaries, traffic flows, and the following lab networks:

| Zone | Network | Planned purpose |
| --- | --- | --- |
| LAN | `10.10.10.0/24` | Trusted client and administration network |
| DMZ | `10.10.20.0/24` | Isolated services network |
| SOC/Test | `10.10.30.0/24` | Monitoring, analysis, and controlled security testing |
| VPN | `10.10.40.0/24` | Remote-access VPN address pool |

Values that may vary by installation or contain sensitive information will be represented with placeholders such as `<WAN_IP>`, `<VPN_PRIVATE_KEY>`, and `<REDACTED>`.

## Planned goals

- Design the OPNsense and Hyper-V topology, including WAN/LAN connectivity and separation of the LAN, DMZ, and SOC/Test networks.
- Plan NAT behavior and least-privilege inter-zone access without exposing the OPNsense management interface publicly.
- Plan DHCP and DNS services for each internal network.
- Plan secure VPN access using the dedicated `10.10.40.0/24` network and protected key material.
- Define logging, packet-capture, and troubleshooting workflows that avoid publishing secrets or unsanitized traffic.
- Define repeatable validation checks and sanitized evidence requirements before any claims of successful implementation.
- Eventually publish sanitized project documentation with GitHub Pages after the lab has been implemented and validated.

## Scope 0 boundaries

This initial scope contains planning documentation and empty evidence/asset locations only. It does not include Hyper-V scripts, OPNsense configuration, firewall rules, VPN configuration, a GitHub Pages website, screenshots, packet captures, or validation evidence.
