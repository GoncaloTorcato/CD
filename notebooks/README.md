# Project notebooks

We keep data preparation separate from model evaluation. Both [08_logistic_regression_baseline.ipynb](08_logistic_regression_baseline.ipynb) and [delivery/music_hit_prediction.ipynb](../delivery/music_hit_prediction.ipynb) read only the existing `data/processed/train.csv` and `data/processed/test.csv` files.

| Notebook | Purpose | Outputs |
| --- | --- | --- |
| [00_data_preparation.ipynb](00_data_preparation.ipynb) | Reproduce all retained transformations from the original competition CSV files. | Complete `data/processed/train.csv` and `test.csv`. |
| [01_genre_analysis.ipynb](01_genre_analysis.ipynb) | Study genre frequencies and coverage. | `reports/genre_analysis/`. |
| [02_genre_preparation.ipynb](02_genre_preparation.ipynb) | Reproduce a separate genre-only working snapshot. | `data/processed/train_genres_only.csv` and `models/genre_vocabulary.json`. |
| [03_text_metadata_preparation.ipynb](03_text_metadata_preparation.ipynb) | Study missing titles, album names, and labels and fill them with `unknown`. | In-memory frames and `reports/text_metadata/`. |
| [04_artist_name_preparation.ipynb](04_artist_name_preparation.ipynb) | Study and trim surrounding spaces in artist names. | In-memory frames and `reports/artist_name_preparation/`. |
| [05_release_date_preparation.ipynb](05_release_date_preparation.ipynb) | Study dates and retain the release year. | In-memory frames and `reports/release_date_preparation/`. |
| [06_duration_preparation.ipynb](06_duration_preparation.ipynb) | Exclude only zero-duration training tracks. | In-memory frames and `reports/duration_preparation/`. |
| [07_artist_followers_preparation.ipynb](07_artist_followers_preparation.ipynb) | Study and add logarithmic follower counts. | In-memory frames and `reports/artist_followers_preparation/`. |
| [08_logistic_regression_baseline.ipynb](08_logistic_regression_baseline.ipynb) | Train and evaluate one fixed logistic regression on prepared data, then refit on all training rows. | `reports/logistic_regression/`, `models/logistic_regression.joblib`, and `delivery/predictions.csv`. |
| [09_record_label_encoding.ipynb](09_record_label_encoding.ipynb) | Study record labels and measure the effect of adding group-aware target encoding. | Before/after metrics and decision in `reports/record_label_encoding/`. |

To regenerate prepared CSV files, run notebook 00. To evaluate the current prepared data, run notebook 08 or the delivery notebook from top to bottom. The model notebooks do not repeat cleaning, select genres again, or compare alternative feature sets.

The fixed model uses logarithmic followers, prepared genre indicators, audio attributes, duration, release year, binary features, one-hot encoded small categories, and a target-encoded record-label feature. Original followers, IDs, titles, artist names, and the target remain outside the input feature set. Notebook 09 records the before/after experiment; notebooks 08 and delivery fit only the adopted configuration.

The validation partition comes from the prepared labeled training file; the unlabeled test file is used for final probability predictions. Numerical imputation, scaling, and model-time categorical encoding are fitted on the training partition only. The existing genre columns were selected during preparation before this split, so the reported validation evaluates that fixed prepared dataset.

Record-label target encoding uses five internal training folds with duplicate groups kept together. Training rows receive smoothed rates computed from other groups. Validation/test rows use an encoder fitted only on the available training labels, with unseen labels mapped to the training hit rate. Encoded rates are between 0 and 1 before standardization. The encoder and scaler are saved with the model; supervised encodings are not written into the processed CSV files.

The delivery notebook depends on the prepared CSV files. Raw files and large processed files are not changed during model training.
