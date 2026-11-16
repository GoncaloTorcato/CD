# Zero-duration training tracks

We examined zero, missing, and negative durations in the original training and test data.

| Dataset | Rows | Zero-second tracks | Zero-second tracks (%) | Missing durations | Negative durations |
| --- | ---: | ---: | ---: | ---: | ---: |
| train | 350,051 | 2 | 0.000571 | 0 | 0 |
| test | 87,513 | 0 | 0.000000 | 0 | 0 |

## Decision

We removed 2 training tracks with `duration_sec = 0`: `244276`, `287253`. A zero-second duration is suspicious metadata, and these records represent a negligible fraction of the training set. We retained every other training row and kept the original track identifiers and relative row order. We did not remove short non-zero tracks or apply a broader duration threshold.

Our prepared training set contains 350,049 rows. We retained all 87,513 test rows because each track requires a prediction. We included this training-only filter before the other preparation steps in `delivery/music_hit_prediction.ipynb`. The working notebook keeps its copies in memory; raw CSV files remain unchanged.
