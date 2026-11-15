# Dataset

According to the competition description, the dataset consists of:

- `train.csv`: track identifiers, features, and the `music_hit` target (1 for a music hit and 0 otherwise).
- `test.csv`: track identifiers and features without the target. It is used to generate predictions for submission.
- `sample_submission.csv`: an example of the submission format.

The currently available [`project_data.csv`](project_data.csv) file contains 87,513 rows and the columns `id` and `music_hit`. The `music_hit` values are decimals between 0 and 1, so the file appears to be a submission or sample submission; it does not contain the features needed to train a model. The files `train.csv`, `test.csv`, and `sample_submission.csv` have not been found in this folder.

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
