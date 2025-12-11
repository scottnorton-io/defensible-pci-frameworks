# 99-glossary.md

# Glossary

## General Security Terms

**Assume-Breach Mentality**

Defensive philosophy that assumes perimeter defenses will eventually fail, forcing design of internal controls that detect and contain attackers who have gained access.

**Defense in Depth**

Security strategy employing multiple layers of controls such that breach requires simultaneous failure across several independent defensive layers.

**Least Privilege**

Security principle where users and systems receive only the minimum access required for their specific function, limiting damage potential from compromised accounts.

**Compensating Control**

Alternative security measure implemented when standard PCI DSS requirements cannot be met, providing equivalent protection through different means.

**Zero Trust Architecture**

Security model that assumes no user or system is trustworthy by default, requiring verification for every access request regardless of network location.

## Attack Vectors and Threats

**Business Email Compromise (BEC)**

Phishing attack where attackers impersonate executives or vendors to trick employees into transferring funds or revealing sensitive information.

**Credential Stuffing**

Attack using username/password pairs stolen from other breaches to attempt authentication across multiple services.

**Data Exfiltration**

Unauthorized extraction of data from an organization's systems, typically the ultimate goal of breach attacks.

**Denial-of-Service (DoS)**

Attack that exhausts system resources (bandwidth, CPU, memory, connections) to render services unavailable to legitimate users.

**Distributed Denial-of-Service (DDoS)**

DoS attack executed from many sources simultaneously, typically using compromised devices in a botnet.

**Insider Threat**

Security risk from users with legitimate access who misuse their privileges for malicious purposes or through negligence.

**Lateral Movement**

Attacker technique of moving through a network after initial compromise, seeking higher privileges or access to sensitive data.

**Memory Scraping**

Malware technique that captures payment card data from system memory while being processed, before encryption.

**Phishing**

Social engineering attack using fake emails, websites, or messages to trick users into revealing credentials or sensitive information.

**Ransomware**

Malware that encrypts victim data and demands payment for decryption keys.

**Zero-Day Vulnerability**

Software security flaw unknown to the vendor and without available patches, often exploited before disclosure.

## PCI DSS Specific Terms

**Cardholder Data (CHD)**

At minimum, the full Primary Account Number (PAN). May also include cardholder name, expiration date, and service code.

**Cardholder Data Environment (CDE)**

The people, processes, and technology that store, process, or transmit cardholder data or sensitive authentication data.

**Compensating Controls Worksheet (CCW)**

Documentation required when implementing compensating controls in place of standard PCI DSS requirements.

**Primary Account Number (PAN)**

The payment card number (typically 13-19 digits) that identifies the issuer and account.

**Qualified Security Assessor (QSA)**

Individual certified by PCI SSC to conduct PCI DSS compliance assessments.

**Report on Compliance (ROC)**

Detailed documentation of PCI DSS assessment results for Level 1 and Level 2 merchants and service providers.

**Self-Assessment Questionnaire (SAQ)**

Validation tool for smaller merchants to self-assess PCI DSS compliance.

**Sensitive Authentication Data (SAD)**

Security-related information including full track data, CAV2/CVC2/CVV2/CID, and PINs/PIN blocks. Must not be stored after authorization.

## Technical Controls

**Anti-Malware**

Software that detects, prevents, and removes malicious software including viruses, trojans, ransomware, and spyware.

**Application Whitelisting**

Security control that allows only approved applications to execute, blocking all others by default.

**Behavioral Analytics**

Security monitoring that establishes baselines for normal activity and alerts on deviations indicating potential compromise.

**Content Delivery Network (CDN)**

Geographically distributed servers that cache and serve content, providing both performance and DDoS protection benefits.

**Data Loss Prevention (DLP)**

Security controls that monitor and block unauthorized transmission of sensitive data through network, endpoint, and storage inspection.

**Egress Filtering**

Network security controls that restrict outbound connections from internal systems to prevent data exfiltration and command-and-control communications.

**Hardware Security Module (HSM)**

Physical computing device that safeguards cryptographic keys and performs encryption operations in a tamper-resistant environment.

**Intrusion Detection System (IDS)**

Security tool that monitors network traffic for suspicious activity and alerts on potential threats.

**Intrusion Prevention System (IPS)**

Security tool that monitors network traffic and actively blocks detected threats.

**Multi-Factor Authentication (MFA)**

Authentication requiring two or more verification factors: something you know (password), something you have (token), or something you are (biometric).

**Network Segmentation**

Dividing networks into isolated segments with firewall controls between them, limiting attacker lateral movement.

