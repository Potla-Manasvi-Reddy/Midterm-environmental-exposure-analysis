# Demographics, Geography, and Diesel Particulate Matter

## Overview

This analysis examines how modeled diesel particulate matter (PM) differs with the share of residents of color across U.S. census tracts, using EPA EJScreen 2024 data. It asks how much of that gap remains after accounting for population density, income, and geographic location (EPA region), and whether the gap is the same in every region.

The analysis addresses three questions:

1. How strongly is the share of residents of color associated with modeled diesel PM?
2. How much of that association remains after adjusting for population density, low-income share, and EPA region?
3. Does the association differ across the ten EPA regions?

## Data

The analysis uses the EPA EJScreen 2024 (v2.32) census-tract dataset, available through Zenodo. Diesel PM values come from EPA's 2020 AirToxScreen model; demographics come from the 2018–2022 American Community Survey.

Tracts were kept if they had at least 100 residents, a diesel PM estimate, demographic data, and land area. This reduced the data from 86,082 to **84,222 census tracts** (49 states, D.C., and Puerto Rico). Of the 1,860 dropped tracts:

| Reason dropped | Tracts |
|---|---|
| Fewer than 100 residents | 993 |
| U.S. territories (no diesel model) | 686 |
| Alaska (no diesel model) | 177 |
| Other (missing data) | 4 |

The variables include log10 diesel PM (outcome), percent residents of color and percent low income (each per 10 percentage points), log10 population density, EPA region, and county (taken from the first five digits of the tract ID, used to cluster standard errors).

## Methodology

**Simple Linear Regression**

A simple linear regression (`m1`) estimates the association between the share of residents of color and log10 diesel PM. Because the outcome is on a log10 scale, coefficients are reported as percent changes in diesel PM per 10 percentage points.

**Multiple Linear Regression**

Density, income, and EPA region are added one at a time (`m2`–`m4`) to see how the people-of-color coefficient changes. `m4` is the main model. Two checks use it: centering the predictors (`m4c`) and changing the reference region from New England to the Southeast (`m4_rl`). Variance inflation factors check whether predictors are too correlated to separate.

**Geographic Analysis**

EPA region enters as a categorical predictor, with New England as the reference. An interaction model (`m5`, `poc10 * region`) lets the people-of-color slope differ by region and is compared with `m4` using `anova()`. The model is also fit separately within each region as a robustness check.

**Effect Sizes and Inference**

Effect sizes include standardized coefficients, Cohen's f², and an interquartile comparison in real units. Because neighboring tracts are not independent, all confidence intervals are clustered by county.

**Logistic Regression**

A logistic model (`m_logit`) asks whether a tract is in the national top 20% for diesel PM (EPA's 80th-percentile screening cutoff), using the same predictors as `m4`. Results are checked at the 70th, 90th, and 95th percentiles, and calibration and linearity are assessed.

## Results

| Metric | Estimate |
|---|---|
| Unadjusted association (`m1`) | +10.6% diesel PM per +10 pts residents of color |
| `m1` R² | 0.158 |
| After adding density (`m2`) | +0.8% (95% CI: −0.4% to 2.0%) |
| After adding income (`m3`) | +2.5% (95% CI: 1.2% to 3.9%) |
| After adding region (`m4`, main model) | **+2.9% (95% CI: 1.9% to 3.8%)** |
| `m4` R² | 0.642 |
| Region effect vs. New England | +9.5% (Mountains & Plains) to +50.5% (Pacific Northwest) |
| Regions with a positive association (within-region fits) | 7 of 10 |
| Steepest regional gaps | Mountains & Plains 9.0%; Pacific Northwest 8.5% |
| Regions with essentially no gap | NY/NJ/PR 0.0%; South Central −0.5% |
| Interaction model (`m5`) adjusted R² | 0.642 → 0.650 (F = 206.9) |
| Cohen's f² | Density 1.046; Region 0.046; Income 0.032; Race 0.017 |
| Logistic odds ratio (top 20%) | 1.18 per +10 pts (95% CI: 1.11 to 1.26) |

Tracts with more residents of color have more modeled diesel PM. Population density explains most of this association, but not all of it: after adjusting for density, income, and EPA region, each additional 10 percentage points of residents of color is associated with 2.9% more diesel PM. Adding income increased the coefficient (suppression), because lower-income tracts have slightly less diesel PM at the same density.

Every EPA region has more diesel PM than New England at the same demographics, density, and income, but adding region barely changed the people-of-color coefficient (2.5% to 2.9%). Region shifts the overall level of diesel PM without explaining away the demographic gap.

The gap itself differs by region. It is strongest in Mountains & Plains and the Pacific Northwest (about three times the national estimate) and essentially zero in NY/NJ/PR and South Central. The single national estimate is a compromise that hides where disparities are steepest. Estimates for the Central Plains and Pacific Southwest depend on how density and income are modeled and should be read with caution.

## Model Diagnostics and Limitations

Residual plots support a linear model: the residuals-versus-fitted line is mostly flat and no tract has undue influence. Residuals have heavier tails than a normal distribution, and the fit is looser in regions that mix dense cities with remote areas (NY/NJ/PR, Mountains & Plains, Pacific Southwest, Pacific Northwest).

The independence assumption fails because neighboring tracts share highways and air-model inputs. Clustering standard errors by county widened the people-of-color confidence interval about six-fold (from 2.7%–3.0% to 1.9%–3.8%); the result remained above zero.

Diesel PM concentrations are modeled estimates, not direct measurements of personal exposure. Alaska and the U.S. territories have no diesel estimates and are excluded, so Region 10 covers only Idaho, Oregon, and Washington. "People of color" is a single combined group, so differences between racial and ethnic groups cannot be seen. Because the analysis uses census-tract data, the findings should not be interpreted as individual-level exposure or as evidence of causal relationships.

## Reproducibility

The analysis is implemented in R in `Final_Project_Doc.qmd`. Required packages: `data.table`, `dplyr`, `ggplot2`, `scales`, `sandwich`, `lmtest`, and `hexbin`.

1. Download the EJScreen 2024 dataset from Zenodo and unzip it.
2. In the setup chunk, change `data_dir` to the folder containing `EJScreen_2024_Tract_with_AS_CNMI_GU_VI.csv`.
3. Render `Final_Project_Doc.qmd` in RStudio. All chunks run in order; no other scripts are needed.

The raw data are not included in this repository because of file size.

## Data Source

Fitzgerald, W., & Gehrke, G. (2025). *EPA Environmental Justice Screening Tool (EJ Screen) data, 2015–2024* (Version v1) [Data set]. Zenodo. https://doi.org/10.5281/zenodo.14767363

Data: https://zenodo.org/records/14767363?preview_file=2024.zip
