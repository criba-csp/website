# 🤖 CLAUDE.md

Working notes for anyone (human or agent) changing this repo.

## What this is

The website for **Cribado** — a family of self-hosted report sieves.
Today that means **cribado-csp**, a CSP-violation reporting endpoint and
analytics tool (a [report-uri.com](https://report-uri.com) alternative
run in-house); **cribado-dmarc** (DMARC aggregate reports) is planned and
not yet built. The site is a single static `index.html`: no build step,
no dependencies, no JavaScript. Keep it that way; a product whose family
motto is "lightweight, no build step" does not get to ship a bundler on
its own homepage.

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
  hairline rules, an italic epigraph under each `h2`. Cribado's accent is
  **amber** (`#a1580a` light, `#e3a457` dark) — a warning colour for a
  warnings tool — so the family sites are visibly siblings and not the
  same site.

## Accuracy rules (these matter more than the prose)

- **The cribado-csp source repo is private** (`cribado/cribado-csp` on
  GitHub). Never link to it from the site; the link would 404 for every
  visitor. The page says the source is unpublished and the licence
  pending — update both when publication actually lands.
- **cribado-dmarc does not exist yet** (as of 2026-08-04). The site names
  it to show the family's shape, and says "not yet built" in the same
  breath. Never add claims about it beyond intent until there is code to
  trace them to.
- **The server-trust deviation must stay stated in the open.** Cribado's
  operators can read every report it stores — a deliberate departure
  from the CARLOS default of server-blindness, justified in cribado-csp's
  `CLAUDE.md` ("The one rule"). The site must never claim or imply
  end-to-end encryption, and must never quietly drop the trade-off
  section.
- **Don't overclaim maturity.** cribado-csp v1 is in progress: ingest and
  dashboard run, deployment is the current work. Update the Status
  section when reality changes, not before.
- **Never reference Tito on the site or in this repo's prose** — no name,
  no link (decided 2026-08-03). Cribado stands on its own; "its makers"
  is as specific as the copy gets.
- **Naming** (rebranded 2026-08-04 from the earlier "Crispa"): the family
  is **Cribado**, titleized in prose — Spanish for sieving, from *criba*
  (sieve); the site states the etymology in the intro, keep it. Apps are
  lowercase and hyphenated, styled as code: `cribado-csp`,
  `cribado-dmarc`. Don't revert any of this in a drive-by edit.
- Every technical claim on the page is traceable to the cribado-csp
  repo's `README.md`, `CLAUDE.md`, and `DESIGN.md` (sibling checkout at
  `../cribado-csp`). If you change a claim, check it against those — and
  ultimately the code — rather than against the previous copy.

## Deploying

**GitHub Pages, for now** — enabled 2026-08-03, serving `main` (root);
pushing to `main` publishes, and `.nojekyll` is in place. The likely
eventual path is the same as the CARLOS site's: ship as a `-kind static`
app on `carlosframework/platform` (`carlos ship` / `promote` / `add`),
with Pages kept as the fallback.
