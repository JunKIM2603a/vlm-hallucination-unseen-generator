# Novelty Collision Log

## Status

**COMPLETED — 2026-09-23**

## Bottom line

The exact proposed experiment — **train a hallucination detector on outputs from four generating VLMs and test on a fifth unseen generator, then compare against a matched random split** — was **not found as an already-established SHROOM-Visions result** in this search.

However, the novelty margin is **substantially narrower than originally assumed** because recent work already establishes several neighboring pieces:

1. **SHEEP itself** explicitly motivates model-independent evaluation and documents detector behavior differences across generating VLMs.
2. SHEEP reports **generator-conditioned HalluShift++ results** and cross-origin recalibration effects, including systematic degradation for one source/backbone combination.
3. **UHP Detection** argues that LVLMs exhibit distinct, model-specific hallucination patterns in consistency space.
4. **CounterVHD** explicitly reports cross-model transferability for a hallucination detector in a clinical LVLM setting.
5. SHROOM-Visions system papers already explore strong span detectors, activation probes, multi-judge ensembles, and calibrated multimodal taggers.

Therefore the proposed contribution cannot safely be framed as merely:

> "Hallucination detectors may behave differently across generating models."

That observation is already strongly anticipated by the 2026 literature.

The defensible remaining gap would have to be narrower:

> **Does conventional random-split training overestimate hallucination-detector performance relative to a strict leave-one-generating-VLM-out training protocol, and can that gap be causally linked to generator-identifying representations?**

Even this gap should not be pursued on SHEEP unless public generator provenance becomes available.

---

## Collision matrix

| Work | Date | Relevant finding | Relation to proposed study | Classification |
|---|---|---|---|---|
| **SHEEP — Can Humans Dream of Electric Sheep?** | 2026-08-02 | 20k multilingual samples; 1.6k human-written + 18.4k from five VLMs. Explicit goal is reducing dependence on particular model generations. Reports detector metrics per generating LVLM and cross-origin recalibration effects. | Very close motivation and empirical evidence that detector behavior depends on generation source, but does not appear to present the exact 4-train/1-unseen-generator detector-training protocol. | **HIGH / near-collision** |
| **Overview of SHROOM-Visions 2026** | 2026-08-26/28 | Frames the task as model-agnostic and designed for enduring evaluation across model generations; summarizes 27-team shared task. | Reinforces that model-independence is already an explicit benchmark design objective. | **PARTIAL-HIGH** |
| **UHP Detection** | 2026-08-04 | Learns structured consistency-space features and argues LVLMs have unique hallucination patterns; evaluates across multiple LVLMs and datasets. | Strong overlap with the idea that hallucination signals are generator/model-specific. The proposed study must avoid perturbation-consistency as its main novelty. | **HIGH concept overlap** |
| **SpanCalib-VLM** | 2026-08-30 | Multimodal span tagger + generative VLM fusion with calibration on SHROOM-Visions. | Strong baseline/system overlap, but not the same generator-disjoint training question. | **PARTIAL** |
| **Two-Token Features and Small-Large Ensembles** | 2026-09-09 | Fine-tuned token classifier + large VLM judge; synthetic hallucination data for ensemble diversity. | Relevant detector baseline; no identified unseen-generator training protocol. | **PARTIAL** |
| **Vroom-Vroom** | 2026-09-15 | Multi-judge VLM committee + activation probes; top shared-task results. | Activation probing overlaps with representation-level analysis, but not generator-ID invariance. | **PARTIAL** |
| **SKstars at SHROOM-Visions** | 2026-09-21 | Zero-shot + LoRA VLM ensemble; notes difficulty transferring dev-set improvements to hidden test. | Recent detector baseline; no explicit generator-disjoint analysis identified. | **CLEAR/PARTIAL** |
| **CounterVHD** | 2026-06-26 | Hallucination detector for clinical LVLM outputs with reported cross-model transferability. | Directly relevant to the broader claim that detector transfer across generators/models matters; domain and task differ. | **PARTIAL-HIGH** |

---

## Key evidence

### SHEEP

Paper:
https://arxiv.org/abs/2608.01021

Key points relevant to novelty:

- 1,600 human-written samples and 18,400 samples from five VLMs.
- Five generators: Gemma 3, InternVL3, MiniCPM-V 4.5, LLaVA-NeXT, Qwen3-VL.
- The paper explicitly asks whether human-written data can replace model-generated hallucinations to make detector benchmarking less dependent on particular models.
- It reports HalluShift++ F1 broken down by generating LVLM.
- It also recalibrates on data from different origins and reports that calibration on LLaVA systematically degrades performance; the paper interprets this as an example of bias introduced by model-dependent benchmarks.

This is the strongest novelty pressure on the original proposal.

### SHROOM-Visions overview

Paper:
https://arxiv.org/abs/2608.25662

Official task page:
https://helsinki-nlp.github.io/shroom/2026

The task explicitly describes itself as **model-agnostic** and positions SHEEP as suitable for evaluation across model generations.

### UHP Detection

Paper:
https://arxiv.org/abs/2608.03817

Code:
https://github.com/amirezzati/uhpdet

Relevant overlap:

- detects hallucination using image/text perturbation consistency features;
- argues different LVLMs have unique hallucination patterns;
- reports cross-dataset generalization.

Conclusion for this repository: **do not use perturbation consistency as the main novelty claim.**

### SpanCalib-VLM

Paper:
https://arxiv.org/abs/2608.29974

Code:
https://github.com/Aman-byte1/Hallucination-Detection-in-LVLMs

Relevant overlap:

- SHROOM-Visions span detection;
- multimodal XLM-R + SigLIP tagger;
- fine-tuned generative VLM;
- calibration-focused fusion.

Useful as a strong detector baseline family if a new dataset is selected.

### Vroom-Vroom

Paper:
https://arxiv.org/abs/2609.17327

Relevant overlap:

- multiple fine-tuned VLM judges;
- character-level majority voting;
- activation probes.

Representation probing is therefore not novel by itself. A generator-ID probe would need to answer a different mechanism question.

### Two-Token Features and Small-Large Ensembles

Paper:
https://arxiv.org/abs/2609.10244

Relevant overlap:

- per-token hidden-state features from a 4B VLM;
- ensemble with a much larger zero-shot VLM judge;
- synthetic hallucination data.

### SKstars

Paper:
https://arxiv.org/abs/2609.24198

Published 2026-09-21.

Relevant overlap:
- zero-shot + LoRA-adapted VLM ensemble;
- SHROOM-Visions evaluation;
- recent evidence that detector improvements do not transfer trivially from development data to hidden test data.

### CounterVHD

Paper:
https://arxiv.org/abs/2606.28520

Relevant overlap:
- hallucination detection across multiple LVLM backbones;
- explicit claim of cross-model transferability;
- clinical domain and entity-grounding formulation differ materially from SHROOM-style span detection.

---

## Collision assessment by proposed claim

### Claim A
"Different generating VLMs have different hallucination fingerprints."

**Not novel enough.**

SHEEP and UHP already provide strong evidence pointing in this direction.

### Claim B
"Hallucination detector performance differs by generating VLM."

**Not novel enough by itself.**

SHEEP already reports detector performance by generating LVLM and cross-origin recalibration effects.

### Claim C
"Random split materially overestimates performance compared with strict leave-one-generator-out detector training."

**Potentially still open based on this search.**

No exact matched random-vs-LOGO detector-training experiment was identified.

### Claim D
"The random-vs-LOGO gap is caused partly by generator-identifying representations, and adversarial generator removal reduces it."

**Potentially differentiated, but requires strong causal evidence.**

A simple generator probe is insufficient because activation probing is already common in recent systems. The contribution would need:

1. generator identity is recoverable;
2. recoverability predicts LOGO degradation;
3. an intervention suppresses generator identity;
4. suppression reduces the LOGO gap while retaining hallucination detection.

---

## Final novelty decision

**CONDITIONAL / HIGH COLLISION PRESSURE**

The exact LOGO training protocol was not found to be fully occupied, but the surrounding motivation and several expected findings are already present in 2026 work.

Because the dataset-provenance gate independently failed, this research should **not proceed on SHEEP in its current form**.

If the topic is revived with another dataset that exposes generator provenance, the paper should be reframed around the strict **random-split vs generator-disjoint training gap + causal shortcut evidence**, not around the general idea of model-specific hallucination behavior.

## Search cutoff

2026-09-23.
