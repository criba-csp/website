# 🤖 CLAUDE.md

Working notes for anyone (human or agent) changing this repo.

## What this is

The website for **crispa** — Tito's self-hosted CSP-violation reporting
endpoint and analytics tool, a [report-uri.com](https://report-uri.com)
alternative run in-house. The site is a single static `index.html`: no
build step, no dependencies, no JavaScript. Keep it that way; a product
whose family motto is "lightweight, no build step" does not get to ship a
bundler on its own homepage.

## The one rule: AI authorship is always marked (🤖 / 👨)

This repo practices factor X on itself. Every piece of prose carries an
authorship marker so a reader — human or agent — can tell who wrote what,
and so a human can fence text off from AI rewriting.

- **🤖 — written by an LLM.** Always **visible**, immediately before the
  heading, paragraph, or section it applies to. A 🤖 on a heading
  **cascades**: it marks that heading and everything beneath it, down to
  the next marker of the same-or-higher level or a human-certified block.
  One 🤖 on a document's top heading marks the whole document. On the
  website, the marker must render visibly on the page — never hide it in a
  comment.
- **No marker — ambiguous.** Could be either. Never *assume* AI
  authorship; when you genuinely don't know, leave it unmarked.
- **A person emoji (👨 / 👤 / 🧑 …) — certified human, off-limits.** The
  text was written or vetted by a person. **An LLM must not rewrite,
  rephrase, condense, or delete it.** You may add new 🤖 prose nearby, but
  the human's words are fixed. In HTML/Markdown the person marker may hide
  in a comment (`<!-- 👨 -->`) so it doesn't render; the 🤖 marker must
  **never** be hidden.

Baseline: **everything in this repo was AI-written unless a block carries
a person marker.**

## Conventions

- **One page, zero dependencies.** No frameworks, no fonts fetched from
  anywhere, no analytics, no JavaScript.
- **Light and dark** via `prefers-color-scheme` — keep both working when
  touching styles.
- **House style is inherited from [11factor](https://11factor.org)** via
  the [CARLOS site](https://carlosframework.com): Charter/Georgia serif, a
  single accent colour, `--max: 42rem` measure, sections separated by
  hairline rules, an italic epigraph under each `h2`. crispa's accent is
  **amber** (`#a1580a` light, `#e3a457` dark) — a warning colour for a
  warnings tool — so the family sites are visibly siblings and not the
  same site.

## Accuracy rules (these matter more than the prose)

- **The crispa source repo is not yet published.** Never link to it from
  the site; the link would 404 for every visitor. The page says the source
  is unpublished and the licence pending — update both when publication
  actually lands.
- **The server-trust deviation must stay stated in the open.** crispa's
  operators can read every violation it stores — a deliberate departure
  from the CARLOS default of server-blindness, justified in crispa's
  `CLAUDE.md` ("The one rule"). The site must never claim or imply
  end-to-end encryption, and must never quietly drop the trade-off
  section.
- **Don't overclaim maturity.** v1 is in progress: ingest and dashboard
  run, deployment is the current work. Update the Status section when
  reality changes, not before.
- **The name is crispa, lowercase**, styled that way even at the start of
  a sentence.
- Every technical claim on the page is traceable to the crispa repo's
  `README.md`, `CLAUDE.md`, and `DESIGN.md` (sibling checkout at
  `../crispa`). If you change a claim, check it against those — and
  ultimately the code — rather than against the previous copy.

## Deploying

Not yet wired up. The likely path is the same as the CARLOS site's: ship
as a `-kind static` app on `carlosframework/platform`
(`carlos ship` / `promote` / `add`). `.nojekyll` is in place in case
GitHub Pages is used as an interim or fallback host.
