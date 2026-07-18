# licensing

velocit.ee is split across multiple components with different licenses. here's what applies where.

---

## velocit-ee/core — apache 2.0

the engine stack (VME, VNE, VSE, VLE and the shared library — Python, with an iPXE/dnsmasq/nginx seed stack and optional OpenTofu/Ansible renderers) is licensed under the [apache license 2.0](https://www.apache.org/licenses/LICENSE-2.0).

you can use it, modify it, redistribute it, and build commercial products on top of it. you must include attribution and the license notice. you cannot use the velocit.ee name or logo to imply endorsement of your product.

the third-party tools velocitee drives or invokes (Proxmox VE, OPNsense, MAAS, OpenTofu, Ansible, nmap, …) keep their own licenses; velocitee talks to them over their APIs or as subprocesses and never links them into its code. the full boundary is documented in the [core README](https://github.com/velocit-ee/core#readme).

---

## velocit-ee/web — mit

the landing page and waitlist backend are licensed under the [mit license](https://opensource.org/licenses/MIT).

do whatever you want with it. attribution appreciated but not required.

---

## velocit-ee hosted service — proprietary

if velocit.ee ever offers a hosted or managed service, that service is proprietary. the code powering it may not be the same as the open source components above, and no license is granted to use, copy, or redistribute it.

---

## trademarks

"velocit.ee" and the shrimp logo are not covered by any open source license. you can reference the project by name in factual contexts (e.g., "built with velocit.ee tooling"). you cannot use the name or logo in a way that implies endorsement or that your product is officially affiliated with velocit.ee.

---

## contributing

by submitting a pull request to any velocit-ee repository, you agree to the [Contributor License Agreement](https://github.com/velocit-ee/core/blob/main/CLA.md). in short: your contribution is licensed under the repository's license (apache 2.0 for `core`, mit for `web`), you confirm you have the right to submit it, and you grant velocitee the flexibility to relicense the combined work later. no separate signing step — opening the PR is the agreement.

---

*for licensing questions: [inquiries@velocit.ee](mailto:inquiries@velocit.ee)*
