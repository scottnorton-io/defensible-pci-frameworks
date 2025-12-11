# system-hardening.md

# System Hardening and Configuration Management Framework: Locking Down the Basics So Attackers Can't Get In

System hardening eliminates unnecessary attack vectors through secure configuration, minimal services, and continuous monitoring. Misconfigured systems and default settings create easily exploitable vulnerabilities that attackers systematically scan for and exploit.

## Real-World Configuration Failures

In 2019, Capital One suffered a breach affecting 100 million customers when an attacker exploited misconfigured AWS S3 permissions. The attacker didn't use sophisticated zero-day exploits—they simply accessed data through overly permissive configurations that granted broader access than necessary. The firewall configuration allowed access from any authenticated AWS identity, not just the application's specific identity. Default settings remained in place that should have been hardened for production use.

The breach demonstrated that sophisticated attacks aren't always necessary. Attackers scan continuously for low-hanging fruit—default credentials, unnecessary services, overly permissive firewall rules. Organizations with rigorous hardening standards significantly reduce the exploitable attack surface.

## Defense Architecture

System hardening assumes default configurations are insecure. The goal is establishing and maintaining secure configurations through standards, automation, and continuous monitoring.

### Layer 1: Secure Configuration Standards (PCI DSS 2.2.1)

Hardening baselines define secure system states that all systems must achieve before production deployment. Industry-standard benchmarks from Center for Internet Security (CIS), Defense Information Systems Agency Security Technical Implementation Guides (DISA STIGs), and vendor-specific hardening guides provide proven frameworks tested across millions of systems. Organizations document configuration standards for each system type—web servers, databases, network devices, operating systems—specifying required settings with technical precision. Automated configuration enforcement applies standards consistently through infrastructure-as-code and configuration management tools.

Configuration standards must address service minimization (disable everything not required for business function), secure defaults (change vendor defaults including passwords, sample accounts, unnecessary features), authentication requirements (password complexity, account lockout, MFA), and logging (comprehensive audit trails). Standards should be specific enough for consistent implementation—"enable logging" is too vague, "log all authentication attempts including source IP, timestamp, and result" provides implementable guidance.

**Use Case:** A payment processor develops hardening baselines for their RHEL application servers. The baseline removes all GUI components (unnecessary for servers), disables unused network protocols (IPv6, multicast, unnecessary TCP/UDP services), implements SELinux enforcing mode, configures iptables with default-deny rules, requires key-based SSH authentication with password authentication disabled, and removes compiler toolchains. New servers deploy through automated provisioning that applies these settings before the system joins production networks. Configuration drift scans run daily, alerting on any deviation from baseline.

### Layer 2: Network Security Configuration (PCI DSS 1.1.6)

Firewall and router configurations control traffic flow between network segments and between the cardholder data environment and external networks. Documented network topology diagrams show all cardholder data flows, network segments, and security boundaries. Data flow diagrams illustrate how payment data moves through systems from collection through processing and storage. Firewall rulesets follow deny-all, permit-by-exception principle—block everything by default, then explicitly permit only required traffic. Biannual configuration reviews validate that rules remain necessary and appropriate. Change management processes ensure all rule modifications receive security review and approval before implementation.

Firewall reviews identify rule creep where temporary rules become permanent without proper justification, overly permissive rules added during troubleshooting that grant broader access than necessary, and rules no longer serving business purposes because applications decommissioned or workflows changed. Regular review prevents gradual degradation of network segmentation.

**Real-World Example:** During a firewall review, a financial services company discovers a temporary rule created 18 months earlier allowing any internal host to access production database servers on port 3306. The rule was added during a late-night outage for emergency troubleshooting. It was supposed to be removed the next business day. The rule never got removed. Review identifies the risk, investigation confirms no business justification exists, and the rule is removed. The overly permissive rule created 18 months of unnecessary exposure.

### Layer 3: Patch Management (PCI DSS 6.3.3)

