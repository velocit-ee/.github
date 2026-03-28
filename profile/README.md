# velocit.ee

open source infrastructure automation for schools, labs, and anyone else running real hardware on a shoestring.

---

built at [wiesbaden high school](https://whs-germany.dodea.edu) — proven in a real school lab. now being rebuilt the right way.

**the idea:** your network, your servers, your storage — all declared in one file, deployed in one command. no cloud lock-in, no enterprise contracts, no guessing what changed.

```yaml
# velocitee.yml — the whole lab in one file
nodes:
  - hostname: dolus
    role: compute
    ip: 172.16.10.58
    os: ubuntu-24.04

  - hostname: nas01
    role: storage
    ip: 172.16.67.4
    os: truenas-scale
```

---

## what's here

| repo | what it is |
|------|-----------|
| [core](https://github.com/velocit-ee/core) | the automation engine — ansible, terraform, maas |
| [web](https://github.com/velocit-ee/web) | velocit.ee landing page + waitlist backend |
| [docs](https://github.com/velocit-ee/docs) | guides, architecture, deployment walkthroughs |

---

## philosophy

> shed the old. rebuild stronger.

labs die when they're too fragile to touch. velocit.ee is the opposite — every node is reproducible, every config is in git, every deployment is a one-liner.

we're not building for the enterprise. we're building for the people running `dd if=ubuntu.iso` at midnight because the lab needs to be up by 8am.

---

## status

early. working. being used in production.

join the waitlist at [velocit.ee](https://velocit.ee) if you want updates.

---

*[contribute](https://github.com/velocit-ee/core/blob/main/CONTRIBUTING.md) · [report a bug](https://github.com/velocit-ee/core/issues/new?template=bug.yml) · [inquiries@velocit.ee](mailto:inquiries@velocit.ee)*
