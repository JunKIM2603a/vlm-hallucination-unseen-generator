# Random-Split Experiments

Purpose: establish the conventional in-distribution baseline.

Required safeguards:

- use the same eligible sample pool as the corresponding LOGO study when possible;
- group duplicate/source-linked examples when needed to prevent trivial leakage;
- store seed, split-manifest hash, config, and git commit;
- do not use held-out-generator information to tune the LOGO experiments.
