# physical-security.md

# Physical Security Framework: Protecting Your Data from the Real-World Threats You Can't See on a Screen

Physical security protects against threats requiring physical presence—facility intrusion, device theft, hardware tampering. Digital security controls offer no protection against adversaries with physical access to systems, making physical security fundamental to overall defense.

## Real-World Physical Security Failures

In 2008, a major data center suffered a breach when an unauthorized individual followed an authorized employee through a secure door—classic "tailgating." The intruder accessed the data center floor, installed hardware keyloggers on payment processing terminals, and left undetected. The keyloggers captured administrative credentials over several weeks before discovery. The breach succeeded not through sophisticated hacking but through physical security failure.

ATM skimming illustrates physical device tampering. Attackers install card readers over legitimate card slots, capturing card data and PINs from unsuspecting customers. The attacks succeed because physical device inspection is infrequent or superficial, allowing skimmers to operate for days or weeks before detection. Regular physical inspection and tamper-evident seals detect skimmers before they capture significant data.

## Defense Architecture

Physical security defense assumes adversaries will attempt facility access. The goal is detecting and preventing physical intrusion through layered controls—perimeter access, area access, device access, and monitoring throughout.

### Layer 1: Facility Access Control (PCI DSS 9.1, 9.2)

Restricting physical access to sensitive areas begins with perimeter controls and extends through layered interior access restrictions. Badge access systems with unique identifiers track who enters and exits secured areas, creating audit trails for investigation. Visitor logs document non-employee access with escort requirements ensuring visitors never access sensitive areas unattended. Video surveillance of entry points provides visual verification and forensic evidence. Security guards for high-value facilities add human assessment to technical controls, identifying suspicious behavior automated systems might miss.

Access control systems should integrate with HR systems for automatic badge deactivation upon termination. An employee terminated at 3 PM should have badge access revoked by 3:01 PM, not the next business day. Audit trails of physical access enable investigation and pattern analysis—repeated failed access attempts, after-hours access by day-shift employees, or access to areas outside job requirements trigger investigation.

**Use Case:** A payment processing data center implements layered physical security. The building entrance requires badge access with reception desk verification. The data center floor requires secondary badge access with biometric verification (fingerprint or facial recognition). Server cabinet rows require tertiary badge access specific to administrators supporting those systems. A compromised badge from a network administrator provides building entry and data center floor access but not cabinet access to payment processing servers. Layering limits compromise impact even when outer controls fail.

### Layer 2: Physical Access Monitoring (PCI DSS 9.3, 9.4)

Surveillance and logging detect unauthorized access and provide forensic evidence. Video recording with minimum 90-day retention captures all access to sensitive areas. Access event logging captures entry and exit timestamps, forced door alarms, and propped-door alerts. Regular review of access logs identifies anomalies including tailgating (two entries with single badge scan), after-hours access without business justification, and attempts to defeat access controls. Quarterly physical security assessments test controls through simulated intrusion attempts and social engineering.

Monitoring without review provides little value. Cameras recording activity that nobody watches and logs that nobody reviews create illusion of security without actual protection. Regular log analysis identifies patterns: an employee accessing the facility every Saturday when no weekend work is scheduled, a badge used simultaneously at multiple locations (badge sharing), or failed access attempts suggesting reconnaissance.

**Real-World Example:** A financial services company reviews physical access logs monthly. Analysis identifies an unusual pattern: a developer's badge accesses the data center at 3 AM every Thursday for the past six weeks, but time tracking systems show no approved after-hours work. Investigation reveals the developer is running unauthorized bitcoin mining operations on company servers. The regular schedule (mining during low-utilization hours) and badge-based attribution enable investigation. Access logs transform physical security from deterrence to detection.

### Layer 3: Media & Device Security (PCI DSS 9.8)

Secure destruction prevents data recovery from discarded media. Cross-cut shredding renders paper documents unrecoverable. Degaussing or physical destruction eliminates data from magnetic media including hard drives and backup tapes. Cryptographic erasure suffices for encrypted solid-state media where physical destruction is impractical—overwriting encryption keys makes encrypted data permanently unrecoverable even though data bits remain. Chain of custody documentation tracks media from creation through destruction, preventing uncontrolled disposal.

Disposal without secure destruction creates data breach risk. Dumpster diving remains an effective attack vector against organizations with poor media destruction practices. Attackers recover discarded hard drives, backup tapes, printed reports, and test data files that organizations assumed were destroyed.

**Use Case:** A merchant services provider implements secure media destruction procedures. All paper documents containing cardholder data go into secure shred bins collected weekly by a certified destruction vendor. Hard drives and backup tapes undergo physical destruction (crushing/shredding) rather than simple deletion or formatting. Cryptographic erasure applies to encrypted mobile devices before repurposing. The media destruction vendor provides certificates of destruction with serial numbers of destroyed devices. Annual audits verify destruction records match decommissioned asset records.

### Layer 4: Device Tampering Protection (PCI DSS 9.1.1, 9.9)

Physical security extends to devices handling cardholder data. Payment devices face physical tampering threats including skimmer installation, PIN pad replacement, and card reader modification. Regular inspection identifies tampering attempts through visual examination, comparison to known-good devices, and validation that tamper-evident seals remain intact. Serial number tracking and inventory validation detect device replacement. Secure storage when devices are not in use prevents unauthorized access during non-business hours.

Payment terminal inspection should occur before each business day for high-traffic locations and weekly minimum for lower-traffic locations. Inspection checklist includes visual examination for unusual attachments, verification of serial numbers, validation of tamper-evident seals, and connection verification ensuring only authorized cables are connected.

**Real-World Detection:** A retail chain implements daily point-of-sale device inspection. A store manager performing morning inspection notices a payment terminal feels slightly different—thicker than normal. Closer examination reveals a thin overlay on the PIN pad and an attachment at the card reader. The manager follows reporting procedures, the device is immediately taken out of service, and law enforcement is notified. Forensic analysis confirms a sophisticated skimmer capturing card data and PINs. Because inspection occurred daily, exposure is limited to overnight installation—likely zero transactions compromised. Without inspection, the skimmer could have operated for weeks or months.

## Implementation Sequence

1. **Identify all facilities** storing or processing cardholder data within 30 days (establish complete scope)
2. **Implement badge access and visitor controls** within 90 days (restrict physical access)
3. **Deploy video surveillance and access logging** within 60 days (monitoring capability)
4. **Establish secure destruction procedures** within 30 days (prevent data recovery from disposed media)
5. **Implement device inspection program** within 60 days (detect tampering on payment terminals)

## Metrics That Matter

- **Badge access coverage:** Target 100% of sensitive areas protected by electronic access controls
- **Physical access log review completion:** Target 100% quarterly with documented investigation of anomalies
- **Secure destruction compliance:** Target 100% of retired media destroyed per procedure with certificates maintained
- **Device inspection frequency:** Target per schedule (daily for high-value devices, weekly minimum for others) with 100% completion

## Physical Security as Foundation

Physical security represents the most fundamental defensive layer. Attackers with physical access can bypass most digital controls—installing hardware keyloggers, imaging hard drives, accessing server consoles, replacing firmware, and exfiltrating data through direct device access. No amount of network security, strong authentication, or encryption protects against adversaries who can physically access systems.

The goal is ensuring physical access to systems requires defeating multiple independent controls—building access, area access, device access—with monitoring throughout detecting unauthorized access attempts. Physical security defense assumes determined attackers will attempt physical intrusion, making detection and response capabilities as important as prevention.