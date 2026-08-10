# Scope 11 — Final Validation Checklist

## Local validation completed

- [x] README describes the completed lab instead of an unstarted implementation.
- [x] README links to the live case study, complete evidence index, and detailed Scope 9 report.
- [x] Thirteen sanitized Scope 11 captures cover Hyper-V topology, OPNsense interfaces, firewall policy, DHCP/DNS, Source NAT, outbound connectivity, and WireGuard runtime.
- [x] Each Scope 11 capture has an exact matching copy under `docs/assets/images/` for GitHub Pages.
- [x] Local README, evidence-index, and case-study links resolve to existing files.
- [x] The Git diff passes whitespace/error checks.
- [x] Captures exclude passwords, VPN private keys, authentication material, and real public IP addresses.
- [x] LinkedIn, CV, and interview wording is limited to documented implementation and validation evidence.

## Already validated on the current live site

Before these local Scope 11 additions, the existing GitHub Pages main page, CSS, and two Scope 9 evidence images returned HTTP 200. Desktop/mobile navigation, the architecture diagram, network-zone table, evidence previews, and full-resolution links were also validated. HTTPS is enforced and Pages uses `main` with `/docs` as its source.

## Required after commit and push

- [ ] Confirm the new commit is present on the GitHub `main` branch.
- [ ] Wait for GitHub Pages deployment to finish successfully.
- [ ] Confirm the live main page and CSS return HTTP 200 over HTTPS.
- [ ] Open every new Scope 11 image link from the live case study and confirm HTTP 200.
- [ ] Open the claim-to-evidence index on GitHub and test each repository image link.
- [ ] Recheck desktop and mobile layout, navigation, evidence links, and readable image scaling.
- [ ] Recheck the published files for credentials, private keys, authentication material, and unintended identifying data.
- [ ] Record the final commit ID and the live-validation date in the project handoff.

The new Scope 11 files are local until they are deliberately committed and pushed. They must not be described as live before the post-publish checks above pass.
