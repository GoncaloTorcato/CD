# Music Hit Prediction

A data science project to predict the probability that a track is a music hit using its metadata and audio features. The evaluation metric is **ROC AUC**.

## Directories

- `data/raw/` — original training and test data, kept unchanged.
- `data/processed/` — cleaned and prepared data for analysis and modeling.
- `notebooks/` — numbered notebooks for analysis and data preparation; see [notebooks/README.md](notebooks/README.md).
- `delivery/` — the [submission notebook](delivery/music_hit_prediction.ipynb), running one logistic regression configuration on the prepared CSV files, and `predictions.csv` with test probabilities.
- `src/` — reusable code for data preparation and model training.
- `models/` — trained models and preprocessing metadata, including the selected genre vocabulary.
- `reports/` — reports and results; `reports/figures/` stores plots.
- `submissions/` — CSV files containing predictions for submission.

The downloaded competition files are in `data/raw/`. See [data/README.md](data/README.md) for the dataset and column descriptions.

The [complete preparation notebook](notebooks/00_data_preparation.ipynb) reproduces the retained changes and exports the prepared CSV files. The [logistic regression baseline](notebooks/08_logistic_regression_baseline.ipynb) and delivery notebook both read those files directly and train one fixed configuration with logarithmic followers, prepared genre indicators, and group-aware record-label target encoding. They write scores to `reports/logistic_regression/`, save the model and encoders to `models/logistic_regression.joblib`, and generate `delivery/predictions.csv`. The [record-label study](notebooks/09_record_label_encoding.ipynb) documents the measured contribution of the added feature.

## Submission

The file must contain one row per track in the test set, with an `id` and a `music_hit` probability between 0 and 1:

```csv
id,music_hit
350052,0.2
350053,0.2
350054,0.6
```
