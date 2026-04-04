# velocit.ee

**networks that survive anyone leaving.**

Open-core infrastructure deployment platform for small nonprofits, small businesses, and low-budget organizations. Four independent, modular engines released in phases — each one useful on its own, each one feeding the next.

---

## engines

### VME — velocitee metal provisioning engine
**phase 1 · in development**

Runs on a seed machine (laptop or Raspberry Pi) connected to the provisioning network. Serves a dnsmasq + nginx + iPXE stack to PXE boot target hardware and install Proxmox VE or Ubuntu Server fully unattended. Writes a structured handoff manifest on success.

→ [velocit-ee/vme](https://github.com/velocit-ee/vme)

---

### VNE — velocitee network configuration engine
**phase 2 · planned**

Consumes the VME handoff manifest. Deploys OPNsense as a VM on Proxmox via Terraform, then configures VLANs, DHCP, DNS, and baseline firewall rules via Ansible. Runs automated connectivity verification before declaring success.

---

### VSE — velocitee services configuration engine
**phase 3 · planned**

Deploys containerized services onto the verified network, driven by a config bundle. Idempotent Ansible roles. Designed to be re-run safely at any time.

---

### VLE — velocitee lifecycle engine
**phase 4 · planned**

Monitoring, auto-documentation generated from handoff manifests, config drift detection, and single-command repair.

---

## config sources

Engines accept config from three sources:

- local raw file
- git repository
- velocit.ee authenticated registry *(SaaS tier)*

---

## open source + SaaS

The full engine stack (VME → VLE) is **Apache 2.0** licensed and self-hostable. No lock-in.

The [velocit.ee](https://velocit.ee) paid tier adds AI-assisted config generation (guided survey + freeform prompt) and an authenticated config registry — for organizations that want the managed path rather than the DIY one.

Schools and nonprofits get the SaaS tier free.

---

```
license:  Apache-2.0 (core engines)
status:   VME in active development · VNE/VSE/VLE planned
```
