# Project notebooks

The analysis and preparation code previously stored in `scripts/` is now organized here. Each notebook starts with a short explanation of its purpose, inputs, and outputs, followed by numbered steps.

These are working notebooks. The single notebook for submission is [delivery/music_hit_prediction.ipynb](../delivery/music_hit_prediction.ipynb), which contains the retained preparation steps and reads the original CSV files directly. It does not depend on these working notebooks or their exported artifacts.

| Notebook | Purpose | Outputs |
| --- | --- | --- |
| [01_genre_analysis.ipynb](01_genre_analysis.ipynb) | Count genres and compare coverage for different vocabulary sizes. | Frequency ranking, coverage table, and summary in `reports/genre_analysis/`. |
| [02_genre_preparation.ipynb](02_genre_preparation.ipynb) | Replace `artist_genres` with 1,000 binary genre columns and `genre_unknown`. | `data/processed/train_genres_only.csv` and `models/genre_vocabulary.json`. |
| [03_text_metadata_preparation.ipynb](03_text_metadata_preparation.ipynb) | Study `track_name`, `album_name`, and `record_label`, then fill missing fields with `unknown`. | Cleaned training/test frames in memory and `reports/text_metadata/summary.md`. |
| [04_artist_name_preparation.ipynb](04_artist_name_preparation.ipynb) | Study surrounding spaces in `artist_name`, check follower consistency, and trim the names. | Cleaned training/test frames in memory and `reports/artist_name_preparation/summary.md`. |
| [05_release_date_preparation.ipynb](05_release_date_preparation.ipynb) | Study release dates and replace `release_date` with the numeric `release_year` feature. | Prepared training/test frames in memory and `reports/release_date_preparation/summary.md`. |
| [06_duration_preparation.ipynb](06_duration_preparation.ipynb) | Study durations and exclude only zero-duration training rows, retaining every test track. | Filtered training/test frames in memory and `reports/duration_preparation/summary.md`. |
| [07_artist_followers_preparation.ipynb](07_artist_followers_preparation.ipynb) | Study follower-count skewness and add `artist_followers_log1p`, preserving the original counts. | Prepared training/test frames in memory and `reports/artist_followers_preparation/summary.md`. |

Select a Python environment with the repository dependencies installed, then restart the kernel and run all cells from top to bottom. All working notebooks work from the project root or `notebooks/`, and each can run independently. Notebook 02 optionally regenerates a separate genre-only snapshot (`train_genres_only.csv`), which is about 735 MiB; notebooks 03–07 keep their prepared frames in memory. Raw files are never modified. The delivery notebook combines training-only zero-duration filtering, missing-text filling, artist-name trimming, release-year extraction, a logarithmic follower feature, and genre encoding without depending on intermediate files. With `EXPORT_PROCESSED_CSV = True`, it exports the complete preparation to `data/processed/train.csv` and `data/processed/test.csv`.

Genre frequencies count tracks, not unique artists. Tracks without genres have `genre_unknown = 1`; tracks with known genres outside the selected vocabulary have `genre_unknown = 0`.

The current preparation uses the full training CSV. When evaluating models, select the genre vocabulary using only the training split and reuse it on validation and test data.
