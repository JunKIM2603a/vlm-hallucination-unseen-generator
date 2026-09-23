# Leave-One-Generator-Out Experiments

For each generating VLM:

```text
train      = all other eligible generators
validation = train-side generators only
test       = held-out generator only
```

The held-out generator must not be used for:
- model selection;
- threshold tuning;
- calibration;
- early stopping.

Primary outputs:
- per-generator metric;
- mean LOGO metric;
- matched random-split metric;
- random-minus-LOGO gap.
