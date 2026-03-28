# OSIM Framework — Orthogonal Systems Invariance Method

A systems-based framework for designing, enforcing, and validating security architectures under adversarial conditions.

## What is OSIM?

OSIM is a complete Zero Trust security architecture methodology covering:

- **Structural enforcement** — default-deny firewall policy with explicit-allow only
- **Machine-verifiable invariants** — 17 binary security properties that must hold at all times
- **ATT&CK-mapped threat modeling** — every enforced boundary mapped to MITRE technique IDs
- **Four-layer detection architecture** — structural, network, content, and behavioral
- **Governance-first change management** — firewall-as-code with SHA-256 drift detection
- **Red team validation** — structured scenarios RT-01 through RT-03 with mandatory evidence chains

## Repository Structure
```
osim-core/
├── framework/          OSIM portfolio and architecture documentation
├── runbooks/           Step-by-step build and deployment runbooks
├── bug-reports/        Security tool bug discoveries and patches
└── governance/         Firewall rules, invariants, change logs
```

## Reference Implementation

Five-zone enterprise simulation environment:

| Zone | VLAN | Subnet | Trust Tier |
|------|------|--------|------------|
| MGMT-A (Admin Workstations) | 10 | 10.x.x.0/24 | Tier 0-User |
| MGMT-B (Infrastructure) | 11 | 10.x.x.0/24 | Tier 0-Infra |
| OPS (Operations) | 20 | 10.x.x.0/24 | Tier 1 |
| DMZ (Exposed Services) | 30 | 10.x.x.0/24 | Tier 1-Ext |
| SECURITY (Detection Plane) | 40 | 10.x.x.0/24 | Tier 0-Det |

## Hardware Stack

- **OPNsense 26.1.5** — bare-metal firewall (HP T620 Plus, 5-port Intel NIC)
- **Proxmox VE** — primary hypervisor (Lenovo P520, Xeon W-2135, 64GB RAM, 3.5TB NVMe)
- **Proxmox VE** — isolated red node (Lenovo T480, 48GB RAM)
- **Cisco Catalyst 3560CX** — managed switching, VLAN enforcement boundary

## Security Toolstack

- **Wazuh** — SIEM/EDR
- **Suricata** — IDS/IPS (ET Open rulesets, JA3 TLS fingerprinting)
- **Zeek** — network flow analysis via SPAN
- **MISP** — threat intelligence platform
- **TheHive** — case management
- **Caldera** — adversary emulation
- **Greenbone/OpenVAS** — vulnerability management

## Bug Discoveries

During OSIM homelab commissioning, three bugs were found and patched in OPNsense 26.1.5 core:

| Bug | File | Impact |
|-----|------|--------|
| Python module loaded unconditionally | unbound.inc:206 | DNS failure in chroot |
| Chroot blocks outbound forwarding | unbound.inc:341 | Zero outbound DNS packets |
| forward-addr outside zone block | unbound.inc:307-323 | Forwarders silently ignored |

Full details: [opnsense-unbound-fixes](https://github.com/osim-framework/opnsense-unbound-fixes)

## Author

Alec Sanchez — Security Engineer / Architect  
secureadminpublic@protonmail.com  
[Portfolio](https://alecsanchezsecurityportfolio.netlify.app)

---
*OSIM v2.0 — 2026*
