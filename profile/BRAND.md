# Velocitee — brand guide

Internal reference. Pin the choices so the site, the docs, the READMEs and any
future surface stay coherent. Drift on any of these means a reviewer should ask
"is that intentional, or a one-off?"

## Naming

The product is **Velocitee Vector**: four engines that take hardware from bare
metal to a documented, running stack. `velocit.ee` is the address it lives at,
not the name.

That distinction is the whole point of the 2026 rebrand. The old identity led
with the domain hack — `v` + a caret block + an animated `.ee` underline — which
meant the *URL* was the brand and there was no product noun to attach anything
to. Established infrastructure projects lead with a product: Proxmox VE, Wazuh,
OPNsense. Velocitee does the same.

Note that the repository is still `velocit-ee/core` and the Python distribution
is still `velocitee`. Those are identifiers, not the product name, and renaming
them would break every install and every link for no gain.

| Surface | Form |
|---|---|
| Product | **Velocitee Vector** — the open-source engine stack |
| Project / org, in prose | **Velocitee** |
| GitHub org | `velocit-ee` (hyphenated; required by GitHub) |
| Domain | `velocit.ee` — always lowercase, and only ever an address |
| Python distribution | `velocitee` |
| Engines | `VME`, `VNE`, `VSE`, `VLE` — all caps standalone |
| Engines in prose | "VME — metal", "VNE — network": name, dash, role |
| Console scripts | `vme`, `vne`, `velocitee-discover` |

Never write a command that does not exist. There is no `velocitee deploy`. The
old landing page animated one for a year, and it was the single most damaging
detail on the site because it was trivially checkable.

Do not number the engines inline in marketing copy ("the phase 2 engine"); use
the role.

## Voice

- **Direct.** "VME provisions hardware." Not "VME aims to enable hardware
  provisioning workflows."
- **Sentence case everywhere**, headings included. The old guide called for
  lowercase marketing headlines; that reads as a startup affectation next to
  the documentation, and the two surfaces no longer disagree.
- **No marketing flourish.** "Open-source infrastructure engines" is the
  description. Never "revolutionary", "cutting-edge", "next generation",
  "seamless", "effortless".
- **No emoji** in code, commits, or content.
- **Don't position against MAAS.** Velocitee is "lighter, lower-resource,
  scales down to a Pi" — not "MAAS for small orgs". Naming MAAS as one of VME's
  optional backends is fine; using it as a comparison anchor is not.
- **State the maturity.** Every surface that describes an engine states its rung
  on the ladder. See below.

## Honesty rules

These are brand rules because breaking one damages the project more than any
visual inconsistency could.

- **`engines.json` in velocit-ee/core is the single source of truth for engine
  status.** The READMEs and the docs site regenerate from it via
  `tools/render_engine_status.py`; the website mirrors it in
  `site/src/data/engines.ts`. Change the data, never the rendered copy.
- **The maturity ladder is Planned → Alpha → Beta → Stable**, and an engine
  never claims a rung it has not reached. "It works on my hardware" is evidence
  for Alpha, not Beta; Beta requires the tests to exist.
- **Never show a command, flag or output the software does not produce.** If a
  terminal block appears on a surface, it is real.
- **Never advertise a price for something that does not exist.** The site
  carried a pricing page with monthly figures for tiers that had never been
  built. It is gone, and it does not come back until there is something to sell.
- **Reserved provisioner backends are disclosed as reserved.** The registry
  holds eleven names that validate and then refuse to run. Anywhere the backend
  list appears, that is said plainly.
- **Legal pages are reachable from every page.** Imprint, privacy and terms sit
  in the footer, on every surface, always. This is a legal requirement in
  Germany, and there is a test enforcing it in `velocit-ee/web/test/site.test.mjs`.

## Palette

Light page, dark chrome, one accent. Colour carries meaning: the accent marks
actions and links, and the status colours mean exactly what they say. Nothing is
tinted for decoration.

The previous palette was a dark charcoal terminal aesthetic with three
simultaneous neon accents (blue, green, cyan) and pulsing LED indicators. It
read as a product launch page rather than an infrastructure project.

Tokens live in `velocit-ee/web/site/src/styles/global.css` as `--v-*` custom
properties, mirrored into Tailwind in `tailwind.config.mjs`. Light is the source
of truth; the dark block redefines the values, never the roles.

