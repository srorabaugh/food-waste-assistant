# Food Waste Reduction Assistant

An early-stage ingredient-based recipe recommendation project built with Python, pandas, and Jupyter. The goal is to help people use food they already have, reduce waste, and credit original Food.com recipe authors.

## Current checkpoint

The notebooks in `notebooks/` capture the **current prototype**, including known bugs. Notebook outputs were excluded from this upload; the source code is preserved.

- `notebooks/data_exploration.ipynb`: load the Food.com/Kaggle recipes CSV, select useful columns (including `RecipeId`, `AuthorName`, `AggregatedRating`, and `ReviewCount`), clean ingredient strings, and save `cleaned_recipes.csv`.
- `notebooks/ingredient_matching.ipynb`: parse ingredient strings, calculate pantry ingredient overlap, rank candidate recipes using ratings and review counts, and attempt strict pantry-only filtering.

## Fixes in this checkpoint

- Parse the original R-style ingredient vectors without stripping legitimate leading letters.
- Recompute match scores and strict filtering together from the current pantry.
- Use a review-count Bayesian shrinkage score (default prior strength: 20 reviews).
- Display missing ingredients and add small notebook smoke tests.

These changes have **not been run against the full downloaded dataset** because that CSV was not provided here. Run both notebooks in order locally to validate end-to-end behavior.

## Remaining work

1. Run the notebooks against the full downloaded dataset and inspect the strict match count.
2. Add original recipe links and creator attribution in the interface.
3. Improve ingredient synonyms and pantry matching (e.g., sugar vs granulated sugar).
4. Move reusable functions into `src/`, expand tests, and build an interface.

## Setup

```bash
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
cd notebooks
jupyter notebook
```

Download the Food.com/Kaggle recipe dataset separately and place it at `data/recipes.csv` in the repository root. Run the exploration notebook before the matching notebook. Dataset files and virtual environments are ignored by Git. Review the source dataset's license and terms before redistributing it.

**Status:** learning project / work in progress; the recommendation results have not yet been validated.
