# Dataset Provenance Audit

This directory stores the evidence needed to decide whether the project is viable.

## Hard question

Can every machine-generated sample used in the experiment be mapped reliably to its generating VLM?

If **no**, the planned leave-one-generator-out study should be stopped.

## Evidence checklist

- [ ] authoritative dataset/repository identified
- [ ] dataset version or commit pinned
- [ ] generator metadata field located
- [ ] generator names/IDs enumerated
- [ ] machine-generated sample count verified
- [ ] human-written sample count verified
- [ ] missing generator IDs counted
- [ ] duplicate/source relationships inspected
- [ ] ambiguous samples documented
- [ ] final eligible-sample mapping hash recorded

## Recommended mapping columns

```text
sample_id
source_id
image_id
prompt_id
generator_id
generator_name
is_human
target_label
hallucination_type
metadata_file
metadata_field
provenance_source
eligible
exclusion_reason
```

## Evidence log

| Item | Finding | Source | Verified date |
|---|---|---|---|
| dataset release | TODO | | |
| generator field | TODO | | |
| generator list | TODO | | |
| machine count | TODO | | |
| human count | TODO | | |

## Rule

Do not guess the generator from writing style or model fingerprints and then use that guessed identity as ground-truth provenance.
