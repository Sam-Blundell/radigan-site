# Radigan's personal site — design notes

## Project status

- **Repo:** `radigan-site`
- **Local path:** `~/code/personal/radigan-site`
- **Friend's placeholder name:** Radigan (his screen name; real name to be filled in later)
- **Current state:** Hugo project scaffolded via `hugo new site` (standard directories present: `archetypes/`, `content/`, `layouts/`, `static/`, `assets/`, `data/`, `i18n/`, `themes/`, plus `hugo.toml`). No theme installed. No layouts written yet. No content yet.
- **Directory placement plan:** lives in `~/code/personal/` while Sam is authoring it. Moves to `~/code/external/` after handoff (when GitHub repo ownership transfers to Radigan and Sam's local copy becomes a reference clone). See "Directory placement" section below.

## Context

A personal site for Radigan, a friend who has been meaning to put one together for a while but hasn't gotten around to it. Sam is offering to do the technical setup so Radigan can focus on writing content.

**About Radigan (relevant to design decisions):**

- Studied mechatronics; works in industrial automation
- Most comfortable language is C; learning some others but not web
- No prior web development experience
- Works on a Windows machine
- Likes simple things, similar instinct to my own site
- Interested in industrial design; fan of Death Stranding

## Approach

**Hugo, set up by Sam, deployed via Cloudflare Pages.**

Reasoning:

- Radigan won't want to hand-edit shared markup (nav/footer) across multiple HTML files, so we need *some* form of templating.
- A Makefile/bash build script would be the most spiritually C-flavored option, but doesn't work cleanly on Windows.
- A runtime JS include would be the simplest zero-build option, but caps the site's long-term ceiling and adds a JS dependency.
- Hugo's learning curve is the main objection, but **Sam is absorbing it on Radigan's behalf** by doing the setup. Radigan's day-to-day reduces to "edit markdown, `git push`, Cloudflare rebuilds." He never has to touch a template.
- Cloudflare Pages runs Hugo on their build infra, so Radigan doesn't even need Hugo installed locally (optional if he wants preview).

**Tradeoffs accepted:**

- Bus factor: Radigan won't fully understand the layouts. If something breaks he'll need help or have to learn Hugo himself. Low risk for a static personal site.
- Sam is somewhat on the hook for ongoing maintenance.

## Layouts

**Written from scratch, not derived from a theme.**

Reasoning:

- The site is minimal enough that the total layout code is small (~5 files, ~150 lines).
- Stripping a theme down to the aesthetic we want usually takes longer than writing from scratch — most Hugo themes assume blogs with heavy ornamentation.
- Writing from scratch forces Sam to learn Hugo properly rather than absorbing it through someone else's idioms.
- Output stays lean — no surprise CSS, no JS we didn't write.

**Files to write:**

- `layouts/_default/baseof.html` — outer HTML shell (head, body, nav, footer)
- `layouts/_default/single.html` — individual content pages (about, now, CV...)
- `layouts/_default/list.html` — index pages (blog index, projects index)
- `layouts/index.html` — homepage specifically
- `layouts/partials/nav.html`, `layouts/partials/footer.html` — shared chunks pulled into `baseof.html`

No `theme = "..."` line in `hugo.toml`. Hugo uses project-root `layouts/` directly.

## Pages to scaffold

All enabled by default; Radigan removes what he doesn't want:

- Landing
- About
- Now
- CV
- Projects
- Blog
- Links

All content is placeholder text until he has time to swap it out.

## Aesthetic direction

**Direction: NASAcore / Cold War futurism / "operator manual" aesthetic.**

Going with first instinct and surprising Radigan with this. If he doesn't like it once he sees it, easy to change — Markdown content is portable, only the layouts and CSS would need rework.

Inspired by Radigan's interest in industrial design and Death Stranding. Reference points:

- Apollo guidance computer DSKY
- Military terminal UIs (1970-1990)
- Period IBM / Honeywell / Burroughs documentation
- Death Stranding HUD, BB pod readouts, chiral network UI

**Core visual ingredients:**

- Monospace typography (candidates: IBM Plex Mono, Berkeley Mono, JetBrains Mono, VT323, Space Mono)
- Severely limited palette — near-monochrome with one accent (amber CRT, NASA orange, signal green, hazard yellow — TBC)
- Hairline borders, sharp corners, never rounded
- ASCII-style decoration: corner brackets, dividers, box-drawing characters
- ALL-CAPS labels with technical designations (MODULE-A, SYS.04, REV-2)
- Status readouts, timestamps, version stamps shown prominently as design elements
- Grid layouts that feel like control panels or instrument clusters

**Framing examples:**

- CV → `[PERSONNEL FILE]`
- Now → `[CURRENT STATUS / LAST UPDATED: ...]`
- Links → `[EXTERNAL TRANSMISSIONS]`

**Design ethic:** still form-follows-function, no ornament for its own sake — just expressed through technical-document language rather than Swiss-modernist whitespace. The aesthetic should never get in the way of the content being legible.

## Directory placement

Lives in `~/code/personal/` during development. Moves to `~/code/external/` after handoff. Rationale:

- `~/code/personal/` = belongs to Sam. Fits while Sam is authoring the repo on his GitHub.
- `~/code/external/` = doesn't belong to Sam. Fits after handoff, when canonical ownership transfers to Radigan and Sam's local copy becomes a reference clone of Radigan's repo.

The directory move mirrors the real ownership transition.

**Handoff mechanics (for later, not now):**

- Transfer GitHub repo to Radigan's account (GitHub's "transfer repository" feature) OR have him fork/clone and archive Sam's copy.
- Re-point Cloudflare Pages at Radigan's repo, or have him set up his own Cloudflare account connected to his repo (cleaner long-term).
- `mv ~/code/personal/radigan-site ~/code/external/radigan-site` once handoff is complete.

## Deferred for later

- **Domain:** TBC. Sam will handle.
- **Local preview:** skipping for now. Radigan will just use the Cloudflare push-and-wait loop. Can walk him through installing Hugo on Windows later if he wants it.
- **Real content:** placeholders for everything; Radigan swaps them out when he has time.

## Notes to self

- I'm planning this to learn Hugo properly — useful tool for the future.
- Migration path is easy if any of these decisions need to change later (especially aesthetic). Markdown content is portable.
