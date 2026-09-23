# Novelty Collision Log

## Status

**PENDING — complete a fresh September 2026 literature search before professor submission or novelty claims.**

This file separates verified evidence from planning assumptions.

## Target contribution to protect

> Evaluate VLM hallucination detectors under a generator-disjoint protocol and test whether random-split performance is inflated by generator-specific shortcuts.

The intended contribution is **not** simply perturbation-consistency-based hallucination detection.

## Required collision search

| Work / family | What to verify | Status | Evidence |
|---|---|---|---|
| SHEEP | provenance, baseline splits, cross-generator analysis | TODO | |
| SHROOM / SHROOM-Visions 2026 | generator-disjoint detector evaluation | TODO | |
| UHP Detection | overlap with perturbation/consistency mechanisms | TODO | |
| SpanCalib-VLM | overlap in span-level detector calibration/generalization | TODO | |
| Vroom-Vroom / multi-judge | overlap with cross-model robustness | TODO | |
| recent SHROOM detector papers | random-vs-generator-disjoint evaluation | TODO | |
| 2026 Aug–Sep literature | explicit unseen-generator hallucination-detector study | TODO | |

## Questions for each paper

1. Is the generating VLM identity known?
2. Is train/test generator-disjoint?
3. Is one generating VLM completely unseen during training?
4. Is the paper evaluating a hallucination detector rather than the generator itself?
5. Does it test whether random split overestimates generalization?
6. Does it analyze generator-identifying representations or shortcuts?
7. Does it use generator-adversarial or other invariance training?

## Collision classification

- **CLEAR** — different research question.
- **PARTIAL** — shares dataset/method/motivation, but not the central generator-disjoint claim.
- **HIGH** — directly evaluates unseen generators in hallucination detection.
- **COLLISION** — central hypothesis and intended contribution already substantially demonstrated.

## Evidence standard

Prefer:
1. paper PDF / official proceedings;
2. official project page or repository;
3. dataset card / first-party metadata;
4. secondary summaries only for discovery.

Record title, authors, publication date, venue, identifier/URL, and the exact relevant experiment.

## Decision

- [ ] CLEAR / manageable overlap → continue
- [ ] PARTIAL overlap → narrow contribution
- [ ] HIGH / COLLISION → redesign or drop before expensive experiments

## Last checked

Not yet completed.
