# contributing to velocit.ee

thanks for wanting to help. here's how it works.

---

## before you start

- check [open issues](https://github.com/velocit-ee/core/issues) — your bug or idea might already be tracked
- for significant changes, open an issue first to discuss before writing code
- for small fixes (typos, docs, obvious bugs), just open a PR

---

## development setup

```bash
git clone https://github.com/velocit-ee/core.git
cd core
cp velocitee.yml.example velocitee.yml
# edit velocitee.yml for your environment
```

requirements: ansible 2.14+, terraform 1.6+, python 3.10+

---

## making changes

1. fork the repo
2. create a branch: `git checkout -b type/short-description`
   - `fix/` for bug fixes
   - `feat/` for new features
   - `docs/` for documentation
   - `infra/` for ansible/terraform/maas changes
3. make your changes
4. test against a real environment if possible — we do not mock infrastructure
5. commit using [conventional commits](https://www.conventionalcommits.org/):
   ```
   feat(ansible): add role for postgres 16 on ubuntu 24.04
   fix(terraform): correct proxmox vm resource block for cloud-init
   docs: update maas quickstart for ubuntu 24.04
   ```
6. open a pull request against `main`

---

## pull request checklist

- [ ] tested on real hardware or a local VM (document your test environment)
- [ ] no hardcoded IPs, credentials, or site-specific values — use variables
- [ ] `velocitee.yml.example` updated if new vars are introduced
- [ ] docs updated if behavior changed
- [ ] conventional commit messages

---

## what we won't merge

- changes that only work on one specific vendor's hardware without an abstraction layer
- anything that phones home, requires cloud accounts, or adds licensing restrictions
- code that hasn't been run at least once

---

## reporting security issues

do not open a public issue for security vulnerabilities. email [inquiries@velocit.ee](mailto:inquiries@velocit.ee) with the subject line `security:` and a description. we'll respond within 72 hours.

---

## code of conduct

see [CODE_OF_CONDUCT.md](CODE_OF_CONDUCT.md).

---

*questions? open a discussion or email [inquiries@velocit.ee](mailto:inquiries@velocit.ee)*
