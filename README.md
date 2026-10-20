# Environmental Justice and Diesel PM Exposure Across U.S. Census Tracts

## Project Overview

This project examines disparities in modeled diesel particulate matter (PM) concentrations across U.S. census tracts using EPA EJScreen 2024 data. The analysis focuses on how neighborhood demographics, population density, income, geographic location, and traffic proximity relate to differences in diesel PM concentrations.

The project combines exploratory data analysis, linear and logistic regression, geographic comparisons, and model diagnostics to examine these relationships. Particular attention is given to how the estimated demographic association changes after accounting for other neighborhood characteristics, and whether these relationships differ across EPA regions.

## Dataset

**Source:** EPA EJScreen 2024 census-tract data  
**Dataset:** https://doi.org/10.5281/zenodo.14767363

The original dataset contains 86,082 census tracts. After preprocessing and applying the analysis filters, 84,222 tracts are retained.

The main variables include:
- Diesel particulate matter concentration (µg/m³)
- Percentage of residents of color
- Low-income population percentage
- Population density
- Traffic proximity
- EPA region

Diesel PM is a modeled ambient pollution estimate, rather than a direct measurement of individual exposure.

## Analysis

The project is organized into two branches, each covering a different part of the analysis.

### 1. Demographic and Geographic Analysis

**Branch:** [`kayla-eda`](../../tree/kayla-eda)

This branch examines the relationship between demographic composition and diesel PM concentrations, with a focus on population density, income, and geographic variation.

The analysis includes exploratory data analysis, simple and multiple linear regression, regional comparisons, interaction models, and logistic regression to examine the likelihood of a census tract falling within the highest diesel PM exposure category.

Model diagnostics, confidence intervals, effect sizes, and sensitivity checks are used to evaluate the results and their statistical reliability.

### 2. Traffic Proximity Analysis

**Branch:** [`trafficproximity`](../../tree/trafficproximity)

This branch examines the association between traffic proximity and modeled diesel PM concentrations, including how traffic proximity changes the estimated demographic association.

The analysis includes simple linear regression, comparison of adjusted multiple regression models with and without traffic proximity, and a decile-based comparison of diesel PM concentrations across traffic-proximity levels.

Regression diagnostics and measurement limitations are also considered when interpreting the findings.

## Main Findings

The results show a positive association between the proportion of residents of color and modeled diesel PM concentrations. Population density accounts for a substantial portion of this relationship, although a smaller positive association remains after adjusting for income and EPA region.

The strength of the demographic association also varies geographically, with some EPA regions showing considerably larger differences than others.

Traffic proximity is positively associated with modeled diesel PM. Including traffic proximity improves model fit and reduces the estimated demographic coefficient, but does not eliminate the association.

Together, these findings suggest that neighborhood density, geographic location, and traffic-related conditions are important for understanding the distribution of modeled diesel PM across census tracts.

## Interpretation and Limitations

The analysis is based on census-tract-level data and modeled pollution estimates. These measures are useful for identifying broader geographic patterns but cannot establish individual exposure levels.

Regression results may also be affected by spatial dependence, differences in model fit across regions, and environmental factors not captured by the available variables.

The findings describe statistical associations and should not be interpreted as evidence of causation.

## Repository Structure

The analyses are maintained in separate Git branches:

| Branch | Contents |
|---|---|
| `main` | Project overview and navigation to the analysis branches |
| [`kayla-eda`](../../tree/kayla-eda) | Exploratory analysis, demographic and geographic regression models, logistic regression, and model diagnostics |
| [`trafficproximity`](../../tree/trafficproximity) | Traffic-proximity regression, adjusted model comparisons, decile analysis, and diagnostics |

Refer to the respective branches for the analysis code, visualizations, and supporting documentation.

## Tools

The analysis uses R for data preprocessing, statistical modeling, and visualization, with Git and GitHub for version control and collaboration.

## Data Reference

EPA EJScreen 2024 census-tract dataset. Available at: https://doi.org/10.5281/zenodo.14767363