| Token | Light | Dark | Used for |
|---|---|---|---|
| `--v-page` | `#ffffff` | `#0f1417` | Page background |
| `--v-raised` | `#f5f7f7` | `#151b1f` | Alternating section bands |
| `--v-sunken` | `#14181b` | `#0a0e10` | Command blocks — dark in both themes |
| `--v-ink` | `#10161a` | `#0a0e10` | Header and footer chrome |
| `--v-line` | `#dde3e5` | `#232c31` | Hairlines, table rules, card borders |
| `--v-line-hi` | `#c3cbcf` | `#333f46` | Emphasised borders, form fields |
| `--v-heading` | `#10161a` | `#e8edef` | Headings |
| `--v-body` | `#3b454b` | `#b9c3c8` | Body text |
| `--v-muted` | `#66727a` | `#859399` | Secondary text |
| `--v-faint` | `#98a3aa` | `#5d6b72` | Labels, metadata, table eyebrows |
| `--v-accent` | `#0d6e6b` | `#2aa39e` | The one accent: links, buttons, active nav |
| `--v-alpha` | `#9a5b00` | `#d99b3d` | Alpha status, the maturity notice |
| `--v-ok` | `#16704a` | `#4bb07f` | Passing checks, Beta/Stable status |
| `--v-crit` | `#a72020` | `#e06b6b` | Failures |

Deep teal rather than the default framework blue: it reads as infrastructure and
it does not look templated. Do not introduce a second accent. Status colours are
for status only — never use amber because a card needs visual interest.

## Type

- **IBM Plex Sans** (400/500/600) for everything: headings, body, UI, navigation.
- **IBM Plex Mono** (400/500) for commands, labels, eyebrows, status chips,
  version strings, table headers.
- Self-hosted via `@fontsource/ibm-plex-sans` and `@fontsource/ibm-plex-mono`.
- Heading letter-spacing `-0.011em`. Restrained; the previous `-0.045em` was a
  display-face mannerism.
- **No icon fonts.** Inline SVG only.

Plex is a workhorse pair with a real mono sibling. The previous Space Grotesk is
a display face, which is the wrong register for a page that is mostly tables,
config keys and command lines.

## Motion

**There is none**, beyond hover and focus transitions of ~140ms.

The previous stylesheet ran six keyframe animations on page load: pulsing status
LEDs, a typing terminal, sliding hero text, an animated logo underline, a
gradient travelling along the pipeline connector. Together they were the loudest
signal that this was a landing page rather than a project site, and the pulsing
"live" indicators implied telemetry that did not exist.

If motion is ever reintroduced it must respect `prefers-reduced-motion`, which
the stylesheet already honours globally.

## Brand mark

**There isn't one yet, and nothing should pretend otherwise.**

The identity is currently typographic: the wordmark is "Velocitee" in Plex Sans
600, optionally followed by the product suffix "Vector" in Plex Mono at a
smaller size and muted colour. That is the whole mark.

An earlier pass drew a placeholder glyph — four bars stepping right, one per
engine — and shipped it as the favicon, the docs header logo and the OpenGraph
card. It has been removed. A placeholder mark is worse than no mark: it looks
decided, so it quietly becomes the logo by default, and every surface that
adopts it has to be revisited when the real one lands.

Until then:

- The site, the docs and the OpenGraph card carry the wordmark only.
- There is **no favicon**. Browsers show their default tab icon. That is a
  deliberate, visible gap rather than a filled-in guess.

**When a real mark exists**, adding it touches four places and nothing else:

| Where | What to do |
|---|---|
| `velocit-ee/web/site/src/components/Wordmark.astro` | Add the glyph beside the wordmark. Every surface renders the brand through this component. |
| `velocit-ee/web/site/src/layouts/Base.astro` | Restore the `<link rel="icon">` block (the removed markup is left as a comment) and `public/site.webmanifest` with its icons array. |
| `velocit-ee/web/site/public/og-image.svg` | Add the glyph to the card, then re-rasterise `og-image.png` at 1200×630 with the webfonts loaded. |
| `velocit-ee/docs/mkdocs.yml` | Restore the `logo:` and `favicon:` theme keys (also left as a comment) and add the assets. |

Whatever it becomes, it has to work at 16px, in one colour, and hold still —
see the motion rule above.

## Surfaces and ownership

| Surface | Repo | Owner of the visual |
|---|---|---|
| Website | `velocit-ee/web` | Brand drives, no exceptions. |
| Docs site | `velocit-ee/docs` | Mirrors the website palette via `docs/assets/velocitee.css`. |
| GitHub org profile | `velocit-ee/.github` | Mirrors the website's tone. No marketing copy. |
| Engine READMEs | `velocit-ee/core` | Documentation tone. |
| Issue / PR templates | `velocit-ee/.github` | Plain. Voice in the description, not the visuals. |

## Pull request review checklist

When a change touches a public surface:

- [ ] Palette uses the tokens above. No new hex values without a discussion here.
- [ ] Sentence case headings.
- [ ] No invented logo. The identity is the wordmark until a real mark exists.
- [ ] No emoji, no MAAS comparison, no "revolutionary"-tier marketing terms.
- [ ] No animation beyond hover/focus.
- [ ] Every command shown is one that exists.
- [ ] Every engine status matches `engines.json`.
- [ ] No price appears anywhere.
- [ ] Legal links still present in the footer (`npm test` in `web/` checks this).

## Updates to this guide

This file is in the org-public `.github` repo, so changes to it are public.
Discuss in an issue first; a PR for a contested change should carry a
one-paragraph rationale.
