# Dataset

According to the competition description, the dataset consists of:

- `train.csv`: track identifiers, features, and the `music_hit` target (1 for a music hit and 0 otherwise).
- `test.csv`: track identifiers and features without the target. It is used to generate predictions for submission.
- `sample_submission.csv`: an example of the submission format.

The three downloaded files are in `raw/`: `train.csv` contains 350,051 rows and 24 columns, `test.csv` contains 87,513 rows and 23 columns, and `sample_submission.csv` contains 87,513 rows with the columns `id` and `music_hit`.

## Processed datasets

The delivery notebook exports the complete preparation to `processed/train.csv` and `processed/test.csv` when `EXPORT_PROCESSED_CSV = True`. These files preserve the relative order of retained rows and include:

- Training-only exclusion of zero-duration tracks (IDs `244276` and `287253`); all test rows are retained.
- Missing `track_name`, `album_name`, and `record_label` values filled with `unknown`.
- Leading and trailing whitespace removed from `artist_name`.
- `release_date` replaced with the numeric feature `release_year`.
- `artist_genres` replaced with the same 1,000 binary genre columns and `genre_unknown` in both datasets. The vocabulary is selected using only training data.

The training file contains 350,049 rows and 1,024 columns; the test file contains 87,513 rows and 1,023 columns, without `music_hit`. Raw files remain unchanged, and processed CSV files are excluded from Git.

To reproduce the current files, run [delivery/music_hit_prediction.ipynb](../delivery/music_hit_prediction.ipynb) from top to bottom with export enabled. The individual studies are in `notebooks/03_text_metadata_preparation.ipynb`, `04_artist_name_preparation.ipynb`, `05_release_date_preparation.ipynb`, and `06_duration_preparation.ipynb`.

The optional genre-only working snapshot is exported separately as `processed/train_genres_only.csv` by [02_genre_preparation.ipynb](../notebooks/02_genre_preparation.ipynb), together with [`models/genre_vocabulary.json`](../models/genre_vocabulary.json). It does not overwrite the complete prepared datasets.

## Column descriptions

| Column | Description |
| --- | --- |
| `id` | Unique identifier for the track in the dataset. |
| `track_name` | Title of the track. |
| `album_type` | Type of album containing the track. |
| `album_name` | Title of the album. |
| `release_date` | Release date of the album or track. |
| `record_label` | Record company that released the album. |
| `duration_sec` | Duration of the track, in seconds. |
| `audio_dance` | How suitable the track is for dancing. |
| `audio_energy` | Energy and intensity of the track. |
| `audio_key` | Musical key of the track, encoded as an integer. |
| `audio_loudness` | Overall loudness, in decibels. |
| `audio_mode` | Whether the track is in a major or minor key. |
| `audio_speech` | Amount of speech-like content in the track. |
| `audio_acoustic` | Likelihood that the track is acoustic. |
| `audio_instrumental` | Likelihood that the track is instrumental. |
| `audio_live` | Likelihood that the track was recorded live. |
| `audio_valence` | How happy or sad the track sounds. |
| `audio_tempo` | Tempo of the track, in beats per minute. |
| `time_signature` | Time signature, in beats per bar. |
| `artist_name` | Name of the primary artist credited on the track. |
| `artist_genres` | List of genres associated with the artist, separated by `\|`. |
| `artist_followers` | Number of users following the artist on the platform. |
| `explicit_lyrics` | Whether the track contains explicit lyrics. |
| `music_hit` | Target: 1 for a music hit and 0 otherwise; present in the training set. |
