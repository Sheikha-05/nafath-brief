Version: NAFATH-V4 Track: <one of:Software ,AI, Mobile, Networking, Cybersecurity or Data>

## Overview
Trust is not enough: every component must be verified. A national service provider depends on software, AI models, mobile applications, and internet networks. A weakness in any component can threaten the entire service. Secure software requires keeping passwords and secrets separate from source code. AI systems need protection against attacks, while mobile applications must pass security checks. Network security uses RPKI to help prevent unauthorized BGP route announcements. Vulnerability management is also essential, as shown by Log4Shell, a serious flaw in the Java logging library Log4j. Finally, a Software Bill of Materials (SBOM) helps identify software components and track vulnerabilities. Together, these measures improve security, reduce risks, and protect national digital services.
## Software
The Twelve-Factor App methodology recommends storing deployment-specific configuration in environment variables, separate from application code. This includes service credentials, database connections, and environment-specific settings. Keeping secrets out of source code reduces accidental exposure through public repositories, code reviews, and version history. Production systems should also use a managed secrets store where appropriate, with restricted access and regular credential rotation.

Resource: The Twelve-Factor App — III. Config - https://12factor.net/config
## AI
Adversarial machine-learning attacks target different stages of an AI system. Poisoning manipulates training data or the learning process to influence the model before deployment. Evasion changes inputs at inference time to cause incorrect predictions. Privacy attacks attempt to reveal sensitive information about training data, while abuse or extraction attacks may exploit model access to obtain capabilities or information. Defences should match the attack type and the system’s lifecycle.

Resource: NIST AI 100-2 E2025 — Adversarial Machine Learning: A Taxonomy and Terminology of Attacks and Mitigations - https://csrc.nist.gov/pubs/ai/100/2/e2025/final
## Mobile 
The OWASP Mobile Application Security Verification Standard (MASVS) defines security requirements for mobile applications, including data storage, cryptography, authentication, network communication, platform interaction, code quality, resilience, and privacy. Teams use these requirements to define an assessment scope and verify an app through security testing, supported by the OWASP Mobile Application Security Testing Guide (MASTG). Findings help developers identify weaknesses and demonstrate which requirements have been tested and met.

Resource: OWASP Mobile Application Security Verification Standard (MASVS) - https://mas.owasp.org/MASVS/
## Networking
BGP route hijacking occurs when a network announces an IP prefix it is not authorized to originate, potentially redirecting traffic through an unintended network or causing disruption. RPKI supports Route Origin Validation using cryptographically signed Route Origin Authorizations (ROAs), which identify authorized origin autonomous systems for prefixes. Networks can reject or deprioritize invalid announcements. However, RPKI origin validation does not verify every AS along the route or prevent all routing attacks, misconfigurations, or traffic interception.

Resource: RFC 6811 — BGP Prefix Origin Validation - https://www.rfc-editor.org/rfc/rfc6811.html
## Cybersecurity
Log4Shell (CVE-2021-44228) was a critical remote-code-execution vulnerability in Apache Log4j 2, a widely used Java logging library. Certain message lookups could trigger attacker-controlled JNDI connections, allowing code execution on vulnerable systems. Its severity came from remote exploitability, broad software exposure, and the potential for severe compromise. The primary fix is to upgrade affected Log4j deployments to a patched version, identify embedded copies, verify remediation, and investigate possible exploitation. Updating Java alone is not sufficient.

Resource: CISA — Mitigating Log4Shell and Other Log4j-Related Vulnerabilities - https://www.cisa.gov/news-events/cybersecurity-advisories/aa21-356a
## Data
A Software Bill of Materials (SBOM) is a machine-readable inventory of software components and their relationships. It helps teams identify affected products when a dependency has a vulnerability and improves supply-chain transparency. NTIA’s minimum elements include Supplier, Component Name, Version, Other Unique Identifiers, Dependency Relationship, Author of SBOM Data, and Timestamp. An SBOM should be generated and maintained through the software lifecycle, preferably in an automated, machine-readable format such as SPDX or CycloneDX.

Resource: NTIA — The Minimum Elements for a Software Bill of Materials (SBOM) - https://www.ntia.gov/sites/default/files/publications/sbom_minimum_elements_report_0.pdf
## Misconception in My Track
A common misconception is that upgrading Java alone fixes Log4Shell. In fact, the vulnerability was in the Log4j library, so teams must identify affected Log4j versions and update the library or affected products to a patched release. CISA explicitly warns that updating Java is not enough. The correct approach also includes checking embedded dependencies, verifying the fix, and investigating signs of compromise. This distinction matters because a system can remain vulnerable even after its Java runtime has been updated.

Evidence from the CISA resource, “Mitigating Log4Shell and Other Log4j-Related Vulnerabilities,” under the Mitigations section: “patching or updating Java is not enough, you must upgrade the Log4j library itself.”
## Open Question
How can the provider continuously verify third-party software, AI models, and network dependencies after deployment, and connect SBOM data with vulnerability alerts to prioritize remediation?
