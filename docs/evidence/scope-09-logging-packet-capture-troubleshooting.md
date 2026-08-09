# Scope 9 — Logging, Packet Capture, and Troubleshooting Evidence

## Objective

Validate firewall logging, blocked segmentation traffic, permitted traffic, packet capture, WireGuard traffic visibility, and a repeatable troubleshooting workflow.

## Validated Evidence

### 1. Firewall Logging

OPNsense filter logging was active and contained both pass and block events.

### 2. DMZ to LAN Segmentation Block

- A temporary test interface placed the Ubuntu test host in the DMZ.
- DMZ source: `10.10.20.198`
- Destination: `10.10.10.1`
- Protocol: ICMP
- Client result: 3 transmitted, 0 received, 100% packet loss
- OPNsense interface: `hn2` / `OPT1`
- Firewall action: block
- Rule label: `Block DMZ to LAN`
- `tcpdump` on `hn2` captured all three ICMP echo requests reaching the firewall.
- `tcpdump` reported 0 packets dropped by the kernel.
- The temporary route and temporary DMZ NIC were removed afterward.
- The existing LAN and Mgmt-Temp adapters remained intact.

Reference screenshot: [DMZ-to-LAN block live view](../../assets/screenshots/scope-09-dmz-lan-block-live-view.png)

### 3. Permitted LAN Management Traffic

- Source: `10.10.10.10`
- Destination: `10.10.10.1`
- TCP destination port: `443`
- Interface: `hn1` / `LAN`
- Firewall action: pass
- Rule label: `anti-lockout rule`
- `curl` reached OPNsense HTTPS and received an HTTP/2 403 application-level response, proving that connectivity reached the web service.
- The firewall log independently confirmed that the traffic was passed.

Reference screenshot: [LAN HTTPS pass details](../../assets/screenshots/scope-09-lan-https-pass-details.png)

### 4. WireGuard Packet Evidence

- `wg0` tunnel network: `10.10.40.0/24`
- Client: `10.10.40.2`
- OPNsense: `10.10.40.1`
- WAN-side `tcpdump` on `hn0` showed bidirectional UDP/51820 WireGuard traffic.
- Tunnel-side `tcpdump` on `wg0` showed the corresponding ICMP traffic from `10.10.40.2` to `10.10.40.1`.
- Ping result: 3 transmitted, 3 received, 0% packet loss
- WireGuard runtime evidence showed listening port `51820`, a recent handshake, and bidirectional transfer counters.
- No WireGuard public or private keys are included.

### 5. Troubleshooting Workflow

1. Reproduce the traffic from the client.
2. Confirm client-side success or failure.
3. Check OPNsense firewall logs for the pass/block action and rule label.
4. Capture traffic on the ingress interface with `tcpdump`.
5. For VPN troubleshooting, compare outer WAN UDP/51820 traffic with inner `wg0` traffic.
6. Verify that temporary test changes are removed.
7. Revalidate management access.

## Cleanup and Safety

- No firewall rules were weakened.
- No VPN private keys or credentials were recorded.
- The temporary Evidence-DMZ NIC was removed.
- The temporary DMZ-to-LAN host route was removed.
- Mgmt-Temp remained preserved.
- Final Ubuntu interfaces were LAN (`10.10.10.10/24`), the management path, and WireGuard (`10.10.40.2/24`).
- SSH management through `opnsense-jump` and `opnsense` remained functional.

## Production Considerations

- Centralized log retention or a SIEM would normally be preferred.
- Packet captures should be tightly scoped and handled as potentially sensitive data.
- Management access should be restricted to trusted networks.
- VPN keys and secrets must never be stored in public documentation.

## Limitations

This is an isolated Hyper-V homelab. The captured evidence demonstrates the implemented lab policy rather than a production deployment.
