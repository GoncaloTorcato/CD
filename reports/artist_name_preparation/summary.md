# Artist name whitespace preparation

We examined surrounding whitespace in `artist_name` and compared follower counts for the affected names.

| Dataset | Rows with surrounding spaces | Distinct affected names |
| --- | ---: | ---: |
| train | 34 | 2 |
| test | 9 | 2 |

| Original name | Trimmed name | Tracks across train and test | Follower counts | Existing rows without spaces |
| --- | --- | ---: | --- | ---: |
| `'Raven Black '` | Raven Black | 11 | 21127 | 0 |
| `'Workout Music '` | Workout Music | 32 | 72649 | 0 |

## Decision

We removed leading and trailing whitespace from `artist_name` in copies of both datasets. We preserved internal spaces, capitalization, accents, missing values, followers, and all other columns. The affected names have consistent follower counts, and neither name has an existing version without surrounding spaces. This operation therefore standardizes the names without merging existing name variants. We did not infer artist identity or fill genre information from names.

We included the same transformation in `delivery/music_hit_prediction.ipynb`. Our working notebook keeps the cleaned frames in memory and leaves the raw CSV files unchanged.
