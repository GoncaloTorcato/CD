# Artist follower transformation

We examined the distribution and validity of `artist_followers` in the original training and test datasets.

| Dataset | Missing | Negative | Zero |
| --- | ---: | ---: | ---: |
| train | 0 | 0 | 2468 |
| test | 0 | 0 | 612 |

| Dataset | Representation | Minimum | Median | 99th percentile | Maximum | Skewness |
| --- | --- | ---: | ---: | ---: | ---: | ---: |
| train | original | 0.0000 | 6418.0000 | 59152035.0000 | 115998928.0000 | 6.9070 |
| train | log1p | 0.0000 | 8.7670 | 17.8956 | 18.5691 | 0.1592 |
| test | original | 0.0000 | 6391.0000 | 71720409.0000 | 115998928.0000 | 6.8064 |
| test | log1p | 0.0000 | 8.7628 | 18.0883 | 18.5691 | 0.1655 |

## Initial decision

We added `artist_followers_log1p = ln(1 + artist_followers)` to both datasets. The logarithm compresses large follower counts while preserving their order, and the added 1 allows zero followers to map to zero.

We retained the original `artist_followers` column so we can compare the original and transformed representations during model evaluation. We did not remove popular artists, change follower counts, or fill missing values as part of this transformation. The formula uses no target information and requires no statistic fitted on training or test data. Its effect on model performance remains to be assessed using validation ROC AUC.

We included the same transformation in `delivery/music_hit_prediction.ipynb`. The working notebook keeps its copies in memory and leaves raw and existing processed CSV files unchanged. The delivery notebook can export the combined preparation to `data/processed/`.
