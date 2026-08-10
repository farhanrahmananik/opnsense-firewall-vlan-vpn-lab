# Scope 11 — Portfolio Evidence Index

## Objective

Provide recruiter- and interviewer-readable evidence for the implemented OPNsense, Hyper-V, segmented networking, DHCP/DNS, NAT, firewall-policy, and WireGuard lab.

All captures are sanitized. They contain no passwords, VPN private keys, real public IP addresses, or authentication material. Private RFC1918 lab addresses remain visible where they are necessary to explain the validated topology.

## Architecture and interfaces

| Claim | Evidence | Verified result |
| --- | --- | --- |
| OPNsense runs as the lab firewall VM | [Hyper-V VM and adapter mapping](../../assets/screenshots/scope-11-hyperv-opnsense-network-adapters.png) | `OPNsense-FW01` was running as a Generation 2 VM with adapters mapped to the Default, LAN, DMZ, and SOC virtual switches. |
| Physical lab interfaces are separated | [OPNsense `hn0`–`hn3` overview](../../assets/screenshots/scope-11-opnsense-interfaces-hn0-hn3.png) | WAN used DHCP on `hn0`; LAN, DMZ, and SOC/Test used `hn1`, `hn2`, and `hn3` with their documented `/24` networks. |
| WireGuard uses a dedicated tunnel network | [OPNsense `wg0` overview](../../assets/screenshots/scope-11-opnsense-wireguard-wg0.png) | `wg0` used `10.10.40.1` with the `10.10.40.0/24` VPN route. |

## Firewall policy

| Claim | Evidence | Verified result |
| --- | --- | --- |
| LAN access is explicitly permitted by service and destination | [LAN firewall rules](../../assets/screenshots/scope-11-opnsense-firewall-rules-lan.png) | Visible rules permitted controlled SSH, HTTPS, and ICMP access to lab zones, DNS to the firewall, and outbound HTTPS. |
| DMZ is isolated from trusted and monitoring networks | [DMZ firewall rules](../../assets/screenshots/scope-11-opnsense-firewall-rules-dmz.png) | OPT1 rules blocked LAN and SOC/Test access while permitting DNS to the firewall and outbound HTTPS. |
| SOC/Test is isolated from LAN and DMZ | [SOC/Test firewall rules](../../assets/screenshots/scope-11-opnsense-firewall-rules-soc-test.png) | OPT2 rules blocked LAN and DMZ access while permitting DNS to the firewall and outbound HTTPS. |

## DHCP, DNS, and outbound connectivity

| Claim | Evidence | Verified result |
| --- | --- | --- |
| Dnsmasq provides DNS and DHCP to the internal zones | [Dnsmasq service settings](../../assets/screenshots/scope-11-opnsense-dnsmasq-service.png) | Dnsmasq was enabled on LAN, OPT1, and OPT2 with the internal DHCP domain configured. |
| Each internal zone has a dedicated DHCP pool | [DHCP ranges](../../assets/screenshots/scope-11-opnsense-dhcp-ranges.png) | LAN, DMZ, and SOC/Test used `.100`–`.199` pools in their respective `/24` networks. |
| DHCP issued addresses inside the isolated zones | [Sanitized active leases](../../assets/screenshots/scope-11-opnsense-dhcp-active-leases.png) | Dynamic leases were visible in OPT1 and OPT2; MAC and DUID columns were excluded from the published capture. |
| Internal networks receive automatic outbound translation | [Automatic Source NAT](../../assets/screenshots/scope-11-opnsense-source-nat.png) | LAN, OPT1, and OPT2 networks were included in automatically generated translation rules to the WAN address. |
| OPNsense resolves external DNS names | [DNS lookup result](../../assets/screenshots/scope-11-opnsense-dns-lookup.png) | `example.com` returned current A, AAAA, MX, and TXT responses with recorded query times. |
| The firewall has controlled outbound TCP/443 connectivity | [Outbound port probe](../../assets/screenshots/scope-11-opnsense-outbound-port-probe.png) | The built-in diagnostic successfully connected to `example.com:443`. |

## WireGuard runtime

| Claim | Evidence | Verified result |
| --- | --- | --- |
| WireGuard listens on the documented port and exchanged traffic | [WireGuard status](../../assets/screenshots/scope-11-opnsense-wireguard-status.png) | `WG-Remote-Access` used UDP/51820; the peer showed a recorded handshake age and bidirectional transfer counters. No keys were displayed. |

## Traffic-decision and packet-capture evidence

Detailed client, firewall-log, and packet-capture correlation remains documented in the [Scope 9 evidence report](scope-09-logging-packet-capture-troubleshooting.md):

- [DMZ-to-LAN block live view](../../assets/screenshots/scope-09-dmz-lan-block-live-view.png)
- [Permitted LAN HTTPS details](../../assets/screenshots/scope-09-lan-https-pass-details.png)

## Limitations

- The evidence validates an isolated Hyper-V homelab, not a production deployment.
- The DNS lookup and TCP/443 port probe validate firewall-side external resolution and connectivity. The Scope 9 report contains the recorded client-side validation and correlation.
- Runtime values such as lease expiry, DNS answers, handshake age, and transfer counters are point-in-time observations.
