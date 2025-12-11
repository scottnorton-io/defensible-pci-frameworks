# Defensible PCI DSS v4.0.1 Frameworks

![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)
![PCI DSS](https://img.shields.io/badge/PCI%20DSS-v4.0.1-red.svg)
![Frameworks](https://img.shields.io/badge/Frameworks-12-green.svg)
![Status](https://img.shields.io/badge/Status-Active-success.svg)

**Reorganizing 272 requirements by threat category so you can build actual defense, not just tick compliance boxes.**

```text
┌──────────────────────────────────────────────────────────────────┐
│  PCI DSS v4.0.1 → 12 Defensive Frameworks → Measurable Security  │
│                                                                  │
│  Traditional Approach          Defensive Framework Approach      │
│  ─────────────────────        ──────────────────────────────     │
│  Requirement 1.1.1 ✓          Phishing Attack Defense            │
│  Requirement 1.1.2 ✓            ↳ Layer 1: User Training         │
│  Requirement 1.2.1 ✓            ↳ Layer 2: Email Filtering       │
│  ...                            ↳ Layer 3: MFA Enforcement       │
│  Requirement 12.10.7 ✓          ↳ Layer 4: Monitoring Detection  │
│                                                                  │
│  Result: Compliant            Result: Defensible                 │
└──────────────────────────────────────────────────────────────────┘
```

## What This Is

A complete reorganization of PCI DSS v4.0.1's 272 requirements into 12 threat-based defensive frameworks. Each framework:

- **Addresses a specific attack type** with real-world breach examples
- **Provides layered defense architecture** showing how requirements work together
- **Includes implementation sequences** with realistic timelines
- **Defines measurable metrics** proving effectiveness
- **Maps back to PCI DSS requirements** for audit trail

## Why This Matters

PCI DSS compliance doesn't prevent breaches. Security teams that understand how requirements combine to defeat specific attacks build more effective defenses. This repository transforms compliance checkbox exercise into strategic security architecture.

**Example**: PCI DSS Requirement 8.3.1 requires MFA for administrative access. That's a checkbox. The **Phishing Attack Defense Framework** shows how MFA (Layer 3) combines with user training (Layer 1), email filtering (Layer 2), and behavioral monitoring (Layer 4) to create comprehensive anti-phishing defense. It provides metrics (phishing click rates <5% after 6 months) and real-world examples (Google's zero successful phishing attacks over 2 years with hardware tokens + training).

## The 12 Defensive Frameworks

1. **[Phishing Attack Defense](docs/frameworks/phishing-defense.md)** - Email filtering, training, MFA, behavioral detection
2. **[Insider Threat Defense](docs/frameworks/insider-threat-defense.md)** - Access controls, activity monitoring, privileged action auditing
3. **[Data Exfiltration Prevention](docs/frameworks/data-exfiltration-prevention.md)** - Network segmentation, DLP, encryption, egress monitoring
4. **[DoS Attack Mitigation](docs/frameworks/dos-attack-mitigation.md)** - Traffic monitoring, rate limiting, capacity planning, failover
5. **[Zero-Day Vulnerability Response](docs/frameworks/zero-day-response.md)** - Patch management, WAF, IDS/IPS, incident response
6. **[Third-Party Vendor Risk](docs/frameworks/vendor-risk-management.md)** - Due diligence, contracts, monitoring, compliance verification
7. **[System Hardening](docs/frameworks/system-hardening.md)** - Secure configuration, minimal services, FIM, change management
8. **[Authentication & Authorization](docs/frameworks/authentication-authorization.md)** - Identity management, MFA, RBAC, lifecycle management
9. **[Encryption & Key Management](docs/frameworks/encryption-key-mgmt.md)** - Data-at-rest, data-in-transit, key lifecycle, HSM
10. **[Physical Security](docs/frameworks/physical-security.md)** - Facility access, surveillance, media destruction, device tampering
11. **[Policy & Governance](docs/frameworks/policy-governance.md)** - Policy documentation, procedures, incident response, compliance
12. **[Security Training](docs/frameworks/security-training.md)** - Baseline awareness, role-specific training, simulations, measurement

## Repository Structure

| Path | Description | Link |
|:-----|:------------|:----:|
| **Root** | | |
| `├── README.md` | Main documentation and getting started guide | [📄](README.md) |
| `├── CONTRIBUTING.md` | Contribution guidelines | [📄](CONTRIBUTING.md) |
| `├── CHANGELOG.md` | Version history and releases | [📄](CHANGELOG.md) |
| `├── LICENSE` | MIT License | [📄](LICENSE) |
| **docs/** | Core documentation | |
| `├── 00-introduction.md` | Overview and philosophy | [📄](docs/00-introduction.md) |
| `├── 01-executive-summary.md` | Business case and ROI | [📄](docs/01-executive-summary.md) |
| `├── 02-framework-architecture.md` | How frameworks interconnect | [📄](docs/02-framework-architecture.md) |
| `├── 98-closing-summary.md` | Implementation guidance | [📄](docs/98-closing-summary.md) |
| `├── 99-glossary.md` | Terms and definitions | [📄](docs/99-glossary.md) |
| `└── addendum-platform0.md` | Platform0 reference implementation | [📄](docs/addendum-platform0.md) |
| **docs/frameworks/** | 12 defensive frameworks | |
| `├── phishing-defense.md` | Email filtering, training, MFA, detection | [📄](docs/frameworks/phishing-defense.md) |
| `├── insider-threat-defense.md` | Access controls, monitoring, auditing | [📄](docs/frameworks/insider-threat-defense.md) |
| `├── data-exfiltration-prevention.md` | Network segmentation, DLP, encryption | [📄](docs/frameworks/data-exfiltration-prevention.md) |
| `├── dos-attack-mitigation.md` | Traffic monitoring, rate limiting, failover | [📄](docs/frameworks/dos-attack-mitigation.md) |
| `├── zero-day-response.md` | Patch management, WAF, incident response | [📄](docs/frameworks/zero-day-response.md) |
| `├── vendor-risk-management.md` | Due diligence, contracts, monitoring | [📄](docs/frameworks/vendor-risk-management.md) |
| `├── system-hardening.md` | Secure config, minimal services, FIM | [📄](docs/frameworks/system-hardening.md) |
| `├── authentication-authorization.md` | Identity management, MFA, RBAC | [📄](docs/frameworks/authentication-authorization.md) |
| `├── encryption-key-mgmt.md` | Data-at-rest, data-in-transit, key lifecycle | [📄](docs/frameworks/encryption-key-mgmt.md) |
| `├── physical-security.md` | Facility access, surveillance, media destruction | [📄](docs/frameworks/physical-security.md) |
| `├── policy-governance.md` | Policy documentation, procedures, compliance | [📄](docs/frameworks/policy-governance.md) |
| `└── security-training.md` | Awareness training, simulations, measurement | [📄](docs/frameworks/security-training.md) |

## Quick Start

### For Security Teams

1. **Start with your biggest threat**: If phishing is your primary concern, read `phishing-defense.md` first
2. **Identify gaps**: Compare your controls against the framework's 4-layer architecture
3. **Prioritize implementation**: Use the implementation sequence and timeline
4. **Measure effectiveness**: Track the metrics that matter

### For Compliance Teams

1. **Map existing controls**: Each framework shows which PCI DSS requirements it addresses
2. **Identify control gaps**: Missing requirements become obvious when viewed as incomplete defenses
3. **Explain to auditors**: "We implement MFA as part of our phishing defense strategy" is more defensible than "We do it because requirement 8.3.1 says so"

### For Executives

Read:

1. `00-introduction.md` - What and why
2. `01-executive-summary.md` - Business case
3. `98-closing-summary.md` - Implementation approach and ROI

## Real-World Impact

**Traditional compliance approach**:

- 6-12 months to "achieve compliance"
- Requirements implemented in isolation
- Limited understanding of security posture
- High breach risk despite compliant status

**Defensive framework approach**:

- 3-6 months to defensible security posture
- Requirements implemented as cohesive defenses
- Clear metrics showing security effectiveness
- Compliance as byproduct of security

## Who This Is For

- Security architects building PCI DSS environments
- Security engineers implementing controls
- Compliance teams preparing for assessments
- QSAs and ISAs helping clients understand requirements
- CISOs prioritizing security investment
- Developers building payment processing systems

## Optional: Platform0 Reference Implementation

The `addendum-platform0.md` demonstrates how these frameworks can be implemented as platform capabilities rather than application responsibilities. Platform0 is a Docker-first, stack-agnostic developer platform that implements 8 of 12 frameworks as built-in patterns.

**Platform0 provides**:

- Authentication and audit logging by default
- Policy-as-code enforcement in CI pipelines
- Automatic SBOM and vulnerability scanning
- Evidence generation for auditors
- Reference implementations in Python and Go

Platform0 is optional - the frameworks are implementation-agnostic and valuable regardless of your technology stack.

## Contributing

Contributions welcome! See `CONTRIBUTING.md` for guidelines.

**Especially valuable**:

- Additional real-world breach examples
- Industry-specific adaptations
- Updated metrics from production implementations
- Technical corrections and clarifications

## License

MIT License - See `LICENSE` for details.

These frameworks are based on publicly available PCI DSS v4.0.1 requirements published by PCI Security Standards Council. This repository provides interpretation and implementation guidance, not the official standard.

## Changelog


See `CHANGELOG.md` for version history.

## Acknowledgments

- **PCI Security Standards Council** for publishing PCI DSS v4.0.1
- **Security researchers and incident response teams** whose breach analyses inform these frameworks
- **Organizations** that have shared implementation experiences

## Get Started

Begin with: `Introduction to Defensive Frameworks`

Or jump directly to the framework addressing your biggest threat.
