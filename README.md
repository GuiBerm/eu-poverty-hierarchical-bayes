# Hierarchical Bayesian Analysis of Regional Poverty and Social Exclusion in Europe

A Bayesian Data Analysis (BDA) project investigating whether regional household disposable income reduces poverty and social exclusion equally across European Union countries, or whether national welfare regimes flatten regional income gradients once urbanization is accounted for.

## Research Question
> Does higher regional disposable income protect against poverty and social exclusion (`ilc_peps11n`) equally across EU member states, or do country-level baselines and income sensitivities vary substantially across national welfare regimes?

## Dataset
Cross-sectional regional data from **Eurostat** for the reference year **2022**, covering **$N = 232$ NUTS-2 regions** nested within **$J = 27$ EU countries** (zero missing values):
* **Outcome (`housing_overburden` / `housing_overburden_scaled`):** 2022 At-Risk-of-Poverty or Social Exclusion rate (`ilc_peps11n`, % of population). *(Note: The CSV retains its initial working filename `eurostat_housing_2022.csv`.)*
* **Primary Predictor (`disposable_income` / `disposable_income_scaled`):** Regional net household disposable income per inhabitant (`nama_10r_2hhinc`, €).
* **Urbanization Control (`pop_density` $\rightarrow$ `log_pop_density_scaled`):** Regional population density (`demo_r_d3dens`, inhabitants/km²), natural-log transformed and globally standardized to reduce right-skewness ($\text{skew}: 5.61 \rightarrow 0.53$).

## Models
Implemented in Python using **Bambi** and **PyMC** with proper weakly informative priors:
1. **Model 1 (Pooled Baseline):** Complete-pooling Gaussian regression ignoring country boundaries.
2. **Model 2 (Hierarchical Varying Intercepts & Slopes):** Partial-pooling multilevel Gaussian regression allowing both baseline poverty rates ($\alpha_j$) and income slopes ($\beta_{\text{inc}, j}$) to vary by country $j \in \{1, \dots, 27\}$, linked via a multivariate normal population distribution.

## Repository Structure
```text
├── data/
│   └── eurostat_housing_2022.csv
├── notebooks/
│   └── 01_hierarchical_arope_bambi.ipynb
├── figures/
├── proposal/
│   └── project_proposal.md
├── requirements.txt
└── README.md
