# OPNsense Firewall, VLAN and VPN Lab

> **Status:** Completed and validated local-only homelab.

This project demonstrates the design, implementation, and validation of an isolated network-security lab built with OPNsense and Hyper-V. The environment combines segmented trust zones, controlled firewall policy, core network services, encrypted remote access, traffic logging, packet capture, and evidence-led troubleshooting.

## Implemented Work

- Deployed OPNsense as the firewall and router for a Hyper-V virtual network topology.
- Segmented trusted LAN, DMZ, and SOC/Test networks with interface-specific firewall policy.
- Configured and validated NAT, DHCP, DNS forwarding, and outbound lab connectivity.
- Implemented WireGuard remote access on UDP/51820 with a dedicated VPN network.
- Validated pass and block decisions through client tests, OPNsense filter logs, and interface-level packet capture.
- Applied a repeatable troubleshooting workflow that correlates client behavior, firewall decisions, ingress captures, and inner VPN traffic.

## Validated Network Architecture

| Zone | Interface | Network | Purpose |
| --- | --- | --- | --- |
| WAN | `hn0` | DHCP-assigned | Outbound lab connectivity through the Hyper-V Default Switch |
| LAN | `hn1` | `10.10.10.0/24` | Trusted clients and management |
| DMZ | `hn2` / `OPT1` | `10.10.20.0/24` | Isolated service testing |
| SOC/Test | `hn3` / `OPT2` | `10.10.30.0/24` | Monitoring and controlled testing |
| VPN | `wg0` | `10.10.40.0/24` | Encrypted WireGuard remote access |

## Verified Scope 9 Results

- **DMZ-to-LAN blocking:** ICMP from `10.10.20.198` to `10.10.10.1` was blocked by the `Block DMZ to LAN` rule. The client sent three probes and received no replies; `tcpdump` on `hn2` captured all three requests with zero packets dropped by the kernel.
- **Permitted LAN HTTPS traffic:** TCP/443 from `10.10.10.10` to `10.10.10.1` passed on `hn1` through the anti-lockout rule. `curl` reached the OPNsense HTTPS service and received an HTTP/2 403 application-level response, while the firewall log independently confirmed the pass action.
- **WireGuard visibility:** A WAN-side capture on `hn0` showed bidirectional UDP/51820 traffic, and a tunnel-side capture on `wg0` showed the corresponding ICMP traffic between `10.10.40.2` and `10.10.40.1`.
- **VPN reachability:** The WireGuard client ping completed with 3 transmitted, 3 received, and 0% packet loss.

## Case Study and Evidence

- [Live case study](https://farhanrahmananik.github.io/opnsense-firewall-vlan-vpn-lab/)
- [Detailed Scope 9 evidence](docs/evidence/scope-09-logging-packet-capture-troubleshooting.md)
- [Sanitized DMZ-to-LAN block screenshot](assets/screenshots/scope-09-dmz-lan-block-live-view.png)
- [Sanitized LAN HTTPS pass screenshot](assets/screenshots/scope-09-lan-https-pass-details.png)

## Security and Limitations

This is a safe, isolated Hyper-V homelab, not a production deployment. OPNsense management is restricted to trusted local paths and is not publicly exposed. No credentials, VPN private keys, or real public IP addresses are published in this repository.