Timely patching closes known vulnerabilities before attackers can exploit them. Automated patch scanning identifies missing patches across all systems in the environment. Risk-based prioritization addresses critical vulnerabilities in internet-facing systems before lower-severity vulnerabilities in internal systems. Testing procedures validate patches in non-production environments before production deployment, identifying compatibility issues or unexpected behavior. Critical patches deploy within 30 days of vendor release, emergency patches for actively-exploited vulnerabilities deploy within days or hours depending on exploitation risk.

Patch management balances speed against stability. Mission-critical payment processing systems require testing to prevent outage from bad patches, but testing cannot delay patches so long that exploitation occurs before deployment. Emergency patch procedures define when speed takes precedence over comprehensive testing—active exploitation shifts risk calculus toward rapid deployment.

**Use Case:** A merchant services provider operates a two-track patch process. Standard patches deploy on a 21-day cycle: Days 1-7 deploy to development, Days 8-14 deploy to test with validation, Days 15-21 deploy to production in rolling phases. Emergency patches for actively exploited vulnerabilities use a 48-hour cycle: Hours 0-12 assess scope and deploy to development, Hours 12-36 deploy to test with critical function validation, Hours 36-48 deploy to production with rollback procedures ready. When a critical vulnerability affecting their payment gateway emerges with active exploitation, emergency procedures activate and the patch deploys globally within 40 hours.

### Layer 4: Change Detection (PCI DSS 10.5.5, 11.5)

File integrity monitoring identifies unauthorized changes to critical system files, application binaries, and configuration files. FIM establishes baselines of authorized system states through cryptographic hashes of critical files. Real-time alerting notifies security when configuration files change, system binaries are modified, or critical data files are accessed unexpectedly. Regular validation scans compare current system state against authorized baselines for all critical systems. Investigation procedures determine whether changes represent authorized maintenance, configuration drift, or malicious modification.

FIM detects both malicious changes from attackers modifying systems to maintain persistence and operational drift from undocumented configuration changes that introduce vulnerabilities. A system administrator manually editing a configuration file to troubleshoot an issue may inadvertently weaken security controls. FIM detects the change regardless of intent, enabling review and remediation.

**Real-World Detection:** A payment platform's FIM alerts on unexpected modification to a web server configuration file at 3 AM on Sunday. Investigation reveals the modification changed authentication requirements from "Require all granted" with IP restrictions to "Require all granted" without IP restrictions, allowing global access. The change wasn't documented in change management systems. Further investigation reveals an attacker compromised the web server through a separate vulnerability and modified the configuration to maintain access. FIM detection enables immediate response—the server is isolated, rebuilt from known-good baselines, and returned to service within 2 hours. Without FIM, the backdoor would have persisted indefinitely.

## Implementation Sequence

1. **Develop configuration baselines** using CIS Benchmarks and vendor guides within 30 days (establish secure state definition)
2. **Audit existing systems** against baselines within 60 days (identify gaps requiring remediation)
3. **Implement automated configuration scanning** within 90 days (continuous compliance verification)
4. **Deploy file integrity monitoring** on critical systems within 60 days (detect unauthorized changes)
5. **Establish change management processes** integrating security review within 90 days (control authorized changes)

## Metrics That Matter

- **Configuration compliance percentage:** Target 100% of systems meeting hardening baselines with exceptions documented and approved
- **Time to deploy critical security patches:** Target <7 days for critical, <30 days for high severity, measured from vendor release to full production deployment
- **Unauthorized configuration changes detected:** Baseline current rate, trend toward zero through improved change management
- **Firewall rule review completion:** Target 100% biannual review completed on schedule with documented justification for all rules

## Configuration as Foundation

System hardening creates the defensive foundation all other controls rely upon. Monitoring systems must be hardened to prevent attackers from disabling logging. Encryption systems must be hardened to protect key material. Authentication systems must be hardened to prevent bypass. Weak system hardening undermines every other defensive layer.

The goal is eliminating unnecessary attack surface and ensuring necessary services operate securely through proven configuration standards and continuous monitoring that detects drift from secure baselines.