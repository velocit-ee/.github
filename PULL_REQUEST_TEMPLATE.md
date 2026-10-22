## Description

<!-- Provide a clear summary of what changed and why. -->

## Type of Change

- [ ] Bug fix (non-breaking change fixing an issue)
- [ ] New feature (non-breaking change adding functionality)
- [ ] Refactoring (internal restructuring with no user-facing behavioral change)
- [ ] Performance improvement
- [ ] Documentation update
- [ ] CI/CD or build tooling change

## Verification & Environment

<!-- Detail the test environment and steps used to verify these changes. -->

```markdown
- Hypervisor / Host:
- Operating System:
- Kernel / Architecture:
- Upstream Tooling (OpenTofu, Ansible, etc.):
- Test Results:
```

## Pull Request Checklist

- [ ] All automated tests pass (`pytest` and/or `cargo test`).
- [ ] Linters and formatting checks pass (`ruff check .`, `cargo clippy`).
- [ ] Verified against a real target environment or hardware lab.
- [ ] No hardcoded IP addresses, credentials, or environment-specific secrets.
- [ ] Documentation and example configurations updated for any changed interface.
- [ ] Commit messages follow the Conventional Commits specification.

## Related Issues

<!-- Example: Closes #123 -->
