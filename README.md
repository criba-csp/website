# 🤖 Cribado — the website

The public website for **Cribado**, a family of self-hosted report
sieves: small tools that store, deduplicate and watch the reports your
systems send back. The name is *cribado* — Spanish for sieving, the work
of a *criba*. The apps: **Cribado-CSP**, a CSP-violation reporting
endpoint and analytics tool we run ourselves, and **Cribado-DMARC**,
its DMARC aggregate-report sibling — on its way, not yet deployed.

The site is three static pages: [`index.html`](index.html) for the
family, [`csp/`](csp/index.html) and [`dmarc/`](dmarc/index.html) for
the apps. No build step, no dependencies, no JavaScript. Cribado apps
are [CARLOS](https://carlosframework.com) applications, and the family's
rules apply to the website too.

## Authorship: the 🤖 rule

Everything in this repo written by an AI carries a **visible 🤖 marker** —
on the page, in this README, at the top of every prose file. That is
factor X applied to the project itself: AI-written words are always
disclosed, never passed off as human. The full rule (including the
human-certification markers that AI must not touch) is in
[`CLAUDE.md`](CLAUDE.md).

## Provenance

Written by an LLM (Claude), on the ideas, instruction, and editing of
humans. The claims on the page are traceable to the Cribado-CSP repo's
`README.md`, `CLAUDE.md` and `DESIGN.md`.

## Licence

To be decided alongside Cribado-CSP's own — open source is the family
default; not optional, only deferred.
