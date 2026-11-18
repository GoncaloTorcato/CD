# Logistic regression on the prepared datasets

We evaluated one fixed logistic regression configuration using only `data/processed/train.csv` and `data/processed/test.csv`. We used the existing cleaning and feature-engineering results without rebuilding them or comparing alternative feature sets.

## Inputs and features

The prepared training file contains 350,049 labeled rows and the test file contains 87,513 unlabeled rows. We used the prepared audio features, duration, release year, logarithmic followers, explicit-lyrics status, album type, musical key, mode, time signature, all existing genre indicators, and target-encoded record label. We kept original followers, IDs, titles, and artist names in the files but excluded them from model inputs. The target `music_hit` was used only as the response variable.

## Validation

We used a fixed group-aware split with 280,031 training rows and 70,018 validation rows. Identical prepared predictor rows share a group and cannot cross the split. We stratified groups by their majority label using random state 0; mixed-label ties were assigned to class 1. We fitted numerical imputation, continuous-feature scaling, small-category encoding, and record-label target encoding only on the training partition. The genre columns were already selected during preparation of the full training CSV, before this split. Our scores therefore evaluate the current prepared dataset rather than independently validating that earlier vocabulary-selection decision. We treat this reused development split as exploratory validation rather than an independent final estimate.

We used regularized logistic regression with C=1, the lbfgs solver, a maximum of 1,000 iterations, and threshold 0.5 for label-based metrics. We used neither class weighting nor resampling.

## Record-label encoding

We added one smoothed hit-rate feature for the record label. We generated its training values through five internal group-aware folds, so neither a training row nor its duplicate group contributes labels to its own encoded value. We fitted a separate encoder on the complete training partition to transform validation rows, using the training hit rate for unknown labels. The rates are between 0 and 1 before standardization; the scaled model input can be negative or exceed 1. The encoder and scaler are saved with the model and refitted on all prepared training data for final test prediction. We kept `record_label` as text in the prepared CSV files because this supervised transformation belongs inside model fitting.

## Results

| ROC AUC | Average precision | Accuracy | Precision | Recall | F1 | Training ROC AUC |
| ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| 0.94094 | 0.70659 | 0.93156 | 0.71958 | 0.55328 | 0.62557 | 0.94278 |

## Final model and predictions

We refitted the same configuration and its model-time preprocessing on all prepared training rows, then generated 87,513 probabilities for the prepared test file. We saved them to `delivery/predictions.csv` and saved the fitted model and feature map to `models/logistic_regression.joblib`. The competition test file has no target, so the reported metrics come from the validation partition. We did not alter the prepared CSV files or submit the predictions.
