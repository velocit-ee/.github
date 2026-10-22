# Contributing to Velocitee

Thank you for your interest in contributing to Velocitee. This guide outlines the development standards, code quality gates, and submission workflows required to ensure consistency across the ecosystem.

---

## 1. Before You Start

* **Issue First for Non-Trivial Changes:** For significant features, architectural modifications, or changes to engine handoff manifests, open an issue first to discuss the design with maintainers.
* **Review Existing Work:** Check [Open Issues](https://github.com/velocit-ee/core/issues) and active pull requests before starting work to avoid duplicate effort.
* **Direct PRs for Small Fixes:** Bug fixes, documentation corrections, and test coverage improvements are welcome as direct pull requests.

---

## 2. Repository & Development Setup

The open-source engine stack is organized in [`velocit-ee/core`](https://github.com/velocit-ee/core) as a unified Python distribution (`shared`, `vme`, `vne`, `vse`, `vle`).

```bash
# Clone the repository
git clone https://github.com/velocit-ee/core.git
cd core

# Create and activate virtual environment (Python 3.11+ required)
python3 -m venv .venv
source .venv/bin/activate

# Install editable development distribution and test suites
pip install -e '.[dev]'

# Verify test suite
pytest

# Optional: Install pre-commit hooks
pre-commit install
```

### External Dependencies
* **Engine Backends:** Testing the `opentofu+ansible` provisioner backend requires `tofu` and `ansible-playbook` binaries installed on your host (install with `pip install -e '.[opentofu_ansible]'`).
* **Carrier Gateway (Rust):** If contributing to the native carrier edge daemon (`vector-gateway`), a standard Rust 2021 toolchain with `cargo` and `clippy` is required.

---

## 3. Development Workflow

1. **Fork and Branch:**
   Create a focused feature branch from `main`:
   ```bash
   git checkout -b <type>/<short-description>
   ```
   Branch naming prefixes:
   * `feat/` — New functionality or capabilities
   * `fix/` — Bug fixes and regression repairs
   * `docs/` — Documentation updates and architectural guides
   * `refactor/` — Code refactoring without behavioral or interface changes
   * `test/` — Test harness additions and coverage improvements

2. **Code Standards & Architecture:**
   * **Manifest Integrity:** Engines communicate strictly via standardized JSON handoff manifests (`manifest.json`). Interfaces must adhere to the JSON schema definitions.
   * **Zero Hardcoding:** Never commit hardcoded IP addresses, site credentials, or environment-specific values. Use structured configurations or environment variables.
   * **Subprocess Hygiene:** Upstream tools (OpenTofu, Ansible, nmap) must be invoked as subprocesses or over REST APIs. Never tightly couple external copyleft libraries into the Python core.

3. **Validation & Quality Gates:**
   Ensure all tests, formatters, and linters pass before opening a pull request:
   ```bash
   # Run pytest across all engine test suites
   pytest

   # Run Ruff code analysis and formatting checks
   ruff check .
   ruff format --check .
   ```

4. **Conventional Commits:**
   Format commit messages according to the [Conventional Commits specification](https://www.conventionalcommits.org/):
   ```
   feat(vne): add automated verification gate for OPNsense firewall state
   fix(vme): reject unhashed passwords during preflight validation
   docs: document OpenWrt cross-compilation pipeline for ARM64 routers
   ```

---

## 4. Pull Request Checklist

Before submitting your pull request, confirm the following criteria:

- [ ] All automated tests pass (`pytest` and, if applicable, `cargo test`).
- [ ] Code conforms to style guidelines and linter checks pass (`ruff check .`).
- [ ] New functionality includes corresponding unit or integration tests.
- [ ] Documentation and example configurations (`velocitee.yml`, `vme-config.example.yml`) are updated to reflect interface changes.
- [ ] Engine status changes update `engines.json` and are verified with `python tools/render_engine_status.py --check`.
- [ ] Commits adhere to Conventional Commit formatting.

---

## 5. Architectural Guardrails (What We Do Not Merge)

To protect the integrity, security, and portability of Velocitee, the following contributions will not be accepted:

* **Vendor-Locked Implementations:** Code targeting specific proprietary hardware or hypervisors without abstraction through the pluggable renderer registry.
* **Telemetry & Phoning Home:** Any unsolicited phone-home telemetry, forced cloud phone-ins, or dependencies on third-party cloud accounts for self-hosted execution.
* **Untested Execution Paths:** Pull requests introducing critical engine logic without automated test coverage or verified lab execution logs.
* **Licensing Encroachment:** Modifications that introduce copyleft license contagion into Apache 2.0 or MIT repositories.

---

## 6. Contributor License Agreement (CLA)

By submitting a pull request to any repository within the `velocit-ee` organization, you agree to the terms of the [Velocitee Contributor License Agreement](https://github.com/velocit-ee/core/blob/main/CLA.md). No separate paperwork is required; the submission of the pull request establishes the agreement.

---

## 7. Security & Code of Conduct

* **Security Vulnerabilities:** Never report security vulnerabilities via public GitHub issues. Follow our coordinated disclosure process in [SECURITY.md](SECURITY.md) or email [security@velocit.ee](mailto:security@velocit.ee).
* **Community Standards:** All contributors and maintainers are expected to adhere to the [Code of Conduct](CODE_OF_CONDUCT.md).

For questions or developer discussions, join our community forums or email [inquiries@velocit.ee](mailto:inquiries@velocit.ee).
