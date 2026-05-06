# velocit.ee

**networks that survive anyone leaving.**

Open-core infrastructure deployment platform — bare metal to a documented,
running stack in four independent engines. Built for the people who keep
small networks alive: school IT closets, nonprofits, homelabs, anywhere
the operator might be a volunteer who'll be replaced in two years and
has to hand off everything they know.

The pitch is *lighter, lower-resource, knowable*. Each engine is small,
single-purpose, and useful on its own. The whole stack runs on a
Raspberry Pi. The handoff manifest between engines is JSON you can read
without a tool.

[![License: Apache 2.0](https://img.shields.io/badge/license-Apache%202.0-blue.svg)](https://github.com/velocit-ee/core/blob/main/LICENSE)
[![CI](https://github.com/velocit-ee/core/actions/workflows/ci.yml/badge.svg)](https://github.com/velocit-ee/core/actions/workflows/ci.yml)
[![Latest release](https://img.shields.io/github/v/release/velocit-ee/core?label=release)](https://github.com/velocit-ee/core/releases)
[![Python 3.11+](https://img.shields.io/badge/python-3.11%2B-blue)](https://www.python.org/)

---

## the pipeline

```
   bare metal
       │
       ▼
   ┌────────┐    ┌────────┐    ┌────────┐    ┌────────┐
   │  VME   │───▶│  VNE   │───▶│  VSE   │───▶│  VLE   │───▶ documented,
   │provision│    │ network │    │services │    │lifecycle│      running
   └────────┘    └────────┘    └────────┘    └────────┘        stack
   PXE boot      OPNsense       containers     monitoring
   + OS install  + VLANs/DHCP   + idempotent   + drift
                 + DNS + FW     + git-driven   + auto-docs
```

Each engine writes a structured **handoff manifest** when it's done. The
next engine reads it and continues. You can enter the pipeline wherever
your hardware already is — bare metal, an existing Proxmox host, a
running OPNsense gateway, an established containerised stack — and you
can stop wherever you like.

---

## engines

### VME — velocitee metal provisioning engine
<!-- ENGINE-STATUS:BEGIN region=engine-pill-vme -->
**Phase 1 · Stable**
<!-- ENGINE-STATUS:END region=engine-pill-vme -->

Boots target hardware over PXE and runs an unattended OS install. Two
selectable backends, same handoff contract:

- **`builtin`** *(default)* — runs a docker-compose seed stack on a
  laptop or a Pi. dnsmasq + nginx + iPXE + cloud-init. No external
  services required.
- **`maas`** *(optional)* — hands provisioning off to an existing
  [Canonical MAAS](https://maas.io) deployment for operators who
  already run one. Uses the MAAS REST API; we don't ship or
  redistribute MAAS.

Writes `vme-manifest.json` describing the provisioned target —
hostname, IP, MAC, OS, SSH key, timing, the backend that ran it —
which every downstream engine consumes.

→ [velocit-ee/core — vme/](https://github.com/velocit-ee/core/tree/main/vme)

### VNE — velocitee network configuration engine
<!-- ENGINE-STATUS:BEGIN region=engine-pill-vne -->
**Phase 2 · Stable**
<!-- ENGINE-STATUS:END region=engine-pill-vne -->

Two paths from one CLI:

- **deploy** — provisions [OPNsense](https://opnsense.org) as a VM on
  Proxmox VE, then configures VLANs, DHCP, DNS, and a baseline firewall.
  Runs an automated verification gate before declaring success. Two
  provisioner backends ship: `velocitee-native` (Python talking
  Proxmox + OPNsense REST directly) and `opentofu+ansible`.
- **join** — discovers the network you're already on, identifies the
  gateway, picks a router adapter (OPNsense / unmanaged catch-all /
  pluggable), and writes a join-mode manifest VSE/VLE can consume.
  Read-only end-to-end. Works on any router; richer integration when
  the gateway has a known API.

→ [velocit-ee/core — vne/](https://github.com/velocit-ee/core/tree/main/vne)

### VSE — velocitee services configuration engine
<!-- ENGINE-STATUS:BEGIN region=engine-pill-vse -->
**Phase 3 · Planned**
<!-- ENGINE-STATUS:END region=engine-pill-vse -->

Deploys containerised services onto the verified network using
idempotent Ansible roles, driven by a config bundle. Designed to be
re-run safely at any time — services converge on the declared state
rather than being imperatively installed once.

### VLE — velocitee lifecycle engine
<!-- ENGINE-STATUS:BEGIN region=engine-pill-vle -->
**Phase 4 · Planned**
<!-- ENGINE-STATUS:END region=engine-pill-vle -->

Monitoring, auto-documentation generated from the chain of handoff
manifests, configuration drift detection against the declared state,
and single-command repair.

---

## built on

velocit.ee is glue. The heavy lifting comes from a small set of
established open-source projects, all permissively licensed and chosen
deliberately to keep the operator's surface area small and the license
boundary clean.

### Provisioning & boot

| Project | Where it's used | License |
|---|---|---|
| [**iPXE**](https://ipxe.org) | VME chainloader bootstrapped over DHCP/TFTP, built from source in the seed stack and embedded with our boot script | GPL v2 (subprocess / artifact, never linked) |
| [**dnsmasq**](https://thekelleys.org.uk/dnsmasq/doc.html) | DHCP + TFTP for the VME seed stack | GPL v2 (run as service, not linked) |
| [**nginx**](https://nginx.org) | HTTP server for VME boot scripts and OS install assets | BSD-2-Clause |
| [**cloud-init**](https://cloud-init.io) / Ubuntu autoinstall | Unattended OS install driver for Ubuntu Server targets | Apache 2.0 / GPL v3 (target side only) |
| [**Proxmox VE**](https://www.proxmox.com/en/proxmox-virtual-environment/overview) automatic-installer | Unattended Proxmox VE installs | AGPL v3 (target product, not embedded) |
| [**Canonical MAAS**](https://maas.io) | Optional VME backend for operators who already run MAAS | Apache 2.0 (REST API client only — no library import) |

### Networking & virtualisation

| Project | Where it's used | License |
|---|---|---|
| [**OPNsense**](https://opnsense.org) | Network appliance VNE deploys: VLANs, DHCP, DNS, firewall | BSD-2-Clause |
| [**Proxmox VE**](https://www.proxmox.com) | Hypervisor VNE drives via REST API | AGPL v3 (target product) |
| [**OpenTofu**](https://opentofu.org) | Infrastructure-as-code engine for the `opentofu+ansible` VNE backend | MPL 2.0 |
| [**bpg/proxmox**](https://registry.terraform.io/providers/bpg/proxmox/latest) Terraform provider | Proxmox API driver under OpenTofu | MPL 2.0 |
| [**Ansible**](https://www.ansible.com) | OPNsense configuration in the `opentofu+ansible` backend (subprocess, not linked) | GPL v3 |
| [**ansibleguy.opnsense**](https://github.com/ansibleguy/collection_opnsense) collection | OPNsense Ansible roles, version-pinned | GPL v3 |

### Discovery & diagnostics

| Project | Where it's used | License |
|---|---|---|
| [**nmap**](https://nmap.org) | Optional service-version + OS fingerprint enrichment in `velocitee-discover` (subprocess, never imported) | NPSL — see *license boundary* |
| Pure Python stdlib | Default scan path: ARP, mDNS, SSDP listening, TCP connect-scan, banner/HTTP/TLS grabs, SNMP v2c sysDescr | PSF |

### Engine runtime (Python)

| Project | Where it's used | License |
|---|---|---|
| [**Pydantic**](https://pydantic.dev) | All config validation and internal schema models | MIT |
| [**Typer**](https://typer.tiangolo.com) | CLI surface for every engine (vme / vne / velocitee-discover) | MIT |
| [**jsonschema**](https://python-jsonschema.readthedocs.io) | JSON-Schema validation of handoff manifests | MIT |
| [**requests**](https://requests.readthedocs.io) | HTTP client for Proxmox, OPNsense, and MAAS REST APIs | Apache 2.0 |
| [**tenacity**](https://tenacity.readthedocs.io) | Retry/backoff policy on transient API errors | Apache 2.0 |
| [**structlog**](https://www.structlog.org) | Structured logging across the stack — JSON for log shippers, key/value for humans | Apache 2.0 / MIT |
| [**passlib**](https://passlib.readthedocs.io) | OPNsense first-boot password hashing (SHA-512 crypt) | BSD |
| [**PyYAML**](https://pyyaml.org) | velocitee.yml + vme-config.yml parsing | MIT |

### Repository & developer tooling

| Project | Where it's used | License |
|---|---|---|
| [**ruff**](https://docs.astral.sh/ruff) | Lint + format for all Python | MIT |
| [**pytest**](https://pytest.org) | Test runner across all engines | MIT |
| [**pre-commit**](https://pre-commit.com) | Local + CI hook orchestration | MIT |
| [**MkDocs Material**](https://squidfunk.github.io/mkdocs-material) | Documentation site at [docs.velocit.ee](https://docs.velocit.ee) | MIT |
| [**Astro**](https://astro.build) | Marketing site at [velocit.ee](https://velocit.ee) | MIT |

### License boundaries — the rules we hold ourselves to

A few of the projects we depend on have licenses that need care. Every
choice below is deliberate and reviewed:

- **GPL-licensed runtimes** (dnsmasq, ansible, ipxe) — we invoke them as
  *subprocesses* or *services*, never link them into our Python code.
  This is the standard, well-understood OSS coexistence pattern.
- **MPL 2.0** (OpenTofu, bpg/proxmox provider) — file-level copyleft;
  full compatibility with our Apache 2.0 codebase.
- **AGPL** (Proxmox VE, OPNsense as products) — they are the things we
  *deploy onto*, not libraries we import. AGPL applies to forks of
  those projects, not to operators driving their REST APIs.
- **NPSL** (nmap) — modified GPL v2 with extra commercial-redistribution
  restrictions. We invoke the binary and parse its XML output; we never
  import a Python wrapper (`python-nmap` and `python-libnmap` are GPL v2
  and would conflict with Apache 2.0). Self-hosted users install nmap
  themselves; we don't ship it.
- **LGPL** (`python-libmaas`) — declined; we use the MAAS REST API
  directly with `requests` to keep the dependency tree clean.
- **BSL** (Terraform, Packer, Vagrant) — declined; we're on OpenTofu.

---

## deployment scenarios

velocit.ee is built around scenarios, not abstract use-cases.

**school IT closet.** A volunteer teacher inherits the rack. A Pi on the
provisioning network runs VME → VNE → VSE → VLE end-to-end. The next
volunteer to take over inherits an auto-generated network diagram, a
manifest of every service running, and a one-command repair tool.

**small nonprofit.** A junior dev sets up the org's first proper
network. They run VME on their laptop to install Proxmox on a
refurbished mini-PC, VNE configures OPNsense + VLANs, VSE deploys their
existing docker-compose stack onto the new host. VLE keeps the docs
honest as the team grows.

**homelab.** Operator already has Proxmox + OPNsense running. They
skip VME entirely, use `vne join` to register the existing network,
and VSE/VLE start managing the services and lifecycle on top of what
they've already built.

**MAAS shop.** Operator already runs Canonical MAAS for inventory and
commissioning. They set `backend: maas` in vme-config.yml, point VME
at their MAAS controller, and the rest of the pipeline (VNE/VSE/VLE)
plugs into the MAAS-provisioned hosts identically to the builtin path.

---

## quick start

```bash
# Install VME on a seed machine (laptop or Pi)
curl -fsSL https://raw.githubusercontent.com/velocit-ee/core/main/vme/install.sh | bash
cd ~/vme/vme

vme setup       # interactive config wizard
vme preflight   # verify the seed machine is ready
vme deploy      # power on the target — everything else is automatic
```

When VME is done it points you at VNE. When VNE is done it points you
at VSE. When VSE is done it points you at VLE.

→ Full guides: [docs.velocit.ee](https://docs.velocit.ee)

---

## config sources

Every engine reads from the same three places:

- a local `velocitee.yml` (or per-engine config like `vme-config.yml`)
- a git repository the engine pulls from
- the velocit.ee authenticated registry *(SaaS tier — AI-assisted
  config generation, schema-validated, version history)*

---

## open source vs SaaS

The engines are open source under **Apache 2.0** and self-hostable.
Fork them, modify them, redistribute them, embed them in commercial
products — go ahead. The patent grant in Apache 2.0 explicitly protects
you from reprisal.

→ [velocit-ee/core](https://github.com/velocit-ee/core)

The [velocit.ee](https://velocit.ee) paid tier adds:

- AI-assisted config generation (guided survey + freeform prompt)
- Authenticated config registry with schema validation + version history
- Drift alerts and remote diagnostics

The SaaS layer is proprietary and lives in a separate repository. The
engines stay open. **Schools and registered nonprofits get the SaaS
tier free.**

---

## documentation

- **Docs:** [docs.velocit.ee](https://docs.velocit.ee) — getting
  started, architecture, references, contribution guidelines
- **Engine source:** [velocit-ee/core](https://github.com/velocit-ee/core)
  — VME, VNE, VSE, VLE, shared library
- **Marketing site:** [velocit.ee](https://velocit.ee)
- **Org profile + brand:**
  [velocit-ee/.github](https://github.com/velocit-ee/.github)

---

## contributing

All contributors sign a [Contributor License Agreement](https://github.com/velocit-ee/core/blob/main/CLA.md)
before merge. The CLA is license-agnostic; it grants velocit.ee the
right to relicense the project later (e.g. dual-licensing for an
embedded SaaS use-case) without rounding up signatures from every
historical contributor.

Read the [contributing guide](https://github.com/velocit-ee/core/blob/main/CONTRIBUTING.md)
and the [code of conduct](https://github.com/velocit-ee/.github/blob/main/CODE_OF_CONDUCT.md)
before opening a PR.

---

<!-- ENGINE-STATUS:BEGIN region=trailing-status -->
```
license:  Apache 2.0 (engines)
status:   VME stable · VNE stable · VSE planned · VLE planned
```
<!-- ENGINE-STATUS:END region=trailing-status -->
