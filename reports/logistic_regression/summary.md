# Logistic regression on the prepared datasets

We evaluated one fixed logistic regression configuration using only `data/processed/train.csv` and `data/processed/test.csv`. We used the existing cleaning and feature-engineering results without rebuilding them or comparing alternative feature sets.

## Inputs and features

The prepared training file contains 350,049 labeled rows and the test file contains 87,513 unlabeled rows. We used the prepared audio features, duration, release year, logarithmic followers, explicit-lyrics status, album type, musical key, mode, time signature, and all existing genre indicator columns. We kept original followers, IDs, titles, artist names, and record labels in the files but excluded them from model inputs. The target `music_hit` was used only as the response variable.

## Validation

We used a fixed group-aware split with 280,031 training rows and 70,018 validation rows. Identical prepared predictor rows share a group and cannot cross the split. We stratified groups by their majority label using random state 0; mixed-label ties were assigned to class 1. We fitted numerical imputation, continuous-feature scaling, and categorical encoding only on the training partition. The genre columns were already selected during preparation of the full training CSV, before this split. Our scores therefore evaluate the current prepared dataset rather than independently validating that earlier vocabulary-selection decision. We treat this reused development split as exploratory validation rather than an independent final estimate.

We used regularized logistic regression with C=1, the lbfgs solver, a maximum of 1,000 iterations, and threshold 0.5 for label-based metrics. We used neither class weighting nor resampling.

## Results

| ROC AUC | Average precision | Accuracy | Precision | Recall | F1 | Training ROC AUC |
| ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| 0.91643 | 0.62718 | 0.92152 | 0.68095 | 0.45252 | 0.54372 | 0.92014 |

## Final model and predictions

We refitted the same configuration and its model-time preprocessing on all prepared training rows, then generated 87,513 probabilities for the prepared test file. We saved them to `delivery/predictions.csv` and saved the fitted model and feature map to `models/logistic_regression.joblib`. The competition test file has no target, so the reported metrics come from the validation partition. We did not alter the prepared CSV files or submit the predictions.
