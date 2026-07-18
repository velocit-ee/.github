# contributing to velocit.ee

thanks for wanting to help. here's how it works.

---

## before you start

- check [open issues](https://github.com/velocit-ee/core/issues) — your bug or idea might already be tracked
- for significant changes, open an issue first to discuss before writing code
- for small fixes (typos, docs, obvious bugs), just open a PR

---

## development setup

The engines are one installable Python distribution (`shared` + `vme` + `vne`).

```bash
git clone https://github.com/velocit-ee/core.git
cd core
python -m venv .venv && source .venv/bin/activate
pip install -e '.[dev]'      # installs the whole stack + test/lint tools
python -m pytest             # runs every engine's suite from the repo root
pre-commit install           # optional: run the hooks locally
```

requirements: python 3.11+. The OpenTofu/Ansible provisioner backend also
needs the `tofu` and `ansible-playbook` binaries at runtime (install the
`.[opentofu_ansible]` extra for the Python side).

---

## making changes

1. fork the repo
2. create a branch: `git checkout -b type/short-description`
   - `fix/` for bug fixes
   - `feat/` for new features
   - `docs/` for documentation
   - `refactor/` for internal restructuring with no behaviour change
3. make your changes; add or update tests under the relevant `tests/` dir
4. run `python -m pytest` and `ruff check .` before pushing. Renderer and
   discovery logic is unit-testable without hardware; paths that drive real
   Proxmox/OPNsense/MAAS are verified on a lab box (note it in the PR).
5. commit using [conventional commits](https://www.conventionalcommits.org/):
   ```
   feat(vne): add a Pulumi renderer backend
   fix(vme): reject a config with no password hash in preflight
   docs: document the OPNsense supported-version matrix
   ```
6. open a pull request against `main`

---

## pull request checklist

- [ ] `python -m pytest` passes; new behaviour has a test
- [ ] `ruff check .` is clean
- [ ] no hardcoded IPs, credentials, or site-specific values — use config/env
- [ ] `vme-config.example.yml` / `velocitee.yml` docs updated if new keys added
- [ ] docs updated if behaviour changed; `engines.json` is the single source
      for engine status (run `python tools/render_engine_status.py --write`)
- [ ] conventional commit messages

---

## what we won't merge

- changes that only work against one specific vendor's hardware or hypervisor
  without going through the renderer/backend abstraction
- anything that phones home, requires a cloud account to run self-hosted, or
  adds licensing restrictions to the open engines
- code that hasn't been run at least once

---

## reporting security issues

do not open a public issue for security vulnerabilities. email [security@velocit.ee](mailto:security@velocit.ee) with a description and, if you have one, a proof of concept. we'll acknowledge within 72 hours. see [SECURITY.md](https://github.com/velocit-ee/.github/blob/main/SECURITY.md) for the full policy.

---

## code of conduct

see [CODE_OF_CONDUCT.md](CODE_OF_CONDUCT.md).

---

*questions? open a discussion or email [inquiries@velocit.ee](mailto:inquiries@velocit.ee)*
