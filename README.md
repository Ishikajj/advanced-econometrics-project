# Haushofer & Shapiro (QJE 2016) — Python Replication

Replication and extension of *The Short-Term Impact of Unconditional Cash Transfers to the Poor* (Haushofer & Shapiro, QJE 2016). RCT of GiveDirectly UCTs in rural Kenya (~1,440 households).

---

## Notebooks

### `dataviewing.ipynb` — Main replication
Replicates Tables 1–6 from the paper:
- **Table 1**: Baseline balance checks
- **Table 2**: Main treatment effects on 8 summary indices (assets, consumption, food security, health, education, psychological well-being, enterprise, intrahousehold empowerment)
- **Table 4**: Psychological well-being outcomes (individual-level)
- **Tables 5–6**: Consumption, assets, and enterprise breakdowns
- **Section 9**: New analysis — heterogeneous treatment effects by baseline wealth (treatment × baseline interaction)

### `monthly_small_timing_bins.ipynb` — Timing analysis
Focuses on the **monthly-small transfer arm only**. Uses ANCOVA timing-bin regressions to test whether material gains (assets + food security) appear earlier than psychological gains across bins defined by months elapsed since last transfer (`Dlastend`). Reference category: `<1 month`.

### `monthly_small_pca.ipynb` — PCA welfare index
Applies **PCA** to four endline outcomes (assets, food security, consumption, psychological well-being) in the monthly-small arm to construct a data-driven welfare composite. Regresses PC1 scores on timing bins and continuous elapsed months to summarise joint welfare dynamics and assess whether adjustment is material-led or synchronised.

---

## Setup

### Data
The `correction/` folder is not tracked by git (it's in `.gitignore`). You need to obtain the datasets separately and place them here locally:
```
correction/Data/
    UCT_FINAL_CLEAN.dta       <- main dataset (required by all notebooks)
    UCT_MetalRoofHHs.dta
    UCT_UNMATCHED.dta
    UCT_Village_Collapsed.dta
```

The datasets are available from the [Harvard Dataverse replication package](https://dataverse.harvard.edu/dataset.xhtml?persistentId=doi:10.7910/DVN/LGGUA4). Create the `correction/Data/` directory inside the repo root and put the `.dta` files there before running any notebook.

### Environment

Dependencies are declared in `pyproject.toml`. The recommended way is with `uv` (already set up in this repo):

```bash
uv sync
uv run jupyter notebook
```

Or with plain pip + venv:

```bash
python -m venv .venv
source .venv/bin/activate   # Windows: .venv\Scripts\activate
pip install -e .
jupyter notebook
```

### Running

Run cells top to bottom in each notebook.

All three notebooks are self-contained and independent of each other.
