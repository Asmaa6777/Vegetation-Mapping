# Vegetation Mapping

This repository contains a notebook-based solution for a vegetation classification challenge. The current workflow trains a multiclass `CatBoostClassifier` on tabular remote-sensing features and generates a submission file with class probabilities for each test sample.

## Repository Contents

- `022 (1).ipynb`: main experimentation notebook.
- `_022_.ipynb`: alternate version of the same workflow with inline `pip install`.
- `Train (6).csv`: training data with labels.
- `Test (4).csv`: test data used for inference.
- `inegi-gcim-vegetation-mapping-challenge20240902-4068-72kg7v (1).zip`: original challenge archive containing `Train.csv`, `Test.csv`, and `SampleSubmission.csv`.

## Dataset Overview

- Training set: 2,123 rows and 43 columns.
- Test set: 923 rows and 42 columns.
- Feature layout: `id`, spectral reflectance bands (`REFLEC*`), principal components (`PCA*`), vegetation and water indices, and radar-derived features.
- Target column: `Target`.
- Number of classes in the training data: 45.
- Missing values: none in the training CSV, 41 empty cells in the test CSV.

## Current Modeling Workflow

The notebooks currently follow this sequence:

1. Load the CSV files.
2. Drop `id` and separate `Target`.
3. Remove outliers from the training set with `IsolationForest`.
4. Encode class labels with `LabelEncoder`.
5. Train a `CatBoostClassifier`.
6. Evaluate with log loss.
7. Build a submission table with per-class probabilities.

## Environment

Use Python 3 with these packages installed:

```bash
pip install numpy pandas matplotlib seaborn scikit-learn catboost jupyter
```

## How To Run

1. Open `022 (1).ipynb` in Jupyter Notebook or VS Code.
2. Update file-loading cells if you want to use the local CSVs instead of the hard-coded GitHub URLs.
3. Run the notebook cells in order.
4. Export the generated submission file after the final cell.

## Notes About The Current Notebooks

- Both notebooks read the dataset from external GitHub URLs even though local CSV copies are already in this repository.
- `_022_.ipynb` installs `catboost` inside the notebook with `!pip install catboost`.
- The submission code creates columns `Target_0` through `Target_124`, but the current training data contains 45 observed classes. Keep this aligned with the challenge submission format before final submission.
- The saved submission filename in the notebook has no `.csv` extension: `submission_3.332917153288488`.

