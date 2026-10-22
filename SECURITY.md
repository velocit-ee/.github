# Security Policy

Velocitee takes the security and integrity of infrastructure automation, edge provisioning, and privacy systems seriously. This policy outlines our vulnerability reporting process, response timelines, and disclosure commitments across all repositories under the [`velocit-ee`](https://github.com/velocit-ee) organization.

---

## 1. Supported Components & Scope

This policy applies to all active components within the Velocitee ecosystem:

| Component | Repository | Scope & Trust Boundary |
| :--- | :--- | :--- |
| **Vector Gateway** | `velocit-ee/vector-gateway` | Kernel quarantine (`nftables`), claim token validation, REST endpoints, and iPXE netboot staging. |
| **Core Engines** | `velocit-ee/core` | Bare-metal provisioning (VME), network orchestration (VNE), handoff manifests, and renderer backends. |
| **Velocitee Prism** | `core/vector/telia/target/prism` | PII redaction accuracy, HMAC audit receipt verification, and sovereign proxy isolation. |
| **Web Console & API** | `velocit-ee/web` | Frontend authentication, session management, and reverse proxy headers. |

### Out of Scope
* Denial-of-Service attacks through raw volume or hardware resource exhaustion on local networks.
* Vulnerabilities requiring unauthorized physical console access to target nodes or seed machines.
* Upstream third-party software vulnerabilities (e.g. underlying Linux kernel, Proxmox VE, or OPNsense exploits); these should be reported directly to upstream vendors.

---

## 2. Reporting a Vulnerability

**Do not open public GitHub issues or disclose vulnerabilities in public forums.**

To report a vulnerability, please send an encrypted or direct email to our security team:

* **Security Contact:** [security@velocit.ee](mailto:security@velocit.ee)

### Report Details
To accelerate remediation, please include:
1. Component name and version or commit SHA.
2. A detailed description of the vulnerability and its potential impact.
3. Step-by-step reproduction instructions or a minimal Proof of Concept (PoC).
4. If you wish to use PGP encryption, state this in your initial message and we will provide our current public key.

---

## 3. Vulnerability Response Timeline

Our security team adheres to the following response targets:

* **Initial Acknowledgment:** Within 48 hours of report receipt.
* **Triage & Assessment:** Within 7 calendar days, providing severity classification and planned remediation schedule.
* **Coordinated Disclosure:** We work closely with finders to validate and deploy patches before public disclosure. We request a standard 90-day coordinated disclosure embargo, or until mutual agreement that remediation is complete.
* **Public Attribution:** Security researchers who discover and responsibly report verified vulnerabilities will be credited in release notes and security advisories, unless anonymity is requested.

---

## 4. Provisioning Network & Trust Boundaries

The Vector Metal Engine (VME) serves unattended installation artifacts (including initial cloud-init configurations) over local HTTP during initial bootstrap. 

* **Expected Environment:** Network booting assumes an **isolated provisioning network or dedicated switch**. 
* **In-Scope Boundary Issues:** If an attacker can trigger unauthenticated credential or token leakage outside the designated provisioning subnet onto routed production networks, that behavior is treated as a high-severity vulnerability.
