# Research Proposal

## Working title

**Do VLM Hallucination Detectors Generalize to Unseen Generators?  
Testing Generator-Specific Shortcut Learning under Leave-One-Generator-Out Evaluation**

## Motivation

Random train/test splits can place outputs from the same generating VLMs on both sides of evaluation. A detector may therefore exploit generator-specific style, formatting, lexical, or representation patterns instead of learning only hallucination-relevant signals.

The central question is whether detector performance survives a **generator-disjoint** evaluation.

## Research gap

This project does not ask merely whether hallucinations can be detected.

It asks whether conventional random-split evaluation can overestimate generalization because the same generator identities occur in both training and testing.

This gap must be rechecked against the latest September 2026 literature before novelty is claimed.

## Hypotheses

### H1
Random-split performance is higher than leave-one-generator-out performance.

### H2
Part of the gap is associated with generator-identifying information in the detector input or learned representation.

### H3
Human-written data and/or generator-invariant representation learning reduce the unseen-generator gap.

## Dataset gate

Primary candidate: SHEEP.

The project proceeds only if trustworthy per-sample generating-VLM provenance exists.

**KILL condition:** generator provenance cannot be recovered reliably from first-party/public metadata.

## Experimental stages

### Stage 0 — viability
1. Verify SHEEP release and generator provenance.
2. Verify counts and usable subsets.
3. Run September 2026 novelty-collision search.
4. Freeze the minimum experimental protocol.

### Stage 1 — Minimum Decisive Experiment
Use a simple text-only detector.

Compare:
- random split;
- five leave-one-generator-out runs.

### Stage 2 — fingerprint mechanism
Measure generator identity recoverability from:
- raw/text features;
- detector embeddings;
- intermediate representations.

Then analyze whether generator predictability is associated with larger unseen-generator failures.

### Stage 3 — multimodal baselines
1. text-only classifier;
2. frozen vision + text feature classifier;
3. multimodal fusion classifier.

### Stage 4 — intervention
Use generator-adversarial representation learning:

```text
L = L_span + α L_type − β L_generator
```

with gradient reversal on the generator branch.

## Main table

| Detector | Random | Holdout G1 | Holdout G2 | Holdout G3 | Holdout G4 | Holdout G5 | Mean LOGO | Gap |
|---|---:|---:|---:|---:|---:|---:|---:|---:|
| Text-only | TBD | TBD | TBD | TBD | TBD | TBD | TBD | TBD |
| Frozen V+T | TBD | TBD | TBD | TBD | TBD | TBD | TBD | TBD |
| Multimodal | TBD | TBD | TBD | TBD | TBD | TBD | TBD | TBD |
| + invariant | TBD | TBD | TBD | TBD | TBD | TBD | TBD | TBD |

## Decision criteria

### GO
Repeated and practically meaningful unseen-generator degradation across multiple holdouts.

### CONDITIONAL GO
Strong generator-dependent heterogeneity. Shift the contribution toward generator-pair shortcut analysis.

### KILL
- provenance unavailable/unreliable; or
- random and LOGO performance remain close across all generator holdouts.

## Main risks

1. Novelty collision with very recent 2026 work.
2. Generator identity confounded with prompts, images, topics, languages, or answer lengths.
3. Metric mismatch between span-level and sample-level claims.
4. Mechanistic overclaiming if H2 is inferred only from H1.

## Intended contributions if supported

1. Evidence that random-split evaluation can overestimate unseen-generator generalization.
2. Characterization of generator-specific shortcuts.
3. Generator-invariant training.
4. A practical generator-disjoint evaluation protocol for hallucination detectors.
