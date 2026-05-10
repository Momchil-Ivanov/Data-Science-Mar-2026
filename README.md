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
├── notebook.ipynb           # Main analysis notebook
├── requirements.txt         # Python dependencies
├── README.md
└── data/
    ├── ct_raw.csv.gz        # Snapshot: ClinicalTrials.gov (study × country rows, gzip CSV)
    └── wb_snapshot.csv      # Snapshot: World Bank country metadata + 2023 population & GDP
```

> **Reproducibility note:** Committed files under `data/` freeze the raw API responses (ClinicalTrials.gov + World Bank extracts) so results do not drift when those services change downstream. The currently committed snapshots use the freeze/access date stated in Section 0 and References of the notebook. Section 1 loads from `data/` by default (`USE_CACHE = True` in Section 1.1). To refresh from the live APIs, set `USE_CACHE = False`, run Sections 1.1–1.2, commit the updated `data/` files, and update the snapshot/access date consistently in the notebook. **References** at the very end of the notebook lists formal citations for both APIs, representative prior literature from Section 0.3, and `requirements.txt`.

## Methods

| Research Question | Statistical Method |
|---|---|
| Trial density by income group | Kruskal-Wallis H test, pairwise Mann-Whitney U (Bonferroni-corrected) |
| Population vs. trial count | Log-log OLS regression, t-test of slope β against proportionality (β = 1) |
| Regional inequality | Lorenz curve, Gini coefficient, Kruskal-Wallis H test |
| Temporal trends | OLS linear trend on High / Low income trial-density ratio (2000–2024) |

## Author

Final exam project for Data Science course, March 2026.
