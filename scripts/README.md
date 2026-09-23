# Scripts

Planned entry points:

```text
audit_provenance.py
build_splits.py
train_text_baseline.py
evaluate.py
probe_generator_id.py
train_generator_adversarial.py
make_main_table.py
```

Implement the main training scripts only after the dataset provenance gate passes.

Every main command should record:
- config;
- git commit;
- dataset version;
- eligible-sample hash;
- split manifest;
- seed.
