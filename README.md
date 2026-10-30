# Project: Real World Data Wrangling with Python

## Project summary

This project wrangles two related real-world datasets to answer the question **"Is GDP per capita a reliable predictor of national happiness, and how has this relationship evolved from 2015 to 2019 across world regions?"** The first dataset - the World Happiness Report country tables for 2015-2019 (Kaggle `unsdsn/world-happiness`) - is gathered by **programmatically downloading** five separate yearly CSV files with `requests` into `data/raw/`; the second - GDP per capita (current US$, World Bank indicator `NY.GDP.PCAP.CD`) - is gathered through an **API call** and parsed from JSON. Assessment documents four issues (one missing corruption-perception value in 2018, 31 country-name mismatches between sources, observations fragmented over five year tables, and 30 divergent column spellings across editions), and the cleaning resolves each of them (Region-median imputation, a curated country-name mapping with a `difflib` fuzzy fallback, a `Year` column plus `pd.concat` into one 782-row table, and a canonical rename), before dropping unnecessary variables and merging happiness with World Bank GDP on `Country` + `Year` (97.8% World Bank coverage). The raw and cleaned versions are kept side by side (`data/raw/happiness_2015..2019.csv`, `happiness_all_years_raw.csv`, `worldbank_gdp_raw.csv` and `data/clean/happiness_worldbank_cleaned.csv`), and the final analysis shows GDP per capita is a real but decelerating happiness predictor (2019 Pearson r = 0.74, flattening beyond ~$40k where Luxembourg scores only 7.09), with 2015-2019 gains concentrated in Central and Eastern Europe (+0.23) and Western Europe (+0.15) and declines in Latin America (-0.19), North America (-0.19) and the Middle East and North Africa (-0.17).

## How to run

1. Install the pinned dependencies: `pip install -r requirements.txt`
2. Execute the notebook top to bottom: `jupyter nbconvert --to notebook --execute --inplace data_wrangling_project_starter.ipynb`
   (the gathering cell re-downloads the raw files; on re-runs everything is idempotent)
3. Outputs land in `data/raw/` (original files) and `data/clean/` (merged cleaned dataset).

## Data sources

- World Happiness Report 2015-2019: <https://www.kaggle.com/datasets/unsdsn/world-happiness> (fetched via a public GitHub mirror of the same files)
- World Bank GDP per capita: <https://api.worldbank.org/v2/country/all/indicator/NY.GDP.PCAP.CD> (indicator `NY.GDP.PCAP.CD`, years 2015-2019)

## Files

- `data_wrangling_project_starter.ipynb` - the complete, executed project notebook (gather -> assess -> clean -> store -> visualize)
- `data/raw/` - raw downloaded/collected files (kept exactly as received, plus a combined raw version)
- `data/clean/` - the final cleaned + merged dataset
- `docs/` - Udacity project documentation and rubric
