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

The terminal aesthetic. Two layers — a base background palette and a
foreground accent palette. Both are pinned in CSS variables on every surface
that uses them.

| Token            | Hex      | Used for |
|------------------|----------|----------|
| `--bg`           | `#0b0e09`| Page background. |
| `--surface`      | `#111510`| Cards, terminal tiles, code blocks. |
| `--surface2`     | `#171d15`| Hover state, inset surfaces. |
| `--border`       | `#232d1f`| Hairlines, dividers. |
| `--green`        | `#5a9e6a`| Primary actions, links. |
| `--green-hi`     | `#7dc48a`| Hover, callouts, highlight prose. |
| `--brown`        | `#9b7a4e`| Secondary accent — section labels. |
| `--brown-hi`     | `#c4a06a`| Highlight on dark surfaces (warm). |
| `--cream`        | `#d4ccb4`| Headings, primary text on dark. |
| `--text`         | `#b8c4a8`| Body text on dark. |
| `--muted`        | `#5e7055`| Secondary text. |
| `--dim`          | `#3a4a34`| Tertiary text, borders. |

The greens drive *action*. The browns drive *attention but not action*. Don't
swap them.

## Type

- **Headings & UI:** IBM Plex Mono (300, 400, 500, 600).
- **Body prose:** IBM Plex Sans (300, 400, 500). Used in long-form copy
  (description paragraphs, doc body); never in headings.
- Loaded via Google Fonts on every public surface. No self-hosting yet.
- **Letter-spacing** on headings: `-0.02em` to `-0.04em`. Tight, terminal feel.
- **No icon fonts.** SVG-only.

## Brand mark

`v` + green caret block + `e` — terminal cursor between two letters. SVG
sources live at:

- `velocit-ee/web/public/favicon.svg` — landing page
- `velocit-ee/docs/docs/assets/favicon.svg` — docs site
- `velocit-ee/docs/docs/assets/logo.svg` — docs header (uses `currentColor`
  so it inherits the chrome's text colour; only the caret is fixed green)

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
