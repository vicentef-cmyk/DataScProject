# Agricultural Water Decoupling in France

**A regional analysis of agricultural production and water withdrawals in metropolitan France (2010–2022)**

## Research question

**Has agricultural water use become decoupled from agricultural production in France?**

This project investigates whether changes in agricultural production have been accompanied by proportional changes in agricultural freshwater withdrawals. It combines official French water and agricultural statistics to examine national trends and differences among the **13 metropolitan regions**.

The analysis is descriptive: it identifies patterns of decoupling but does not establish their causes.

## Research hypotheses

- **H1:** Agricultural water withdrawal intensity has decreased over time in at least some French regions.
- **H2:** Improvements in water withdrawal intensity do not necessarily translate into reductions in total agricultural water withdrawals.
- **H3:** The relationship between agricultural production and water withdrawals varies substantially across French regions.

## Data sources

| Source | Data used | Role in the analysis |
|---|---|---|
| **BNPE** (Banque Nationale des Prélèvements quantitatifs en Eau), accessed through [data.gouv.fr](https://www.data.gouv.fr/fr/datasets/67cad6eb1b824c076b3a4b79/) | Annual water withdrawals by region and use, in m³ | Agricultural water withdrawals, combining surface water and groundwater |
| **Agreste** — regional agricultural economic accounts | Agricultural production excluding subsidies, including annual volume indices | Estimate agricultural production in constant 2010 euros |
| **French regional boundaries (GeoJSON)** | Geographic boundaries and region codes | Maps and geographic matching |

The water indicator covers **withdrawals subject to abstraction fees**. Withdrawals are not equivalent to water consumption.

The BNPE dataset includes years from 2008 to 2022, used for the initial spatial comparison. The combined production–water analysis covers **2010–2022**.

## Methodology

1. **Prepare water data:** filter BNPE records to agricultural use and sum withdrawals across water types for each region and year.
2. **Prepare production data:** select total agricultural production from Agreste's regional accounts and chain annual volume indices to estimate production at constant 2010 prices.
3. **Integrate datasets:** harmonize regional codes and merge production and withdrawal observations for 13 regions over 13 years (**169 region-year observations**).
4. **Calculate economic water productivity:** divide real agricultural production (EUR at 2010 prices) by agricultural water withdrawals (m³).
5. **Assess decoupling:** compare three-year period averages of real production and withdrawals, distinguishing absolute decoupling, relative decoupling, contraction with lower withdrawals, and no decoupling.
6. **Test temporal sensitivity:** compare alternative baseline and end periods to assess how robust regional classifications are.

**Economic water productivity** is an aggregate economic indicator (EUR/m³), **not** a direct measure of technical irrigation efficiency. Water withdrawal intensity is its inverse.

### Temporal comparisons

| Scenario | Baseline | Final period |
|---|---|---|
| Main | 2010–2012 | 2020–2022 |
| Pre-2020 | 2010–2012 | 2017–2019 |
| Alternative baseline | 2013–2015 | 2020–2022 |

## Key findings

### National results

| Comparison | Real agricultural production | Water withdrawals | Economic water productivity | Classification |
|---|---:|---:|---:|---|
| 2010–2012 vs. 2020–2022 | +0.17% | +5.45% | −5.01% | No decoupling |
| 2010–2012 vs. 2017–2019 | +1.21% | +0.79% | +0.42% | Relative decoupling |
| 2013–2015 vs. 2020–2022 | −2.27% | +16.67% | −16.24% | No decoupling |

The main comparison shows **no national decoupling**: water withdrawals increased faster than real agricultural production. The pre-2020 comparison instead suggests a small degree of relative decoupling, illustrating the sensitivity of conclusions to the observation window.

### Regional results

- **Bretagne** exhibited **absolute decoupling** in the main comparison: real production increased by **2.7%** while withdrawals decreased by **21.3%**. Economic water productivity rose by approximately **30.5%**.
- **10 of 13 regions** were classified as showing **no decoupling** in the main comparison.
- **9 of 13 regions** retained the same classification across all three temporal comparisons.

**Overall conclusion:** The evidence does not indicate widespread, sustained decoupling of agricultural water withdrawals from agricultural production across metropolitan France over the study period. Regional differences are important, and the findings depend partly on the selected comparison years.

## Project structure

```text
Project Vicente 2026/
├── data/
│   ├── raw/
│   │   ├── prelevements-d-eau-par-usage-region.csv
│   │   ├── SériesComptesRégionaux_2010-2025_départementales_et_régionales.xlsx
│   │   └── regions.geojson
│   └── processed/
├── notebooks/
│   └── analysis.ipynb
├── .gitignore
└── README.md
```

The notebook is the main deliverable and contains the data preparation, visualizations, regional analysis, sensitivity tests, discussion, limitations, and conclusion.

## How to run

1. Clone or download the repository and open the project folder in **VS Code**.
2. Create a Python environment and install the packages used in the notebook:

   ```bash
   python -m pip install pandas numpy matplotlib geopandas mapclassify openpyxl jupyter ipykernel
   ```

3. Ensure the three source files listed above are available under `data/raw/`. If they are not included in the repository, obtain them from the cited sources.
4. Open `notebooks/analysis.ipynb` and select the project's Python kernel.
5. Run the notebook from top to bottom (**Restart Kernel and Run All Cells**).

The notebook uses relative paths such as `../data/raw`, so run it with `notebooks/` as its working directory.

## Limitations

- **Data reliability:** the official description of the BNPE indicator states that its data are considered reliable up to **2020**; therefore, 2021–2022 results require caution.
- **Climatic variability:** drought and precipitation affect annual irrigation demand; three-year averages reduce, but do not eliminate, this variability.
- **Agricultural specialization:** differences in crops, livestock, and production structures limit direct comparisons of economic water productivity between regions.
- **Withdrawal versus consumption:** the water indicator measures reported withdrawals subject to abstraction fees, not all water use or net water consumption.
- **No causal inference:** the analysis cannot determine whether observed patterns are caused by technology, policy, farm practices, or climate.

## Tools

Python · Pandas · Matplotlib · GeoPandas · Jupyter Notebook · VS Code · Git/GitHub

## Further research

Future work could incorporate regional precipitation, temperature, drought indicators, irrigated area, crop mix, and water-management policies to investigate **why** decoupling patterns differ among French regions.
