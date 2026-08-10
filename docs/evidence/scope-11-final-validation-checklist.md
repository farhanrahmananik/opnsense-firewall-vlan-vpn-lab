# Scope 11 — Final Validation Checklist

## Local validation completed

- [x] README describes the completed lab instead of an unstarted implementation.
- [x] README links to the live case study, complete evidence index, and detailed Scope 9 report.
- [x] Thirteen sanitized Scope 11 captures cover Hyper-V topology, OPNsense interfaces, firewall policy, DHCP/DNS, Source NAT, outbound connectivity, and WireGuard runtime.
- [x] Each Scope 11 capture has an exact matching copy under `docs/assets/images/` for GitHub Pages.
- [x] Local README, evidence-index, and case-study links resolve to existing files.
- [x] The Git diff passes whitespace/error checks.
- [x] Captures exclude passwords, VPN private keys, authentication material, and real public IP addresses.

## Already validated on the current live site

Before these local Scope 11 additions, the existing GitHub Pages main page, CSS, and two Scope 9 evidence images returned HTTP 200. Desktop/mobile navigation, the architecture diagram, network-zone table, evidence previews, and full-resolution links were also validated. HTTPS is enforced and Pages uses `main` with `/docs` as its source.

## Post-publish validation completed

- [x] Scope 11 evidence commit `db83ac4` is present on the GitHub `main` branch.
- [x] GitHub Pages deployed the updated case study successfully.
- [x] The live main page and CSS return HTTP 200 over HTTPS.
- [x] All thirteen new Scope 11 image URLs return HTTP 200.
- [x] The live README links to the claim-to-evidence index, which is available on GitHub.
- [x] Desktop and exact 390-pixel mobile layouts were rechecked; responsive navigation and horizontal containment behave as intended.
- [x] Published files were rechecked for credentials, private keys, authentication material, and unintended identifying data.
- [x] Live validation was completed on 2026-08-10.

Scope 11 evidence is published and live-validated from evidence commit `db83ac4`.
