Here’s a clean `.md` version of this entire chat — formatted for copy-paste into any Markdown editor.
It includes your full VPN project specification and context, preserving structure, clarity, and technical detail.

---

```markdown
# Privacy-First VPN Project Plan (Chat Export)
_Date: 2025-12-06_

---

## Context

You requested a **complete, actionable project plan and deliverables** to build a **privacy-first VPN product** targeted at journalists and activists — focusing on anonymity, lawful disclosure, and small-scale trust-based deployment.

### Primary Objectives

- Build a **WireGuard-based VPN** (server infra + control plane + Android + Windows clients)
- Enable **anonymous fiat purchase & redemption** (cash vouchers, gift cards, optional Monero)
- Implement **narrow, auditable lawful-disclosure mechanism** (threshold-escrowed tokens)
- Model cost-per-user under scenarios of 10 / 100 / 500 users
- Create deployment roadmap and MVP deliverable set

---

## Project Goals

1. **Anonymity-by-default** — no account ties; voucher-only model.
2. **Offshore infrastructure** — avoid Indian jurisdictional reach.
3. **Auditable transparency** — escrow-based lawful disclosure, no operator abuse.
4. **Scalable, secure MVP** — start with 10 users, expand to 500+.

---

## Deliverables Overview (A → M)

### A. Executive Summary
- Goals, threat model, key tradeoffs, MVP assumptions (10 users, 5GB/day bandwidth/user default).

### B. Architecture Diagram (ASCII + Explanation)
- WireGuard + control-plane + voucher system integration.
- Android/Windows clients via reproducible builds.

### C. Complete MVP Tech Spec
- Server OS: Debian/Ubuntu (idempotent script).
- WireGuard setup, tmpfs configs, nftables rules.
- Control-plane stack: lightweight API (Go / Python / Rust), minimal DB schema (SQLite/PostgreSQL).

### D. Anonymous Purchase Flows
- **Cash → Reseller Voucher:** printed/USB codes; reconciliation offline.
- **Gift Card → Tor Redemption:** redeem via .onion portal.
- **Monero (optional):** privacy crypto channel.
- Metadata minimization, OPSEC steps, and server-side handling for each.

### E. Voucher/Control-Plane Schema + API
- Functions: issue, redeem, revoke, usage.
- Minimal metadata schema, expiration logic, reseller SOP for cash handling.

### F. Server Deployment Script
- Secure Debian/Ubuntu provisioning:
  - WireGuard + nftables
  - journald → volatile, no swap, tmpfs for logs
- Generates client.conf per voucher.

### G. Android APK & Windows Client Packaging
- Sideload only (no Play Store).
- Signed reproducible builds, portable Windows binary.
- Step-by-step install guide.

### H. Billing & Cost Model
Formula:

```

cost_per_user = (monthly_infra + ops_reserve + trustee_reserve) / active_users + per_user_bandwidth_cost

```

Assumptions:
- Avg 50GB/user/month
- VPS: $40/mo for 10TB
- Overage: $0.05/GB

Scenarios:
| Users | Infra (USD) | Bandwidth | Cost/User | Suggested Retail |
|--------|--------------|------------|-------------|----------------|
| 10 | $40 | 500GB | $4.00 | $6.00 |
| 100 | $40 | 5TB | $0.40 | $1.00 |
| 500 | $80 | 25TB | $0.16 | $0.50 |

Break-even analysis included; flat voucher pricing model.

### I. Threshold-Escrow Audit Token Design
- Shamir-split keys (3-of-5 trustees)
- Minimal lawful release metadata.
- Fields: token_id, issued_at, trustee_slices[], hash_commitment.
- Cipher: AES-256-GCM, Ed25519 signing.

### J. OPSEC & User Guide (1-page)
- Live USB/VM recommendations
- WireGuard import guide
- Tor redemption
- Metadata stripping & safe sharing basics.

### K. Deployment & Launch Plan
- MVP → 10 users
- Setup monitoring (Grafana, iperf3 tests)
- Run first security audit
- Onboard trustees for escrow
- Publish Terms, disclaimers, transparency report.

### L. Legal/Ethics Disclaimer
- Clarify protection limits.
- Users responsible for endpoint OPSEC.
- No guarantee against global surveillance.
- Clear refusal rules for unlawful use.

### M. Final Deliverable Formats
- Scripts, JSON API, config templates, all in markdown or code blocks.
- Operator cheat-sheet (below).

---

## Operator Cheat-Sheet (10 Lines)

1. Issue voucher:
```

