# Working agreement for coding agents

Read these first, in order:
1. [README.md](README.md)
2. [docs/PROJECT_PLAN.md](docs/PROJECT_PLAN.md)
3. [docs/CHALLENGE_DESIGN.md](docs/CHALLENGE_DESIGN.md)
4. [docs/VALIDATION.md](docs/VALIDATION.md)

## Current state

This repository begins as a **plan-first project**. Do not describe unbuilt features, tests, published evidence, or user outcomes as already completed. These documents are meant to remain useful without a timeline.

## Non-negotiable product rules

- The product is **Spot the Edit + Verify**, a Bangla-first bilingual fictional media-literacy game.
- Preserve the loop: feed -> first judgment -> optional investigation -> evidence-based conclusion -> truthful action replay.
- Treat **publisher attribution** separately from **underlying claim truth**. A missing record in a *complete fictional archive* can refute fictional outlet attribution, not establish every real-world claim false.
- Keep source exploration **optional**, so "checked before concluding" remains an observable behavior.
- Use four classes: edited photo, altered quote, clean fabrication, genuine. Clean fabrications must be visually pristine.
- Render genuine and fabricated items for each invented outlet with **identical** branding, fonts and template assets.
- Never use real outlet impersonations, political public figures, real false claims or unmarked training cards. Keep a persistent training/simulation watermark on all artifacts.
- Scoring must use deterministic ground truth, not free-form model guesses.
- Preserve A/B held-out set separation and do not leak answers during evaluation.
- Protect privacy: no mandatory login or collection of identifying data.

## Scope and technical priorities

Aim for a robust static web app, versioned JSON content, SVG/HTML card templates, inspectable simulated evidence pages, mobile-first UX, Bangla/English, replay and anonymous copy/export. Prefer a reliable complete core loop over speculative integrations.

Do not add accounts, live social scraping, arbitrary news authentication, leaderboards, a backend, or a model API requirement without explicit product-owner approval.

## Working method

- Before coding, check the official Devpost Learn Skill Pack process. These evergreen docs should inform the official `1-start` through `6-ship` steps, **not replace or preempt** generated `devpost/scope.md`, `devpost/prd.md`, or `devpost/spec.md`.
- Build incrementally and test functionality and correctness, especially evidence mapping, replay integrity, regional masks, and localization.
- Keep content rights, fictional-world consistency, and challenge answer keys reviewable.
- Document significant product changes by updating the evergreen docs; never quietly rewrite the learning objective.
- Do not manufacture user-test outcomes or efficacy claims. The project owner writes their own Devpost submission text; agents may help check grammar and completeness.
- Do not insert a calendar timeline into these permanent planning documents unless explicitly requested.
