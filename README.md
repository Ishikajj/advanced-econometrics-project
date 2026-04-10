# Advanced Econometrics Project

This repository contains a replication and extension of **Haushofer & Shapiro (2016), _The Short-Term Impact of Unconditional Cash Transfers to the Poor: Experimental Evidence from Kenya_**. The project reproduces core treatment-effect results from the public replication data and adds extension analyses on heterogeneity, timing, and the joint evolution of material and psychological outcomes.

The repository includes:
- a main replication notebook for data cleaning, sample construction, and treatment-effect estimation,
- a timing-bin ANCOVA notebook focused on the monthly-small transfer arm,
- a PCA notebook that studies whether material and psychological outcomes move together as a common welfare dimension,
- generated figures used in the project write-up.

The main replication notebook explicitly covers data loading, baseline balance, main treatment effects, heterogeneity by recipient gender / transfer timing / transfer size, psychological outcomes, consumption outcomes, assets and enterprise outcomes, and a new extension on heterogeneity by baseline wealth. The public dataset used in the notebook has shape **(2880, 981)** in the current workflow. See the notebook headers and outputs in the repository files. 

## Data source

The raw replication data are **not stored in this GitHub repository**. Users should download them manually from the Harvard Dataverse dataset:
https://dataverse.harvard.edu/dataset.xhtml?persistentId=doi:10.7910/DVN/M2GAZN 

### How to download the data

1. Open the Harvard Dataverse dataset page for DOI `10.7910/DVN/M2GAZN` in a browser.
2. Download the replication dataset files manually.
3. Locate the cleaned Stata data file used by this project: `UCT_FINAL_CLEAN.dta`.
4. Inside the repository, create the following folder structure:

```text
advanced-econometrics-project/
└── Correction/
    └── Data/
        └── UCT_FINAL_CLEAN.dta
```

The analysis notebooks explicitly read the dataset from `Correction/Data/UCT_FINAL_CLEAN.dta`. Both extension notebooks check for that directory and then load the Stata file from exactly that path.
## Setup

### Option 1: using `uv`

```bash
uv sync
uv add scikit-learn
```

### Option 2: using `pip`

```bash
python -m venv .venv
source .venv/bin/activate  # macOS / Linux
pip install -U pip
pip install ipykernel jupyter matplotlib pandas pyreadstat seaborn statsmodels scikit-learn
```

The `pyproject.toml` currently lists `ipykernel`, `jupyter`, `matplotlib`, `pandas`, `pyreadstat`, `seaborn`, and `statsmodels`, with Python `>=3.13`. The PCA notebook also imports `sklearn.preprocessing.StandardScaler` and `sklearn.decomposition.PCA`, so `scikit-learn` should be installed as well.

## How to run the project

Start Jupyter from the repository root:

```bash
jupyter notebook
```

Recommended order:

### 1. `dataviewing.ipynb`
Use this notebook for the main replication workflow. It includes:
- data loading and exploration,
- sample preparation,
- baseline balance,
- main treatment effects,
- heterogeneity by treatment design,
- psychological outcomes,
- consumption outcomes,
- assets and enterprise outcomes,
- heterogeneity by baseline wealth.

This is the best notebook to open first if you want the full project overview. 

### 2. `monthly_small_timing_bins.ipynb`
Use this notebook for the timing extension. It:
- restricts the sample to the **monthly-small** treatment arm,
- builds timing bins from `Dlastend`,
- constructs a material index from baseline-standardized assets and food security,
- estimates ANCOVA-style regressions for material and psychological outcomes.

Its purpose is to test whether material and psychological gains arrive at different times after treatment. 

### 3. `monthly_small_pca.ipynb`
Use this notebook for the latent-dimension extension. It:
- keeps the monthly-small arm,
- baseline-standardizes four endline outcomes,
- runs PCA on assets, food security, consumption, and psychological well-being,
- examines whether the first principal component captures a common welfare process,
- relates PCA scores to elapsed time since transfer.

This notebook is the natural follow-up once the timing-bin results are understood.


## Outputs

The repository includes two saved figures:
- `treatment_effects.png`
- `hetero_treatment_effects.png`
