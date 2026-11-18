# Record-label target encoding

We studied the prepared `record_label` column and compared the existing logistic regression with the same model plus one encoded label feature. Both configurations used the same prepared data, outer validation split, model settings, and threshold of 0.5.

## Dataset profile

| Dataset | Distinct record labels | Missing | Unknown | Labels with one track |
| --- | ---: | ---: | ---: | ---: |
| train | 31559 | 0 | 38 | 14006 |
| test | 17781 | 0 | 14 | 7563 |

## Encoding

We represented each label through a smoothed estimate of its hit rate. We cross-fitted training values using five internal folds with identical predictor groups kept together. We fitted an encoder only on the complete training partition for validation, with unseen categories receiving the training hit rate. We did not use validation targets to calculate encodings. The rates are in [0, 1] before a StandardScaler fitted on cross-fitted training values.

## Validation comparison

| Configuration | Accuracy | ROC AUC | Precision | Recall | F1 |
| --- | ---: | ---: | ---: | ---: | ---: |
| without_record_label | 0.92152 | 0.91643 | 0.68095 | 0.45252 | 0.54372 |
| with_record_label | 0.93156 | 0.94094 | 0.71958 | 0.55328 | 0.62557 |

## Decision

We retained record-label target encoding after accuracy increased by 1.004 percentage points and ROC AUC changed from 0.91643 to 0.94094 on this validation split. We integrated only the adopted configuration into notebooks 08 and delivery. We kept the supervised encoding inside model fitting and left raw and prepared CSV files unchanged. We saved the encoder and scaler with the classifier for inference.

This comparison uses a reused development holdout, so it is exploratory evidence rather than an independent final performance estimate. The fixed genre columns were selected earlier during prepared-data construction.
