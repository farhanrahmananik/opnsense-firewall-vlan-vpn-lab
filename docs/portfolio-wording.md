# Portfolio Wording

Use the versions below without expanding the claims beyond the linked evidence.

## LinkedIn project entry

**OPNsense Firewall, Network Segmentation, and WireGuard VPN Lab**

Built and validated an isolated Hyper-V network-security homelab using OPNsense. Segmented trusted LAN, DMZ, SOC/Test, and WireGuard VPN networks; configured interface-specific firewall policy, automatic outbound NAT, DHCP/DNS services, and UDP/51820 remote access. Verified permitted and denied traffic through client tests, OPNsense filter logs, and interface-level packet captures, then published a sanitized GitHub Pages case study with claim-to-evidence documentation.

**Project:** https://farhanrahmananik.github.io/opnsense-firewall-vlan-vpn-lab/

**Repository:** https://github.com/farhanrahmananik/opnsense-firewall-vlan-vpn-lab

## CV project entry

**OPNsense Firewall, Network Segmentation, and VPN Lab** — Hyper-V, OPNsense, WireGuard, TCP/IP, NAT, DHCP, DNS, tcpdump, Git/GitHub

- Designed and implemented an isolated four-zone Hyper-V lab with OPNsense routing trusted LAN, DMZ, SOC/Test, and WireGuard VPN networks.
- Applied interface-specific allow and block policy, automatic outbound NAT, per-zone DHCP pools, internal DNS service, and WireGuard remote access on UDP/51820.
- Validated pass, block, and VPN flows using client tests, firewall logs, and packet captures across physical and tunnel interfaces; published sanitized evidence and a responsive GitHub Pages case study.

## Interview summary

I built this lab to demonstrate the full firewall workflow, not only configuration screenshots. OPNsense routes separate LAN, DMZ, SOC/Test, and VPN networks in Hyper-V. I applied least-privilege rules between zones, provided DHCP and DNS to the internal networks, configured outbound NAT and WireGuard, and then tested both expected passes and expected blocks. For troubleshooting, I correlated the client result with the firewall decision and packet captures on the ingress or tunnel interface. The public repository contains sanitized evidence, while credentials, private keys, and real public addressing remain excluded.

## Evidence-safe terminology

- Say **segmented networks**, **trust zones**, or **separate Hyper-V virtual switches** for the demonstrated architecture.
- Do not claim production deployment, enterprise scale, high availability, or formal penetration testing.
- Do not claim IEEE 802.1Q VLAN tagging unless separate evidence is added later.
- Describe runtime screenshots as point-in-time validation, not continuous monitoring.
