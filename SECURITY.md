# Security policy

This policy covers every repository under the
[velocit-ee](https://github.com/velocit-ee) organization: the engine stack
(`core`), the marketing site and waitlist backend (`web`), and the docs.

## Reporting a vulnerability

**Do not open a public issue for a security vulnerability.**

Email **security@velocit.ee** with:

- a description of the issue and its impact,
- the affected component (`core` / `web` / `docs`) and version or commit,
- steps to reproduce or a proof of concept, if you have one.

You can encrypt sensitive reports — ask in your first email and we'll share a
key.

## What to expect

- **Acknowledgement within 72 hours.**
- An initial assessment and a target remediation window within 7 days.
- Credit in the release notes when a fix ships, unless you'd rather stay
  anonymous.

We ask that you give us a reasonable chance to fix an issue before disclosing
it publicly — coordinated disclosure protects the volunteers and small orgs
who run velocitee.

## Scope

In scope: the engine code and its provisioning flows, the waitlist/contact API,
authentication on the admin surface, the seed-stack containers, and anything
that handles credentials or user data.

Out of scope: findings that require a compromised seed machine or physical
access to the provisioning network (that trust boundary is documented, not a
vulnerability); denial of service through sheer volume; and reports about
third-party projects velocitee merely drives (report those upstream).

## Handling of the provisioning network

VME serves boot artifacts (including cloud-init user-data, which contains a
password hash and SSH public key) over plain HTTP on the provisioning LAN.
This is inherent to PXE and assumes an **isolated provisioning switch**. If you
find a way this leaks onto a routed or shared network, that is in scope.
