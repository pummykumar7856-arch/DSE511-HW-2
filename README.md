# Life Expectancy in 2020

A short EDA for DSE 511 Homework 2, comparing life expectancy across countries and territories in 2020.

## Dataset

[Our World in Data — Life expectancy](https://ourworldindata.org/grapher/life-expectancy), accessed **September 15, 2026**. The 2020 data comes from United Nations, Department of Economic and Social Affairs, Population Division (2024), *World Population Prospects 2024, Online Edition*, processed by OWID.

Life expectancy at birth summarizes how long people would live under the mortality rates observed that year.

| Original column | Cleaned column | Description |
| --- | --- | --- |
| `Entity` | `country` | Country or territory name |
| `Code` | `code` | Country/territory code |
| `Year` | `year` | Observation year (2020) |
| `Life expectancy` | `life_expectancy` | Life expectancy at birth, in years |

## Run the notebook

Install the dependencies with `python -m pip install -r requirements.txt`, then open `notebooks/DSE-511-ASSIGNMENT-2.ipynb` in Jupyter or VS Code and run all cells using that Python environment. The analysis was run with Python 3.13.

The notebook uses paths relative to `notebooks/`, so use that folder as the kernel's working directory. It reads the saved source CSV and runs without internet access.

## Cleaning and analysis

The source snapshot in `data/life_expectancy_2020_source.csv` contains 261 observations for 2020. We keep three-letter country/territory codes and Kosovo (`OWID_KOS`), removing 24 regional and income-group aggregates. We rename the columns and drop missing values and exact duplicates; neither of those last two steps removes any retained rows.

The resulting 237 rows are saved in `data/cleaned_life_expectancy_2020.csv`. The notebook reports count, mean, median, sample standard deviation, minimum, and maximum, followed by a top-ten bar chart and a histogram.

The snapshot was obtained by downloading the [OWID CSV](https://ourworldindata.org/grapher/life-expectancy.csv) and selecting `Year == 2020`. To repeat the download from the notebook folder:

```python
source = pd.read_csv(
    "https://ourworldindata.org/grapher/life-expectancy.csv",
    storage_options={"User-Agent": "Mozilla/5.0"},
)
source[source["Year"] == 2020].to_csv(
    "../data/life_expectancy_2020_source.csv", index=False
)
```

The header avoids the HTTP 403 encountered with the default request. If refreshing the snapshot, rerun the analysis and update the access date and findings.

## Findings

Mean life expectancy was **72.89 years**, the median was **73.83**, and the sample standard deviation was **7.32**. Values ranged from **50.60 years** in the Central African Republic to **86.09** in Monaco.

Countries and territories receive equal weight, so this mean is not population-weighted world life expectancy. A single year's data cannot show trends or explain the causes of differences.

## Contributions

- **Pummy Kumar** (`pummykumar7856-arch`): created the repository and initial README; added the OWID download, 2020 subset, missing-value and duplicate checks, descriptive statistics, and top-ten plots. Later added a US life expectancy plot for 2015–2023 and updated the README. These changes were merged through PRs #1 and #2 from the `pummy` branch.
- **Kevin Li** (`pricyspark`): fixed the CSV download's HTTP 403 error; improved filtering to remove regional and income-group aggregates while retaining Kosovo; saved source and cleaned CSVs in `data/`; displayed the summary statistics together; added a histogram, concise notebook sections, and findings. Expanded the README with the source citation, variable descriptions, cleaning steps, and run instructions; added dependencies and `.gitignore`. Created the merge-conflict resolution commit `18f4054` and merged the work through PR #3 from `finish-eda`.

The final documentation and merge conflicts were inspected with Codex and verified manually.
The Jupyter Notebook notebooks/DSE-511-ASSIGNMENT-2.ipynb contains the code created to explore the life expectancy dataset.
The notebook opens the life expectancy dataset, produces statistical summaries, and subsets the data to provide a visualization of the top 10 countries with the highest life expectancy in the year 2020.
Added code to produce a time series plot of life expectancy for the USA.
