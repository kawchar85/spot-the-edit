# Product plan — Spot the Edit + Verify

## 1. Product decision

**Promise:** Learn to investigate viral news cards instead of trusting what looks real.

**Format:** An accessible, mobile-first, Bangla-first game with an English interface option.

**Primary audience:** Bangladeshi students and young adults who encounter and share social-media news photocards.

**Secondary audience:** Educators and media-literacy facilitators who can use a short, self-contained exercise.

**Status:** Agreed product direction, to be verified through prototype usability and a small exploratory pilot. Do not present proposed learning improvements as measured results.

### Problem

A photocard may be an unmodified representation of a published report, a modified image/quotation falsely attributed to a publication, or a completely fabricated card with professionally consistent branding. Guessing from appearance alone can fail. Players should learn when to inspect a visual clue, when to consult source records, and when to reserve judgment.

### Learning outcomes

A successful player should be able to:

- Separate a **first visual impression** from an evidence-supported conclusion.
- Locate an altered region when one exists, without assuming every false attribution has visible alterations.
- Examine a claimed publisher's original publication and relevant independent evidence.
- Distinguish **the outlet actually published this** from **the underlying claim is established**.
- Choose "Insufficient evidence" rather than manufacture certainty.
- Explain which evidence mattered and why another clue was inconclusive.

## 2. The core interaction contract

1. **Feed.** Display a share-style photocard using a consistent fictional outlet template and a clearly visible `TRAINING / SIMULATION` mark.
2. **First judgment.** Ask: `Looks fine`, `Suspicious`, or `Can't tell yet`. Record this answer before evidence exploration. It is not the final verdict.
3. **Investigate.** The player may zoom and mark a suspicious area, open the outlet's simulated publication archive, inspect its original card or complete absence of a record, and open a distinct simulated independent source. Log meaningful actions, not invasive tracking.
4. **Conclusion.** Choose `Supported`, `Not supported`, or `Insufficient evidence`; identify the deciding evidence (or lack of sufficient evidence). Never collapse attribution and claim truth.
5. **Replay and feedback.** Show the initial belief, checks actually made, submitted conclusion, ground truth with citations to *in-game* evidence, and a short transferable verification lesson.

**Investigation is optional before concluding**, especially in assessment rounds. Do not gate the conclusion button behind an archive visit: checking behavior must be observed rather than forced.

### Interpretation of conclusions

Each challenge explicitly states the question being evaluated (for example, "Does this card accurately represent what this publisher posted?"). The final label applies to that defined question:

- **Supported:** the scenario's evidence supports the precise question as framed.
- **Not supported:** the evidence positively contradicts the represented attribution or claim.
- **Insufficient evidence:** available evidence cannot justify either conclusion.

A complete **fictional training archive** can establish whether a fictional publisher published a card in the simulated world. Outside the simulation, absence from a real publisher's website alone cannot prove a claim false; corroborate with a second source.

## 3. Four challenge types

| Type | Card shown in feed | In-game publisher archive | Key educational lesson |
| --- | --- | --- | --- |
| Edited photo | A published-style card with a localized visual alteration | Unedited original | Compare primary source imagery; a changed region may distort meaning |
| Altered quote | A genuine card whose quotation has been replaced or modified | Original quotation/card | Attribution requires matching the original words |
| Clean fabrication | Entirely new card using a faithful outlet template | No such publication in the declared complete simulation archive | Absence of visual defects does not establish authenticity |
| Genuine | Faithful reproduction of a published fictional card | Matching original publication | Avoid false alarms; evidence can support authenticity |

When an independent source says something about the *underlying claim*, it must not be silently used as proof of what the named outlet published.

## 4. Product surfaces

- **Welcome / instruction:** short statement of the task and limitations; no lengthy tutorial before the first decision.
- **Feed / card viewer:** clear type, responsive media, zoom/pan, visible simulation watermark, optional tap-to-mark.
- **Investigation workspace:** accessible fictional outlet archive with inspectable records; separate independent source; no hidden "correct" cues in branding.
- **Conclusion:** verdict plus evidence selection and option to express uncertainty; concise confidence-neutral wording.
- **Replay:** ordered list of recorded actions, first impression vs conclusion, evidence that supports/counters it, and transferable lesson.
- **Session summary:** separate measurements for detection, verification, false alarms, and source-checking behavior; export/copy pilot results.

Avoid making the product feel like an ordinary "which picture is fake?" quiz with an archive panel added as decoration. Source investigation and decision replay are the core experience.

## 5. Scoring and observations

Maintain separate metrics instead of collapsing every action into one points total:

