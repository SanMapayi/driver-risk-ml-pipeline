# Reproducibility checklist

Before comparing model runs, record:

- Dataset source, permission to redistribute it, checksum, and label definition.
- Cleaning rules and excluded or derived columns.
- Train/test split method, seed, and whether drivers or journeys overlap between splits.
- Network configuration, optimiser, learning rate, epoch count, and software versions.
- Whether an existing model or processed CSVs were reused.
- Confusion matrix and per-class precision/recall/F1, alongside aggregate metrics.

Keep evaluation data separate from fitting and preprocessing decisions. If rows from the same driver or journey appear in both partitions, document the limitation and consider grouped or temporal evaluation.

The current training entry point can resume from the existing model and reuse the existing processed split. Preserve a copy of those artifacts before replacing them; do not describe a resumed run as training from scratch.

Large models, raw telemetry, or private data should not be uploaded merely to make a repository appear complete. Provide a documented, permitted sample dataset and artifact-retrieval instructions where appropriate.