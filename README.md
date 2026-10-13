# Food Waste Reduction Assistant

An early-stage ingredient-based recipe recommendation project built with Python, pandas, and Jupyter. The goal is to help people use food they already have, reduce waste, and credit original Food.com recipe authors.

## Current checkpoint

The notebooks in `notebooks/` capture the **current prototype**, including known bugs. Notebook outputs were excluded from this upload; the source code is preserved.

- `notebooks/data_exploration.ipynb`: load the Food.com/Kaggle recipes CSV, select useful columns (including `RecipeId`, `AuthorName`, `AggregatedRating`, and `ReviewCount`), clean ingredient strings, and save `cleaned_recipes.csv`.
- `notebooks/ingredient_matching.ipynb`: parse ingredient strings, calculate pantry ingredient overlap, rank candidate recipes using ratings and review counts, and attempt strict pantry-only filtering.

## Known issues / next steps

1. **Fix ingredient parsing.** The original `RecipeIngredientParts` field contains R-style vectors such as `c("cinnamon", "salt")`. Cleaning punctuation first can produce `ccinnamon`, and removing the first `c` unconditionally can damage real ingredients. Parse the original field instead.
2. **Debug strict filtering.** Test `set(recipe_ingredients).issubset(user_ingredients)` on small examples; inspect matching counts and avoid stale notebook state.
3. Recompute match scores whenever the user's ingredient list changes.
4. Improve rating confidence with a stable Bayesian average based on review counts; avoid scaling by the largest review count in a filtered subset.
5. Add original recipe links, attribution, and missing-ingredient explanations.
6. Add tests, move reusable functions into `src/`, and eventually build a user interface.

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
