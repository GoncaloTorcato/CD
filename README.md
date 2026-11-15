# Music Hit Prediction

A data science project to predict the probability that a track is a music hit using its metadata and audio features. The evaluation metric is **ROC AUC**.

## Directories

- `data/raw/` — original training and test data, kept unchanged.
- `data/processed/` — cleaned and prepared data for analysis and modeling.
- `notebooks/` — data exploration, visualizations, and experiments.
- `src/` — reusable code for data preparation and model training.
- `models/` — trained models and associated files.
- `reports/` — reports and results; `reports/figures/` stores plots.
- `submissions/` — CSV files containing predictions for submission.

The existing `data/project_data.csv` file contains only identifiers and values that appear to be predictions; it does not contain the features needed to train a model. See [data/README.md](data/README.md) for the dataset and column descriptions.

## Submission

The file must contain one row per track in the test set, with an `id` and a `music_hit` probability between 0 and 1:

```csv
id,music_hit
350052,0.2
350053,0.2
350054,0.6
```
