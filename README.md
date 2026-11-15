# Music Hit Prediction

A data science project to predict the probability that a track is a music hit using its metadata and audio features. The evaluation metric is **ROC AUC**.

## Directories

- `data/raw/` — original training and test data, kept unchanged.
- `data/processed/` — cleaned and prepared data for analysis and modeling.
- `notebooks/` — numbered notebooks for analysis and data preparation; see [notebooks/README.md](notebooks/README.md).
- `src/` — reusable code for data preparation and model training.
- `models/` — trained models and preprocessing metadata, including the selected genre vocabulary.
- `reports/` — reports and results; `reports/figures/` stores plots.
- `submissions/` — CSV files containing predictions for submission.

The downloaded competition files are in `data/raw/`. See [data/README.md](data/README.md) for the dataset and column descriptions.

## Submission

The file must contain one row per track in the test set, with an `id` and a `music_hit` probability between 0 and 1:

```csv
id,music_hit
350052,0.2
350053,0.2
350054,0.6
```
