---
name: frontend-style
description: Arthur's house style for lightweight front-ends. Use whenever building or styling any web UI — pages, artifacts, prototypes, dashboards, static sites — so output uses his palette and design motifs instead of generic AI defaults. Triggers on "make a page/site/UI", "style this", "use my colors/house style".
---

# Frontend Style

House rules for any web UI built for Arthur. Read `palette.css` in this skill's directory for the tokens; the sections marked **CUSTOMIZE** below are Arthur's to edit — always honor their current contents over your own taste.

## Palette (source: Dropbox/Apps/arthur-grau-palette.scss)

| Token | Hex | Role |
|---|---|---|
| `--scarlet-rush` | `#db2b39` | Accent: CTAs, active states, alerts. Use sparingly. |
| `--dusk-blue` | `#304d6d` | Primary: headers, nav, buttons, links |
| `--dim-grey` | `#6b6b6b` | Secondary text, borders, muted UI |
| `--sky-reflection` | `#7eb2dd` | Highlights, hover states, info surfaces |
| `--sage-green` | `#6cae75` | Success, positive metrics, confirmations |

Neutrals: derive backgrounds from near-white (`#fafaf8`) and near-black (`#1d2126`) — never pure `#fff`/`#000` for large surfaces. Dark mode: `--dusk-blue` shifts to background duty, `--sky-reflection` takes over as primary, keep `--scarlet-rush` as accent.

Link the palette by copying the `:root` block from `palette.css` into the page — artifacts and one-off pages must be self-contained, so inline it, don't reference the file.

## Design motifs — **CUSTOMIZE**

<!-- Arthur: edit this list freely; Claude follows whatever is written here. -->

- Generous whitespace; content column max ~68ch for reading, wider for tables/dashboards.
- Type: system font stack (`-apple-system, 'Segoe UI', sans-serif`); one family, weight does the hierarchy work. No decorative webfonts.
- Flat surfaces with 1px borders in `--dim-grey` at low opacity; shadows only for true overlays (menus, modals).
- Corners: 6px radius on interactive elements, 0 on structural containers.
- Motion: 150ms ease-out on hover/focus only. No entrance animations, no parallax.
- The five-color gradient from the palette file may appear once per page at most, as a thin (~4px) accent bar — never as a background.

## Defaults

- Plain HTML + CSS first; add vanilla JS only when interaction demands it. No framework, no build step, no CDN dependencies for anything lightweight.
- Semantic elements (`header`, `main`, `nav`, `button`) before divs; visible focus states; contrast ≥ 4.5:1 for text (note: `--sky-reflection` and `--sage-green` fail on white — use them for fills and large graphics, not body text).
- Responsive via flexbox/grid and relative units; test the narrow case mentally before shipping.
- Support light and dark via `prefers-color-scheme`, using the dark-mode role swap above.
- Charts and data viz: defer to the dataviz skill, substituting this palette (dusk-blue as first categorical color, scarlet-rush reserved for emphasis).
