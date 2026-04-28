# velocit.ee — brand guide

Internal reference. Pin choices so the landing page, docs site, READMEs, and
any future surface stay coherent. Drift on any of these means a reviewer
should ask "is that intentional, or just a one-off?"

## Voice

- **Direct.** "VME provisions hardware." Not "VME aims to enable hardware
  provisioning workflows."
- **Lowercase headlines** are the default for marketing surfaces (landing
  page, GitHub org page). Documentation uses sentence-case (`# Getting
  started`, not `# getting started`) for readability.
- **No marketing flourish.** "Open-core infrastructure deployment platform"
  is the tagline. Don't reach for "revolutionary" / "cutting-edge" / "next
  generation."
- **No emoji** in code, commits, or content. The skill list says rendering
  emoji is allowed when explicitly asked; it isn't asked here.
- **Never mention MAAS** (Canonical's Metal-as-a-Service) anywhere. The
  comparison hurts more than it helps.

## Palette

Charcoal + blue + green. Two layers — a base background palette (charcoal
shades) and a foreground accent palette (blue for action, green for success,
cyan for info). Both are pinned as CSS variables on every public surface
(`--v-*` prefix).

| Token            | Hex      | Used for |
|------------------|----------|----------|
| `--v-bg`         | `#0d0d10`| Page background — pure near-black charcoal, no green tint. |
| `--v-surface`    | `#141418`| Cards, mac-window body, code blocks. |
| `--v-surface2`   | `#1c1c22`| Mac-window titlebar, status bar, elevated surface. |
| `--v-surface3`   | `#222228`| Mac-window statusbar, deepest surface. |
| `--v-border`     | `#2a2a35`| Hairlines, dividers. |
| `--v-border-hi`  | `#383848`| Hover state borders, pipeline node default. |
| `--v-blue`       | `#3b82f6`| Primary accent — CTAs, active states, data streams. |
| `--v-blue-hi`    | `#60a5fa`| Hover on blue, prompt `$`, accent links, logo `v`. |
| `--v-blue-lo`    | `#1d4ed8`| Pipeline gradient anchor. |
| `--v-green`      | `#22c55e`| Success, verification PASS, `.ee` underline. |
| `--v-green-hi`   | `#4ade80`| Hover on green, ✓ markers, hero "velocity" word. |
| `--v-cyan`       | `#22d3ee`| Info ▶, secondary data signals. |
| `--v-cream`      | `#e8eaf0`| Primary heading color. |
| `--v-text`       | `#c8cdd8`| Body text on dark. |
| `--v-muted`      | `#6b7280`| Secondary text. |
| `--v-dim`        | `#3d4149`| Tertiary text, borders, dim metadata in logs. |

The blues drive *primary action*. The greens drive *success / go signals*.
The cyan is purely informational. Don't swap them.

## Type

- **Headings, body, UI, navigation, buttons:** Space Grotesk (500, 600, 700).
- **Terminals, status bars, code, badges, eyebrows:** JetBrains Mono (400, 500, 600).
- Self-hosted via `@fontsource/space-grotesk` and `@fontsource/jetbrains-mono` on
  the landing site. Docs site loads the same families through MkDocs Material's
  Google Fonts integration.
- **Letter-spacing** on headings: `-0.02em` to `-0.03em`. Tight without being
  cramped.
- **No icon fonts.** SVG-only.

## Brand mark

In header chrome: `v` (blue-hi) + green caret block + `.ee` (green-hi with
animated underline). Inline body marks use a single `v` with a blue caret + `e`.
SVG sources live at:

- `velocit-ee/web/site/public/favicon.svg` — landing-site favicon
- `velocit-ee/docs/docs/assets/favicon.svg` — docs site
- `velocit-ee/docs/docs/assets/logo.svg` — docs header (uses `currentColor`
  so it inherits the chrome's text colour; only the caret is fixed blue)

Don't redraw it. If a new surface needs the mark, copy one of the above.

## Naming

| Surface                    | Form |
|----------------------------|------|
| Domain                     | `velocit.ee` (always lowercase) |
| Org                        | `velocit-ee` (hyphenated; required by GitHub) |
| Project family             | "velocitee" — one word, lowercase |
| Engines                    | `VME`, `VNE`, `VSE`, `VLE` (all caps when standalone) |
| Engines in prose           | "VME — metal", "VNE — network" — name + dash + role |

The four engines map to phases 1–4 of the pipeline. Don't number them
inline ("phase 2 engine") in marketing copy; use the role description.

## Surfaces and ownership

| Surface                  | Repo                  | Owner of the visual    |
|--------------------------|-----------------------|------------------------|
| Landing page             | `velocit-ee/web`      | Brand drives, no exceptions. |
| Docs site                | `velocit-ee/docs`     | Mirrors landing palette via `docs/assets/velocitee.css`. |
| GitHub org profile       | `velocit-ee/.github`  | Mirrors landing tone, no marketing copy. |
| Engine READMEs           | `velocit-ee/core`     | Documentation tone — sentence-case headings. |
| Issue / PR templates     | `velocit-ee/.github`  | Plain. Brand voice in description, not visuals. |

## Pull request review checklist

When changes touch a public surface:

- [ ] Palette uses the tokens above; no new hex values without a vote here.
- [ ] Heading hierarchy follows surface convention (lowercase marketing /
      sentence-case docs).
- [ ] Mark used is one of the SVG sources, not a redraw.
- [ ] No emoji, no MAAS reference, no "revolutionary"-tier marketing terms.

## Updates to this guide

This file is part of the org-public `.github` repo, so changes to it are
public. Discuss in an issue first; PRs to merge a contested change should
include a one-paragraph rationale.