1. **Visual detection:** whether the player marks an intentionally edited region (only applicable to edited-photo and altered-quote cases).
2. **Verification correctness:** whether final verdict **and selected deciding evidence** answer the posed question correctly. Report verdict-only accuracy separately if useful.
3. **False alarms:** unsupported/fake conclusions on genuine cards, with initial suspicion tracked separately if useful.
4. **Checked before concluding:** whether the player consulted a source before submitting the final conclusion; distinguish publisher archive checks from independent-source checks.

Scoring must be deterministic from authored ground truth and action logs; no LLM should decide correctness at runtime. Partial credit or hints may support the training experience, but assessment scoring must remain stable and documented.

## 6. MVP scope

### Required

- All four challenge types, each with an unambiguous question and authored evidence.
- Twelve verified training cards (three per type), plus two **held-out matched sets** of four (one per type in each set).
- Four clickable proof-of-concept examples; they may be reused in training but never in held-out assessment.
- A shared fictional publisher/archive system, independent source pages, and coherent source attribution.
- First judgment, non-forced investigation, final verdict with evidence, replay, and the four separate metrics.
- Bangla/English UI, mobile interaction and appropriate zoom/reading support.
- Static deployment and privacy-preserving local/copyable pilot results.

### Explicitly out of scope

- Checking arbitrary real-world links or user-uploaded photocards.
- Automatic fact-checking or a general-purpose misinformation classifier.
- Accounts, public leaderboards, user profiles, real news APIs, social sharing of challenge images.
- Real political figures, impersonation of real publishers, live news claims, or misleadingly shareable fake cards.
- Complicated AI orchestration or backend dependencies for normal gameplay.
- Claims of statistically established learning gains from a small pilot.

## 7. Implementation direction

- **Architecture:** static web app; data-driven challenges in version-controlled JSON; reusable HTML/SVG for text and photocard layouts; local assets and optional processed image variants.
- **State machine:** `feed -> first_judgment -> investigate -> conclusion -> replay -> next`. A player can conclude directly from investigation without being forced to perform any specific check.
- **State and logging:** keep per-session action order, timestamps relative to session, challenge ID, first judgment, source views, marks, verdict, evidence IDs, and results. Minimize personal data.
- **Evaluation:** local deterministic functions for verdict/evidence accuracy, changed-region mask hits, and behavior counts.
- **Localization:** all user-visible interface strings, challenge prose, evidence text, and feedback must support the same semantics in Bangla and English.
- **Deployment:** low-friction static hosting; play without authentication or a paid external service.
- **Accessibility:** keyboard operation for evidence/answer controls; non-color-only status indicators; image text readable on narrow screens; alt descriptions; zoom; sufficient contrast and touch targets.

The exact framework/library choices may be finalized during the official specification stage. Do not make technology choices that endanger a complete working loop.

## 8. Privacy, authenticity and safety requirements

- Everything is **fictional educational material**. Use fictional outlets, events, people, and a permanent training watermark. Never clone a real newsroom's trademark or impersonate a real person.
- Genuine and fabricated cards from the same fictional outlet must use the **same logo, fonts, spacing, rendering pipeline, and template**. Any discrepancies must be intentionally part of an authored edit, never accidental giveaways.
- The mock publisher archive is explicitly **complete within the scenario**; it is not an actual verification service.
- Never say missing real-world publication equals definitive evidence of falsehood.
- Obtain rights for images/fonts; document licenses and ensure challenges cannot be mistaken for real news when detached from the app.
- Avoid collecting identifying information in the pilot; exports should be anonymized and locally initiated.
- Do not exaggerate pilot outcomes or claim that the system can determine authenticity of arbitrary external media.

## 9. Definition of done

The plan is implemented successfully when:

- A first-time user can complete the full loop across all four card types without assistance.
- At least one cleanly fabricated photocard has **no visual defect** and must be evaluated using publisher/source evidence.
- An edited-card reveal aligns with its original and its region mask, without spurious differences outside intended changes.
- Every challenge has validated ground truth and an explanation grounded in inspectable simulated evidence.
- Every replay accurately reflects actions actually taken, without inventing checks.
- Matched held-out items are kept out of training; evaluations report disaggregated metrics and raw counts.
- Bangla and English experiences function on mobile; the app remains playable without a server.
- End-to-end, data-integrity, scoring, and accessibility smoke tests pass.

## 10. Devpost workflow boundary

This document is an evergreen project plan, **not** a substitute for the official Devpost Learn Skill Pack. When beginning implementation, run its prescribed `1-start` through `6-ship` process and keep the generated `devpost/scope.md`, `devpost/prd.md`, and `devpost/spec.md` in the repository. The participant writes submission text in their own words. Check the official rules for final deliverables before submitting.

Resources: [event](https://learn-ai-basics.devpost.com/) · [rules](https://learn-ai-basics.devpost.com/rules).
