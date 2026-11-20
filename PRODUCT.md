# Product

<!-- impeccable:product-schema 1 -->

## Platform

web

## Users

Primary visitor is a recruiter or hiring-manager type reviewer, scanning quickly to judge fit for a security-engineering role. They land on the page to decide, in a short read, whether this person's experience and demonstrated work match what they're hiring for.

## Product Purpose

A personal portfolio site for 이인직, a Service / Enterprise(In-house) Security Engineer. It exists to let a time-pressed reviewer quickly see who he is, what he's built, and how he works, in support of job search and hiring evaluation.

## Positioning

The differentiator versus other security-engineer portfolios: he's positioned as a **builder, not just an operator**. Rather than only describing policy-operations duties, the site foregrounds actual tooling he designed and built (e.g. the FortiGate policy-automation tool, "FSPM") that removed repetitive manual work, plus concrete AI tools he has put into real use in his security work.

## Operating Context

Enterprise in-house and service-facing security operations: firewall/security policy management, security review/hardening, and incident/change-history tracking are the kind of work his built tooling automates. Content is maintained through a browser-based `/admin` editor that commits directly to the GitHub repo backing the site (via the GitHub Contents API) — there is no separate CMS or build step.

## Capabilities and Constraints

- Static site, no framework: plain HTML/CSS/JS, content driven by `public/content/content.json` and rendered by `public/assets/js/main.js`.
- Current surfaces: a centered profile header (photo, name, one-line role) followed by tab-style sections — About Me, Project, AI Utilization — where only one section is visible at a time (About Me by default) because the Project/AI Utilization tabs will carry many screenshots.
- Deployed as a **public** GitHub Pages repo via a GitHub Actions workflow (`.github/workflows/pages.yml`) that publishes `public/`.
- Hard constraint: this repo is public, so raw/unprocessed screenshots must never be committed. The original screenshot source (`img_src/`) stays local only (gitignored); only manually cropped/sanitized screenshots may be uploaded through `/admin` into `public/assets/img/...`.

## Evidence on Hand

- FSPM (FortiGate policy-automation tool): real internal screenshots exist locally under `img_src/pf/1. FSPM/` (dashboard/policy lookup, policy/object creation, security review & optimization, change history/request & remediation/audit log/env settings). These are not yet sanitized or published; `public/assets/img/aiskill/placeholder.svg` is the current placeholder until cropped versions are uploaded.
- `public/content/content.json`'s About fields (birth, address, email, education, company, one-line bio) and the Project (changelog) entries are currently empty/unfilled — real content is still pending.

## Product Principles

- Lead with built tooling, not job duties — every claim should point at something he actually made, not a task he merely performed.
- Never publish a claim or metric that isn't backed by real tooling/screenshots on hand; no fabricated testimonials, numbers, or employers.
- Protect the employer's security posture: no internal IPs, system names, or other infra specifics ever reach the public repo or site.
- Optimize for a reviewer skimming in under a minute — lead with the one-line identity, let deeper proof (Project, AI Utilization) stay one click away rather than up front.
