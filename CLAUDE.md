# 🤖 CLAUDE.md

Working notes for anyone (human or agent) changing this repo.

## What this is

The website for **Cribado** — a family of self-hosted report sieves:
**Cribado-CSP** (CSP-violation reports; v1 in progress) and
**Cribado-DMARC** (DMARC aggregate reports; on its way — runs locally,
not yet deployed). The site is three static pages — `index.html` (the
family), `csp/index.html`, `dmarc/index.html` — each self-contained with
its own inline `<style>`: no build step, no dependencies, no JavaScript,
no shared CSS file. Keep it that way; a product whose family motto is
"lightweight, no build step" does not get to ship a bundler on its own
homepage. A style change means editing all three `<style>` blocks — the
duplication is the price of self-contained pages, paid knowingly.

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
- **The marks** (2026-08-04): three white dots over three dashes over one
  dot, on a rounded square. Dot rhythm and field colour identify the app:
  Cribado level on brown `#a1580a` (`favicon.svg`), Cribado-CSP
  high-low-high on gold `#b39205` (`csp/favicon.svg`), Cribado-DMARC
  low-high-low on red `#a0410f` (`dmarc/favicon.svg`). **This repo is the
  source of truth**; the app repos carry copies at
  `internal/web/static/favicon.svg` — change here first, then re-copy.

## Accuracy rules (these matter more than the prose)

- **Both app repos are private** (`cribado/cribado-csp` and
  `cribado/cribado-dmarc` on GitHub). Never link to them from the site;
  the links would 404 for every visitor. The pages say the source is
  unpublished and the licence pending — update both when publication
  actually lands.
- **Cribado-DMARC is real but young** (as of 2026-08-04: runs locally,
  not yet deployed — "on its way"). Its page must keep saying so until a
  deployment exists. Its honest limits stay on the page: aggregate
  (`rua`) reports only, never forensic (`ruf`); v1 receives mail through
  a Mailgun inbound route (built-in SMTP is deferred, with the trigger
  written down in that repo).
- **The server-trust deviation must stay stated in the open.** Cribado's
  operators can read every report it stores — a deliberate departure
  from the CARLOS default of server-blindness, justified in Cribado-CSP's
  `CLAUDE.md` ("The one rule"). The site must never claim or imply
  end-to-end encryption, and must never quietly drop the trade-off
  section.
- **Don't overclaim maturity.** Cribado-CSP v1 is in progress: ingest and
  dashboard run, deployment is the current work. Update the Status
  section when reality changes, not before.
- **Don't name competitors** — report-uri.com references were removed
  2026-08-04 ("used as a prompt to build this, not needed in our
  marketing"). The Cribado-CSP repo's own docs still mention it; don't
  let it creep back in when syncing copy from there. The CSP *directive*
  `report-uri` is protocol vocabulary and stays.
- **Never reference Tito on the site or in this repo's prose** — no name,
  no link (decided 2026-08-03). Cribado stands on its own; "its makers"
  is as specific as the copy gets.
- **Naming** (rebranded 2026-08-04 from the earlier "Crispa"): the family
  is **Cribado**, titleized in prose — Spanish for sieving, from *criba*
  (sieve); the site states the etymology in the intro, keep it. App
  branding in prose is titleized with the protocol uppercased —
  **Cribado-CSP**, **Cribado-DMARC** — matching the apps' own UI (decided
  2026-08-04, replacing the earlier code-styled lowercase). Lowercase
  `cribado-csp`/`cribado-dmarc` survives only where it is a real
  identifier: repo names, checkout paths, binary and endpoint labels in
  code samples. Don't revert any of this in a drive-by edit.
- Every technical claim on the pages is traceable to the app repos'
  `README.md`, `CLAUDE.md`, and `DESIGN.md` (sibling checkouts at
  `../cribado-csp` and `../cribado-dmarc`). If you change a claim, check
  it against those — and ultimately the code — rather than against the
  previous copy.

## Deploying

**The live site, [cribado.report](https://cribado.report), runs on the
CARLOS platform** (the Tito deployment, console `carlos.tito.io`) as a
`-kind static` app — cut over 2026-08-04. Publishing a change is the
standard sequence, run from this repo with a clean tree:

```
carlos ship    -account bad -app cribado -kind static -version <sha> .
carlos promote -account bad -app cribado <sha> canary/rehearsal
```

The `cribado.report` route follows `canary/rehearsal` (same reasoning as
the CARLOS site's own cutover: `stable` bakes 72h on a box's first
sighting of a channel head, which would have meant 72h of downtime for a
never-before-served route; a later `stable` flip is optional cleanup).
The route was added once, by an operator on the edge box — `ship` and
`promote` speak the console API, but route management is box-side
(`sudo -u carlos /opt/carlos/carlos add …` over SSM; see
`../cribado-csp/docs/2026-08-03-deploy-design.md` for box access). DNS:
`cribado.report` apex A → `54.228.234.85` (the Tito edge — **not**
`99.81.104.219`, which is the flagship edge; no AAAA) in DNSimple.

**GitHub Pages is switched off** (2026-08-04; it briefly hosted the site
2026-08-03 → 2026-08-04, and never served `cribado.report`). `.nojekyll`
stays in the repo so re-enabling Pages remains a two-minute fallback if
the platform is ever unavailable: enable Pages from `main` (root), add
the custom domain in the repo settings, and point DNS at GitHub's Pages
addresses.
