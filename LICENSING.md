# Licensing & Intellectual Property Policy

Velocitee components are licensed under distinct terms depending on their operational tier, scope, and target deployment environment. This document delineates the governing licenses across all repositories within the [`velocit-ee`](https://github.com/velocit-ee) organization.

---

## 1. Open Source Core Engines — Apache License 2.0

The core engine pipeline—including the **Vector Metal Engine (VME)**, **Vector Network Engine (VNE)**, **Vector Services Engine (VSE)**, **Vector Lifecycle Engine (VLE)**, and the shared engine library located in [`velocit-ee/core`](https://github.com/velocit-ee/core)—is licensed under the [Apache License, Version 2.0](https://www.apache.org/licenses/LICENSE-2.0).

### Permissions & Obligations
* **Commercial & Private Use:** You may freely run, modify, redistribute, and integrate the core engines into commercial products and infrastructure.
* **Attribution & Notice:** All redistributions must include proper copyright attribution and a copy of the Apache 2.0 license.
* **Patent Protection:** The Apache 2.0 license includes an express grant of patent rights from contributors to users.
* **Third-Party Subprocesses:** Third-party upstream tools driven or orchestrated by Velocitee (such as Proxmox VE, OPNsense, Canonical MAAS, OpenTofu, Ansible, and nmap) retain their respective upstream licenses. Velocitee interacts with these tools strictly over external REST APIs, CLI binaries, or network protocols and does not link their source into the Python engine distribution. For full boundary definitions, see the [Core Documentation](https://github.com/velocit-ee/core#readme).

---

## 2. Web Applications & Frontends — MIT License

The public landing applications, documentation themes, and web console interfaces (including [`velocit-ee/web`](https://github.com/velocit-ee/web)) are licensed under the [MIT License](https://opensource.org/licenses/MIT).

* **Terms:** Permissive distribution, modification, private use, and commercial re-use with standard disclaimer of liability.

---

## 3. Carrier Edge & Enterprise Offerings — Proprietary

Commercial carrier distributions, embedded router daemons, and enterprise managed services are proprietary and governed by commercial licensing agreements:

* **Vector Gateway (Carrier Edition):** Statically compiled embedded gateway daemons, kernel-level zero-trust quarantine drivers (`nftables`), and hardware-enforced carrier provisioning firmware.
* **Velocitee Sovereign AI Hub (Enterprise Edition):** Enterprise multilingual PII cleanrooms, compliance receipt ledgers, and sovereign fleet coordination controllers.
* **Managed & Hosted Platforms:** Multi-tenant fleet controllers, telemetry aggregation portals, and managed configuration registries.

No open-source license is granted for proprietary carrier firmware, managed cloud control planes, or enterprise binaries unless explicitly provided under an enterprise master services or commercial OEM agreement.

---

## 4. Trademarks & Brand Assets

"Velocitee", "Velocitee Vector", the shrimp logomark, and associated brand assets are proprietary trademarks of the Velocitee project and its legal entity.

* **Permitted Use:** You may use the name in factual, non-confusing descriptive contexts (e.g., "orchestrated via Velocitee Vector engines").
* **Restricted Use:** You may not use Velocitee trademarks or logos in product names, domain names, or marketing materials in a manner that implies official partnership, sponsorship, or endorsement without written authorization.

---

## 5. Contributor Licensing

All contributions submitted via pull requests across the `velocit-ee` organization are subject to the [Velocitee Contributor License Agreement (CLA)](https://github.com/velocit-ee/core/blob/main/CLA.md).

* **Automatic Submission:** Opening a pull request constitutes acceptance of the CLA terms.
* **Rights Granted:** Contributors license their contributions under the target repository's respective license (Apache 2.0 for `core`, MIT for `web`) and grant the project the authority to defend and re-license the collective work as needed to support long-term sustainability and enterprise partnerships.

---

## Contact & Inquiries

For commercial licensing, enterprise OEM distribution, or legal questions, contact:
* **Legal & Licensing:** [legal@velocit.ee](mailto:legal@velocit.ee)
* **General Inquiries:** [inquiries@velocit.ee](mailto:inquiries@velocit.ee)
