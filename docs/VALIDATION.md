# Validation, evaluation, and quality plan

## Purpose

Determine whether Spot the Edit + Verify is understandable, technically reliable, and *plausibly useful* for evidence-based verification. The pilot is exploratory, not a clinical or population-scale effectiveness trial.

## 1. Prototype gate (four challenges, three unfamiliar players)

Prepare one fully clickable item of each type: edited photo, altered quote, clean fabrication, and genuine card. Include a mock publisher archive, a separate source, first impression, optional investigation, conclusion, and replay.

Have **three people who have not seen the content** attempt the experience. Avoid coaching them through individual choices; observe confusion and spontaneous checking.

**Go:** all three complete the loop and, when asked about the clean fabricated item, can point to the fictional publisher archive/evidence as their reason for disputing its claimed attribution.

**Redesign the investigation step:** if participants continue to treat it as only a real/fake image quiz and routinely skip investigation even after seeing how the first reveal works.

**Difficulty tuning, not a kill condition:** track how many open the publisher archive *before* teaching/reveal. If everyone checks unprompted, the initial set may be too easy or the sample may already have the target skill. Adjust content or recruit a more representative group; do not artificially require participants to make mistakes.

Record concrete blockers and quotes, not only pass/fail judgments.

## 2. Structured exploratory pilot

Target **10 independent testers**; report how many actually participate. Each person completes a held-out pretest, training, and a different held-out post-test.

- Five participants: **A -> training -> B**.
- Five participants: **B -> training -> A**.
- Each held-out set has four questions (one for each card type) in matched A/B pairs.
- Pre/post questions offer the **same unforced investigation tools** and no feedback or hints until the assessment stage is over.
- Training uses 12 different cards with explanatory feedback.
- Held-out cards are **never** reused as examples or practice.
- Run basic usability tests on additional unfamiliar users before relying on a large pilot.
- Do not pressure users to reach a specific conclusion or open a source; the choice to investigate is the behavior being observed.

Pairs are matched in card type, evidence depth, clue visibility, typography, and cognitive load, but matching does not eliminate all set effects or the practice effect of taking the pretest.

## 3. Metrics and denominators

Report **raw counts, denominators, and pre/post differences**; do not present a single blended "truth detection" score.

| Metric | Definition | Important distinction |
| --- | --- | --- |
| Visual detection | Correctly marked intended edit region / eligible *edited photo or quote* items | Not applicable to clean fabrication or genuine cards; define tap tolerance |
| Verification correctness | Correct **final conclusion plus deciding evidence** / all scorable items | Also report verdict-only accuracy so readers understand failure modes |
| False alarms (genuine cards) | Genuine items incorrectly concluded unsupported / all genuine items | Report initial suspicion separately if useful |
| Checked before concluding | Items where an archive or independent-source view occurred before final submission / all items | Report archive checks and independent-source checks separately |
| Appropriate uncertainty | Items where insufficient evidence was warranted and selected / eligible items | Include only if such items actually exist in content |
| Completion | People who finish the full loop / people who start | Also record reported confusion and unavailable controls |

A source-open event is **not** proof that the participant read or understood the evidence. Interpret behavior conservatively. Opening the archive after concluding must not count as "checked before concluding."

Store both per-item logs and anonymized participant-level summaries to avoid treating forty observations as forty independent participants.

## 4. Evidence scoring rules

- Each challenge has a clearly authored question, correct conclusion, and evidence IDs that truly justify it.
- In assessment, the player selects a conclusion and the deciding evidence from what is available; do not force the player to have visited a particular source.
- A final answer is fully correct only if the conclusion **and** deciding evidence are correct. Allow a valid "not enough evidence" choice where appropriate.
- Visual edit masks are separate from final-conclusion scoring; the ability to tap a changed region does not prove a card or story false.
- For genuine cards, don't reward blanket suspicion; measure how often a player incorrectly rejects valid evidence.
- In training, useful hints/explanations are allowed after submission, but no answer leakage into held-out evaluation.
- The replay must show only actions actually taken. Never invent steps for a tidy educational story.
- The implementation must handle missed taps, repeated source opening, answer changes, and incomplete sessions consistently.

## 5. Pilot collection and reporting

Prefer a **local results screen with an explicit "Copy results" / export button**. Participants can paste an anonymized output into a collection form; the game does not need a backend.

Export includes:
- anonymized participant/session ID and A-first/B-first assignment;
- per-item challenge ID, initial choice, visited evidence IDs and event order, optional region hit, final verdict, evidence selection and correctness;
- summarized raw counts with denominators, not just percentages;
- app/content version and optional non-identifying usability notes.

Do **not** collect names, precise locations, employer/political data, third-party social accounts, or real browsing history. Seek participant consent for using their anonymous pilot data in the project write-up.

### What the write-up may claim

- "In a small, counterbalanced pilot of N volunteers, X/Y answers included the correct conclusion and supporting evidence before training and A/B afterward" (using actual observed numbers).
- "Players opened a source before concluding on X/Y items" (if actually logged).
- "Participants reported these specific usability blockers" (if observed).

Do **not** claim population-level efficacy, causal proof from a tiny sample, or that the game authenticates arbitrary news content.

## 6. QA / test checklist

### Game logic

- [ ] Correct first-judgment, investigate, conclude and replay state transitions.
- [ ] A source check is optional; the player can conclude without it.
- [ ] Archive evidence and independent evidence have distinguishable IDs and labels.
- [ ] Scoring is deterministic with unit tests for correct/incorrect verdict, evidence, and mask taps.
- [ ] All four types handle applicable/missing original image and mask correctly.
- [ ] Replay action order matches original events; timestamps don't reorder events.
- [ ] Pre/post has no training feedback or accidental answer-key leaks.

### Content integrity

- [ ] Invented outlets, people, events and permanent training watermark.
- [ ] Same logo, fonts and template files for genuine/fabricated cards of an outlet.
- [ ] Simulated archive actually satisfies its stated completeness contract.
- [ ] Each answer explanation follows from accessible original/archive/source pages.
- [ ] Unedited and edited variants differ only inside allowed mask when pixel compositing is used.
- [ ] Paired held-out sets pass a difficulty and ambiguity review.
- [ ] All assets have appropriate usage rights.

### Experience and accessibility

- [ ] Bangla/English toggle preserves semantics and doesn't reset an active session unexpectedly.
- [ ] Photocard text can be zoomed on small phones; touch targets are usable.
- [ ] Keyboard navigation, focus state, screen-reader labels and non-color-only feedback.
- [ ] "Supported" vs "published by the outlet" distinction is explained consistently.
- [ ] Error/empty states, reload and restart are graceful.
- [ ] Static build loads all content and assets without account, GPU, API key or backend.

### External-review readiness

- [ ] A stranger understands the learning promise in the first screen.
- [ ] A clean fabricated card does not contain a hidden "fake-looking" branding clue.
- [ ] The demo shows initial belief -> checks -> revised conclusion -> replay.
- [ ] Scores and pilot data shown publicly are accurate and qualified.
- [ ] Required official Skill Pack artifacts and submission materials are handled in their own workflow.
