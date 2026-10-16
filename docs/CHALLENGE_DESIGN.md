# Challenge and evidence design

This is the authoring contract for all Spot the Edit + Verify challenges. The aim is to teach **evidence-based investigation**, not template-recognition tricks.

## 1. Canonical card set

- **Edited photo:** a localized edit to a photo used in an otherwise legitimate fictional publisher card; archive contains the original.
- **Altered quote:** a quotation in an otherwise faithful publisher card is replaced or modified; archive contains the original text/card.
- **Clean fabrication:** a card was made from scratch with the **same exact outlet design assets**, but its supposed publication does not exist in the fully specified simulated archive. There need not be an editable "original" or a visual mask.
- **Genuine card:** the shared card matches the archive publication. No forced suspicious clue, and no positive edit mask.

Suggested content inventory: 12 training items (3/type) + matched held-out set A (4 items, 1/type) + matched held-out set B (4 items, 1/type). The four initial prototype examples can later join the training pool; they must not leak into held-out sets.

Use roughly one genuine challenge per four-item balanced set. Do not rely on one-to-one "real/fake" point totals to tell users what to pick.

## 2. Fictional media universe and evidence surfaces

Maintain a small, coherent group of fictional outlets (initially three), each with a reusable **single source of truth** for logo, typography, card templates, metadata, and publication history.

Each challenge may provide:

1. A **shared social-media card** (the artifact the player sees initially).
2. A **publisher archive** page/search, identified as **complete for the fictional scenario**, containing dated records and original photocards when published.
3. An **independent source** page, authored from a distinct organization/perspective, with evidence relevant to the question. It can confirm a fact, contradict a claim, or leave it unresolved.
4. A final **explanation**, identifying what each piece of evidence does and does *not* prove.

**Guardrail:** `publisher_record_missing` in a complete fictional archive can refute attribution *to that fictional outlet*. It does not by itself refute the claim's real-world truth. In ordinary life a missing online post is not proof; cross-check a second reliable source.

Never display "genuine" based solely on clean design, or "false" based solely on an absent article without making the question and simulation assumptions explicit.

## 3. Challenge authoring rules

- Genuine and fabricated cards of the **same outlet must render from identical templates and exact font/logo files**. Do not assign obviously "faker" styles to negative examples.
- Keep image sizes, compression, margins, watermark placement, and metadata treatment consistent across card classes.
- Every card and archive screenshot/page is visibly and persistently marked as a **fictional training simulation**, including in standalone exports.
- Use fictional people, fictional events, and invented news organizations. Avoid real-world political claims, trademarks, and real newsroom logos.
- Make visual edit regions deterministic. For AI/local photo editing, render original and altered variants and paste changed pixels through the intended mask so pixels outside the mask match. Validate the mask, including at common display scales.
- For changed quotes in SVG/HTML, fix text containers to preserve layout and explicitly identify the authored changed text region; do not let incidental line wrapping give away all altered cards.
- A visual mark is optional: fabricated and genuine cards have **no valid edited region**. A clean fabricated card must be able to look indistinguishable in style from a true publisher card.
- Every conclusion must be justified by evidence the player can actually open. Do not expose the answer in file names, CSS classes visible to players, URL paths, or UI styling.
- Write feedback that generalizes beyond the fictional outlet; distinguish a *clue* from *proof*.

## 4. Example data contract (illustrative, not implemented)

```json
{
  "id": "training-clean-fabrication-01",
  "split": "training",
  "matchedPairId": null,
  "type": "clean_fabrication",
  "outletId": "outlet-signal",
  "question": {
    "en": "Did The Daily Signal publish this exact report?",
    "bn": "..."
  },
  "cardAsset": "/assets/cards/training-clean-fabrication-01.svg",
  "originalAsset": null,
  "editMaskAsset": null,
  "publisherArchiveEvidenceId": "archive-01",
  "independentEvidenceIds": ["source-01"],
  "groundTruth": {
    "conclusion": "not_supported",
    "decisiveEvidenceIds": ["archive-01"],
    "attributionPublished": false,
    "underlyingClaimStatus": "undetermined"
  }
}
```

The `bn` placeholder illustrates a translation field only; actual content must contain complete human-reviewed Bangla. The full implementation should formalize separate entities for publishers, sources, archives, assets, and challenge records, with a schema validator and stable evidence IDs.

### Required fields / invariants

| Field / concept | Rule |
| --- | --- |
| `split` | Exactly `prototype`, `training`, `heldout_a` or `heldout_b`; no held-out leakage |
| `type` | Exactly one of four canonical card types |
| `matchedPairId` | Shared between corresponding held-out A/B items only |
| `question` | Specifies what is being verified and its unit of truth |
| `cardAsset` | Always exists; watermark embedded in the asset |
| `originalAsset` | Required where comparison to a real fictional publication is relevant; absent for clean fabrications |
| `editMaskAsset` | Required only for deliberately localized visual edits; absent for genuine/fabrication |
| Archive completeness | Clearly shown in the in-game archive UI, not implied about real sources |
| `groundTruth` | Conclusion, attribution state, claim state where relevant, and inspectable deciding evidence |
| Translations | Parallel human-checked Bangla and English content, not just interface chrome |

## 5. Matched held-out set design

Each A challenge has one B twin with:

- The **same card type** and a closely matched reading burden.
- The **same number of meaningful clues**, and similar edit visibility if applicable.
- Similar archive navigation/search depth and independent-source complexity.
- Comparable language difficulty, headline length, and topic familiarity.
- **Different story content**, preventing memorization of a training or pretest answer.

A/B templates should be identical in structure, but identical templates do not *guarantee* equal difficulty. Have people independent of the author review pairs and rebalance conspicuously unequal ones.

Held-out items must never appear with feedback during training. Keep answer keys isolated from player-facing UI before submission.

## 6. Author acceptance checklist

A challenge is ready only if all answers are yes:

- [ ] A stranger can state the exact verification question.
- [ ] The card cannot be mistaken for a real published item outside the app.
- [ ] The fictional outlet's genuine and fabricated examples use identical branding assets.
- [ ] The archive and independent evidence are navigable and internally consistent.
- [ ] The correct conclusion follows from available evidence, not from an unexplained assertion.
- [ ] The explanation clearly distinguishes publisher attribution from underlying claim truth.
- [ ] Visual region answers are precise when applicable and absent when inapplicable.
- [ ] Bangla and English passages communicate the same facts and uncertainty.
- [ ] Author metadata, answer keys, assets, licenses and citations are present.
- [ ] The item has not leaked into an assessment split.
