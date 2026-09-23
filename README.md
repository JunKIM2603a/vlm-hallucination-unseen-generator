# VLM Hallucination Unseen-Generator Generalization

This repository investigates whether VLM hallucination detectors learn **hallucination signals that generalize across generating models**, or partially exploit **generator-specific fingerprints** shared between train and test data under ordinary random splits.

## Core question

> If a detector performs well on a random split, does that performance persist when every output from one generating VLM is excluded from training and used only for testing?

## Hypotheses

- **H1 — Unseen-generator gap:** random-split performance is higher than leave-one-generator-out (LOGO) performance.
- **H2 — Generator fingerprint:** part of that gap is explained by generator-specific information in inputs or learned representations.
- **H3 — Generator invariance:** human-written data and/or generator-invariant learning reduce the unseen-generator gap.

## Primary dataset

Initial target: **SHEEP — Can Humans Dream of Electric Sheep?**

Current planning assumptions:
- human-written samples: ~1,600
- VLM-generated samples: ~18,400
- generating VLMs: 5

These counts remain **unverified planning assumptions** until the public release and metadata are audited.

### Hard provenance gate

Before any main experiment:

1. Verify reliable per-sample generating-VLM provenance.
2. Verify the mapping for all machine-generated samples used in the study.
3. Record the evidence under `data/provenance/`.
4. **KILL the project if generator provenance cannot be recovered reliably.**

## Minimum Decisive Experiment

Start with the simplest **text-only classifier**.

### Random split
Outputs from the same generating VLMs may occur in both train and test sets.

### Leave-one-generator-out
For each of the five generators:

```text
train = outputs from 4 generators
test  = all eligible outputs from 1 held-out generator
```

Repeat for all five generators.

### Decision rule

- **GO:** repeated, meaningful degradation on unseen generators.
- **CONDITIONAL GO:** degradation varies strongly by held-out generator; analyze which generator pairs create shortcuts.
- **KILL:** provenance is unavailable/unreliable, or LOGO remains close to the random-split baseline across all holdouts.

## Baselines

1. Text-only classifier
2. Frozen vision + text feature classifier
3. Multimodal fusion classifier

## H2 mechanism analysis

A LOGO performance drop alone is not sufficient evidence of a generator fingerprint.

Planned evidence:
- generator-ID probes on detector representations;
- layer/representation analysis;
- generator-pair transfer analysis;
- confound checks for prompt/image/topic/length/style distribution;
- ablations or invariance interventions.

## Proposed intervention

Generator-adversarial representation learning with gradient reversal:

```text
L = L_span + α L_type − β L_generator
```

## Metrics

- character/span IoU
- correlation
- label-conditioned correlation
- hallucination-type metric
- random-vs-unseen-generator gap
- per-generator LOGO performance

## Novelty gate

Before professor submission or full experiments, update `docs/novelty_collision.md` with a fresh **September 2026** search.

Priority checks:
- SHEEP
- SHROOM / SHROOM-Visions 2026
- UHP Detection
- SpanCalib-VLM
- Vroom-Vroom / multi-judge approaches
- recent SHROOM hallucination-detection work

A simple **"perturbation consistency detects hallucination"** contribution is intentionally not the target because of likely overlap with UHP-style work.

## Timeline

| Target | Milestone |
|---|---|
| ~2026-10-02 | dataset provenance + novelty collision gate |
| after PASS | random split vs LOGO minimum experiment |
| ~2026-10-12 | main unseen-generator finding / main table |
| November | invariance method + model/language extensions |
| 2026-12-14 | experiments and thesis paper complete |

## Repository layout

```text
configs/
data/
  raw/
  processed/
  provenance/
docs/
experiments/
  random_split/
  leave_one_generator_out/
  generator_invariance/
results/
scripts/
src/
tests/
```

## Current status

**DROP / KILL as currently specified — 2026-09-23**

The two pre-experiment gates were completed before launching the Minimum Decisive Experiment:

- [x] September 2026 novelty-collision search completed
- [x] SHEEP public provenance audit completed
- [ ] Reliable public per-sample generator provenance available — **FAILED**

### Why the experiment is blocked

The SHEEP paper internally distinguishes five generating VLMs and reports generator-conditioned analyses, but the currently public SHROOM-Visions release/documented JSONL schema does not expose a per-sample generator field, and the official task page does not link separate provenance metadata.

Per the preregistered decision rule, generator identity must **not** be reconstructed from response style or fingerprints and then treated as ground truth.

See:

- `data/provenance/README.md` — provenance audit and KILL decision
- `docs/novelty_collision.md` — 2026-09-23 collision search

### Novelty conclusion

The exact matched **random split vs leave-one-generator-out detector training** experiment was not found to be fully occupied, but SHEEP already studies model-dependent benchmark effects and generator-conditioned detector behavior, while UHP and other 2026 work further increase collision pressure.

The topic should only be reopened if a dataset with reliable public generator provenance is identified or the SHEEP authors release an official sample-to-generator mapping.