**Security Information and Event Management (SIEM)**

System that aggregates logs from multiple sources, correlates events, and provides alerting on security incidents.

**Software Bill of Materials (SBOM)**

Comprehensive inventory of software components and dependencies, enabling rapid vulnerability assessment when new CVEs are disclosed.

**Time-Based One-Time Password (TOTP)**

MFA method generating temporary codes that expire quickly, typically used in authenticator apps.

**Web Application Firewall (WAF)**

Security control that filters HTTP/HTTPS traffic to web applications, blocking common attacks like SQL injection and XSS.

## Encryption and Key Management

**AES (Advanced Encryption Standard)**

Symmetric encryption algorithm widely used for encrypting data at rest. AES-256 provides strong protection.

**Encryption at Rest**

Encrypting data while stored on disk or in databases, protecting against physical theft and unauthorized file access.

**Encryption in Transit**

Encrypting data while being transmitted over networks, typically using TLS/SSL protocols.

**Key Management**

Processes and systems for generating, distributing, storing, rotating, and destroying cryptographic keys.

**Key Rotation**

Periodic replacement of encryption keys to limit exposure if keys are compromised.

**TLS (Transport Layer Security)**

Cryptographic protocol providing secure communication over networks, successor to SSL.

## Vulnerability Management

**Common Vulnerability Scoring System (CVSS)**

Standardized framework for rating vulnerability severity on a 0-10 scale based on exploitability and impact.

**Common Vulnerabilities and Exposures (CVE)**

Public database of disclosed security vulnerabilities with unique identifiers (e.g., CVE-2021-44228 for Log4j).

**Patch Management**

Process for testing and deploying software updates that fix vulnerabilities and bugs.

**Penetration Testing**

Authorized simulated attack against systems to identify exploitable vulnerabilities before real attackers do.

**Vulnerability Scanning**

Automated assessment of systems to identify known vulnerabilities, misconfigurations, and security gaps.

## Incident Response

**Indicators of Compromise (IoC)**

Forensic evidence suggesting a system has been breached, such as unusual network traffic, unauthorized files, or anomalous authentication.

**Mean Time to Detect (MTTD)**

Average time from breach occurrence to detection, key metric for security operations effectiveness.

**Mean Time to Respond (MTTR)**

Average time from detection to containment and remediation, indicating incident response capability.

**Security Operations Center (SOC)**

Centralized team and technology for monitoring, detecting, investigating, and responding to security incidents.

## Compliance and Governance

**Risk Assessment**

Systematic process for identifying, analyzing, and evaluating security risks to determine appropriate controls.

**Security Awareness Training**

Program educating personnel on security threats, policies, and proper behaviors to reduce human-factor risks.

**Service Level Agreement (SLA)**

Contract defining expected service levels, including uptime, response times, and performance metrics.

**Third-Party Service Provider (TPSP)**

Vendor or partner that stores, processes, or transmits cardholder data on behalf of another organization.

## Acronyms

**API** - Application Programming Interface

**CAV2/CVC2/CVV2/CID** - Card Verification Values

**CDE** - Cardholder Data Environment

**CHD** - Cardholder Data

**DDoS** - Distributed Denial-of-Service

**DLP** - Data Loss Prevention

**DNS** - Domain Name System

**DoS** - Denial-of-Service

**HSM** - Hardware Security Module

**IDS** - Intrusion Detection System

**IoC** - Indicators of Compromise

**IPS** - Intrusion Prevention System

**MFA** - Multi-Factor Authentication

**MTTD** - Mean Time to Detect

**MTTR** - Mean Time to Respond

**PAN** - Primary Account Number

**PCI DSS** - Payment Card Industry Data Security Standard

**PCI SSC** - Payment Card Industry Security Standards Council

**PIN** - Personal Identification Number

**POS** - Point-of-Sale

**QSA** - Qualified Security Assessor

**ROC** - Report on Compliance

**SAD** - Sensitive Authentication Data

**SAQ** - Self-Assessment Questionnaire

**SBOM** - Software Bill of Materials

**SDLC** - Software Development Lifecycle

**SIEM** - Security Information and Event Management

**SMS** - Short Message Service

**SOC** - Security Operations Center (or Service Organization Control in audit context)

**SQL** - Structured Query Language

**SSL** - Secure Sockets Layer (deprecated, replaced by TLS)

**TLS** - Transport Layer Security

**TOTP** - Time-Based One-Time Password

**TPSP** - Third-Party Service Provider

**VPN** - Virtual Private Network

**WAF** - Web Application Firewall

**XSS** - Cross-Site Scripting