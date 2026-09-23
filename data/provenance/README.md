# Dataset Provenance Audit

## Final status: FAIL / KILL

Checked: **2026-09-23**

The project required public, reliable per-sample generating-VLM provenance for SHEEP. That requirement is **not met by the currently public SHROOM-Visions/SHEEP release that could be verified**.

## Evidence

### 1. Authoritative public task page

The official SHROOM-Visions 2026 page identifies SHEEP/SHROOM-Visions as a 20,000-sample dataset and states that the model-written portion comes from **5 diverse LVLMs**. It provides links to the released data and images:

- https://helsinki-nlp.github.io/shroom/2026
- official repository page source:
  https://github.com/Helsinki-NLP/shroom/blob/main/2026.md

However, the official page does **not** publish or link a separate generator-provenance metadata file. Searching the official `2026.md` source found no `metadata` or `generator` field/documentation.

### 2. Publicly documented JSONL schema

A SHROOM-Visions participant repository documents the released labeled JSONL schema as:

```json
{
  "id": "train-en-413",
  "language": "en",
  "prompt": "...",
  "image_name": "...jpg",
  "response": "...",
  "labels": [
    {
      "start": 148,
      "end": 154,
      "prob": 0.33,
      "label": "mischaracterization"
    }
  ]
}
```

Source:

https://github.com/sckwokyboom/Vision-Hallucination-Detector/blob/main/data/README.md

The documented public schema contains **no per-sample generating-model field** such as `generator_id`, `model_name`, `origin_model`, or equivalent.

### 3. The SHEEP paper does know generator identity internally

The SHEEP paper states that model-written samples were generated using five VLMs:

- Gemma 3
- InternVL3
- MiniCPM-V 4.5
- LLaVA-NeXT
- Qwen3-VL

Paper:

https://arxiv.org/abs/2608.01021

The paper also reports analyses broken down by generating LVLM, so the authors clearly possessed generator provenance during dataset construction.

But this is **not sufficient for this project**: the research prerequisite was that generator provenance be available in the **actual public metadata** so that a reproducible leave-one-generator-out split can be built without guessing or reconstructing model identity.

## Checklist

- [x] authoritative dataset/repository identified
- [x] public release located
- [x] five generating VLMs verified from the paper
- [x] public labeled JSONL schema inspected through a participant implementation
- [x] official task-page source checked for metadata/generator documentation
- [ ] per-sample generator metadata field located
- [ ] reproducible sample → generator mapping recovered from public metadata

## Decision

**KILL the planned SHEEP leave-one-generator-out study in its current form.**

Do not infer generator labels from response style, model fingerprints, output wording, or clustering and then treat those inferred labels as ground truth.

## What would reopen this gate?

Only strong provenance evidence, for example:

1. an official metadata release containing sample → generator identity;
2. an official authors' repository with that mapping;
3. a first-party supplementary file released after this audit;
4. direct author-provided provenance that can be redistributed/reproduced for the study.

Until then, Issue #1 is considered failed and the planned MDE is blocked.
