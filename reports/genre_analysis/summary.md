# Genre frequency analysis

We analyzed `train.csv` using `notebooks/01_genre_analysis.ipynb`.

- Track rows: 350,051
- Tracks with known genres: 187,459
- Tracks without genres: 162,592 (46.45%)
- Distinct genres: 3,886

We counted each genre once per track row, so our frequencies reflect tracks rather than unique artists.
A track may contribute to multiple genres, so percentages do not sum to 100%.

## Most frequent genres

| Genre | Tracks | % of all tracks |
| --- | ---: | ---: |
| karaoke | 13,491 | 3.85% |
| rap | 12,524 | 3.58% |
| pop | 12,240 | 3.50% |
| rock | 11,691 | 3.34% |
| hip hop | 9,231 | 2.64% |
| classical | 7,327 | 2.09% |
| pop rap | 6,908 | 1.97% |
| dance pop | 6,489 | 1.85% |
| trap | 4,942 | 1.41% |
| classic rock | 4,661 | 1.33% |
| album rock | 4,263 | 1.22% |
| r&b | 4,171 | 1.19% |
| soul | 3,855 | 1.10% |
| urban contemporary | 3,775 | 1.08% |
| country | 3,684 | 1.05% |
| hard rock | 3,601 | 1.03% |
| baroque | 3,259 | 0.93% |
| edm | 3,236 | 0.92% |
| early music | 3,150 | 0.90% |
| sleep | 3,141 | 0.90% |

## Selection coverage

We calculated both coverage percentages using only tracks with known genres.
At least one selected genre does not mean all of a track's genres are represented.

| Rule | Genre columns | At least one genre covered | All genres covered |
| --- | ---: | ---: | ---: |
| top_10 | 10 | 30.88% | 9.34% |
| top_25 | 25 | 38.80% | 13.43% |
| top_50 | 50 | 45.23% | 20.65% |
| top_100 | 100 | 52.46% | 32.99% |
| top_200 | 200 | 62.22% | 46.06% |
| top_500 | 500 | 77.66% | 66.54% |
| top_1000 | 1000 | 88.70% | 81.37% |
| min_50_tracks | 1094 | 89.94% | 83.34% |
| min_100_tracks | 664 | 82.45% | 72.78% |
| min_250_tracks | 326 | 70.96% | 56.64% |
| min_500_tracks | 176 | 61.03% | 43.24% |
| min_1000_tracks | 84 | 50.18% | 28.35% |
| all_genres | 3886 | 100.00% | 100.00% |

## Initial decision

We selected the 1,000 most frequent genres as an initial preparation choice, reducing the number of genre columns from 3,886 to 1,000. Among tracks with known genres, 88.70% retain at least one genre and 81.37% retain all their genres. We flagged tracks without genre information with `genre_unknown`. We chose this initial trade-off between coverage and the number of features; its effect on model performance still needs to be checked using validation ROC AUC.

We will compare vocabulary sizes using validation ROC AUC before making our final selection.
During model evaluation, we will calculate genre frequencies using only the training split and apply the resulting vocabulary to validation data.
