# Missing text metadata

We studied missing values in `track_name`, `album_name`, and `record_label` in the original training and test data. We treated null values, empty strings, and whitespace-only fields as missing.

| Dataset | Column | Missing values | Missing (%) |
| --- | --- | ---: | ---: |
| train | `track_name` | 4 | 0.0011 |
| train | `album_name` | 1 | 0.0003 |
| train | `record_label` | 38 | 0.0109 |
| test | `track_name` | 1 | 0.0011 |
| test | `album_name` | 0 | 0.0000 |
| test | `record_label` | 14 | 0.0160 |

## Decision

We replaced missing values in these three columns with `unknown` in copies of both datasets. We retained every track because the remaining metadata and audio features can still be used. We preserved non-missing text, including existing names such as `Unknown`, and left the raw CSV files unchanged. This preparation does not require target information or statistics learned from either dataset.

Our working notebook keeps the cleaned copies in memory. We included the same transformation in `delivery/music_hit_prediction.ipynb`, before genre encoding. Whether to use these text columns as model features remains a separate modeling decision.