./vpnctl issue --quota 100GB --expiry 30d > voucher.json

```
2. Provide code to reseller.
3. Redeem over Tor:
```

curl --socks5 127.0.0.1:9050 -X POST [https://control.onion/redeem](https://control.onion/redeem) -d voucher=CODE

```
4. System generates `client.conf`.
5. Deliver to user securely.
6. Test using `wg show` and `curl ifconfig.me`.
7. Rotate keys monthly.
8. Monitor bandwidth via Grafana.
9. Disable expired vouchers:
```

./vpnctl revoke CODE

````
10. 1 Gbps VPS (10TB/mo) ≈ 100 vouchers @100GB each.

---

## Jurisdiction & Operational Rules

- **Incorporate offshore**: Estonia, Switzerland, Isle of Man, Singapore, Netherlands.
- **No Indian hosting**, block Indian IP ranges.
- **Offshore payment & trust accounts only.**
- **Signing keys stored offshore via multi-party Shamir split.**
- **Offshore registrar/domain with WHOIS privacy.**
- **No Indian ops in production key custody.**
- **Publish legal notice & ToS** explicitly disallowing Indian usage.

---

## Phased Rollout

**Phase 1 — Pilot (10 Users)**
- Manual vouchers, local testing, feedback loop.

**Phase 2 — MVP (100 Users)**
- Automated voucher control-plane, Android/Windows clients.

**Phase 3 — Governance**
- Trustee onboarding, escrow key audits, transparency reporting.

**Phase 4 — Scale (500+)**
- CDN for update delivery, regional servers (non-India), subscription resellers.

---

## Monitoring & Testing Scripts

- Leak test: `curl https://ipleak.net/json`
- Speed test: `iperf3 -c speedtest.server`
- Monitoring: Prometheus + Grafana.
- Build verification: Reproducible build hash diff checks.
- Audit plan: Independent crypto-audit every 6 months (~$3–5k).

---

## VPS & Bare-Metal Deployment Templates

**VPS Template**
```bash
apt update && apt install wireguard nftables fail2ban ufw
wg genkey | tee server.key | wg pubkey > server.pub
````

**Bare Metal**

* LUKS disk encryption
* tmpfs mounts for `/var/log`
* journald volatile mode

---

## Compliance Flags

* Local tax reporting (for resellers only).
* Offshore data protection (GDPR/DPDP awareness).
* Audit trails for voucher issuance (non-identifying).
* Export compliance (encryption notices).

---

## References

* WireGuard official documentation
* Debian Admin Security Guides
* Tor Project – Anonymous Payment Integration
* GDPR / DPDP frameworks
* Shamir Secret Sharing (RFC 3526)

---

## Connected Soarix Context

This VPN project aligns with **Soarix Nexus** (R&D branch) under Soarix Solutions’ ecosystem.
It contributes to privacy-respecting AI infrastructure and can later integrate with **Soarix AI** for automation, **Soarix Publishing** for transparency reports, and **Soarix Media** for ethical communications.

---

## Executive Insight

This system provides a **legally robust privacy backbone** for journalists and high-risk users while maintaining auditability.
Starting small ensures security is proven before scaling. The key success metric is **trust retention** — not user volume.
Once the 100-user MVP passes review, you can open limited beta partnerships or small collective funding rounds for infrastructure sustainability.

---

*End of Document*

```

---

Would you like me to add this as a downloadable `.md` file (so you can save it directly to your system)?
```
