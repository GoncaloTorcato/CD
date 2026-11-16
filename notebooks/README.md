# Project notebooks

The analysis and preparation code previously stored in `scripts/` is now organized here. Each notebook starts with a short explanation of its purpose, inputs, and outputs, followed by numbered steps.

These are working notebooks. The single notebook for submission is [delivery/music_hit_prediction.ipynb](../delivery/music_hit_prediction.ipynb), which contains the retained preparation steps and reads the original CSV files directly. It does not depend on these working notebooks or their exported artifacts.

| Notebook | Purpose | Outputs |
| --- | --- | --- |
| [01_genre_analysis.ipynb](01_genre_analysis.ipynb) | Count genres and compare coverage for different vocabulary sizes. | Frequency ranking, coverage table, and summary in `reports/genre_analysis/`. |
| [02_genre_preparation.ipynb](02_genre_preparation.ipynb) | Replace `artist_genres` with 1,000 binary genre columns and `genre_unknown`. | `data/processed/train.csv` and `models/genre_vocabulary.json`. |

Select a Python environment with the repository dependencies installed, then restart the kernel and run all cells from top to bottom. Both notebooks work from the project root or `notebooks/`, and each can run independently. Notebook 02 regenerates the processed CSV, which is about 735 MiB; raw files are never modified.

Genre frequencies count tracks, not unique artists. Tracks without genres have `genre_unknown = 1`; tracks with known genres outside the selected vocabulary have `genre_unknown = 0`.

The current preparation uses the full training CSV. When evaluating models, select the genre vocabulary using only the training split and reuse it on validation and test data.
