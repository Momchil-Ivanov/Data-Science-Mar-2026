# Clinical Trial Footprint vs. Population Structure

A data science project analyzing how clinical trials are distributed globally relative to population size and economic development.

## Research Questions

1. How many trials per million inhabitants do different countries have, and how does this differ between rich and poor countries?
2. Does a larger population proportionally lead to more trials, or is the relationship sub/super-linear?
3. Is there a systematic difference in trial density between world regions (Europe, Africa, Asia, etc.)?
4. How has the picture changed over time (2000–2024)?

## Data Sources

- **ClinicalTrials.gov API** — trial metadata aggregated by country (`https://clinicaltrials.gov/api/v2/`)
- **World Bank API** — population, GDP per capita, region, income group (`https://api.worldbank.org/v2/`)

## Setup

```bash
pip install -r requirements.txt
jupyter notebook notebook.ipynb
```

## Structure

```
.
├── notebook.ipynb        # Main analysis notebook
├── requirements.txt      # Python dependencies
└── README.md
```

> **Reproducibility note:** No data files are stored in this repository. All data is fetched from public APIs at runtime. Running Section 1 of the notebook from top to bottom recreates the full dataset.

## Methods

| Research Question | Statistical Method |
|---|---|
| Trial density by income group | Kruskal-Wallis H test, pairwise Mann-Whitney U (Bonferroni-corrected) |
| Population vs. trial count | Log-log OLS regression, t-test of slope β against proportionality (β = 1) |
| Regional inequality | Lorenz curve, Gini coefficient, Kruskal-Wallis H test |
| Temporal trends | OLS linear trend on High / Low income trial-density ratio (2000–2024) |

## Author

Final exam project for Data Science course, March 2026.
