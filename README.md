# Traffic Proximity and Diesel Particulate Matter

## Overview

This analysis examines the relationship between traffic proximity and modeled diesel particulate matter (PM) concentrations across U.S. census tracts using EPA EJScreen 2024 data. It also evaluates whether accounting for traffic proximity changes the association between neighborhood demographic composition and diesel PM.

The analysis addresses two questions:

1. How strongly is traffic proximity associated with modeled diesel PM concentrations?
2. To what extent does including traffic proximity change the association between the proportion of residents of color and diesel PM, after adjusting for population density, low-income share, and EPA region?

## Data

The analysis uses the EPA EJScreen 2024 census-tract dataset, available through [Zenodo](https://doi.org/10.5281/zenodo.14767363). After preprocessing, the analytical sample contains 84,222 census tracts.

The variables include modeled diesel PM concentrations, traffic proximity, proportion of residents of color, population density, low-income share, and EPA region.

## Methodology

The analysis consists of three main components:

**Simple Linear Regression**

A simple linear regression estimates the association between log-transformed traffic proximity and modeled diesel PM concentrations on the original concentration scale.

**Multiple Linear Regression**

Two models are estimated using log-transformed diesel PM as the outcome. The baseline model includes demographic composition, population density, low-income share, and EPA region. The extended model adds traffic proximity.

Comparing these specifications allows changes in the demographic coefficient and overall explanatory power to be evaluated.

**Traffic-Proximity Decile Analysis**

Census tracts are grouped into ten traffic-proximity deciles, and mean diesel PM concentrations are compared across groups to examine the distribution of modeled pollution levels.

Regression diagnostics are also considered to assess model assumptions and identify potential limitations in statistical inference.

## Results

| Metric | Estimate |
|---|---:|
| Simple regression coefficient | 0.0422 |
| Simple regression R² | 0.3924 |
| R² without traffic proximity | 0.6422 |
| R² with traffic proximity | 0.6848 |
| Demographic coefficient without traffic | 0.1193 |
| Demographic coefficient with traffic | 0.0674 |
| Reduction in demographic coefficient | 43.5% |
| Adjusted traffic coefficient | 0.0543 |
| Lowest traffic-decile mean diesel PM | 0.0529 µg/m³ |
| Highest traffic-decile mean diesel PM | 0.4273 µg/m³ |

Traffic proximity is positively associated with modeled diesel PM concentrations. In the simple regression, traffic proximity accounts for approximately 39.2% of the variation in diesel PM.

Adding traffic proximity to the adjusted model increases R² from 0.6422 to 0.6848 while reducing the demographic coefficient by approximately 43.5%. The demographic association remains positive, indicating that traffic proximity accounts for part, but not all, of the observed relationship.

The decile analysis provides a complementary descriptive result: mean modeled diesel PM is approximately 8.1 times higher in the highest traffic-proximity decile than in the lowest.

## Model Diagnostics and Limitations

Residual diagnostics indicate some departures from linearity and constant variance. Spatial dependence between neighboring census tracts may also affect conventional standard errors and confidence intervals.

Diesel PM concentrations are modeled estimates rather than direct measurements of personal exposure. Traffic proximity serves as a proxy for traffic-related conditions and does not capture all potential pollution sources.

Because the analysis uses aggregated census-tract data, the findings should not be interpreted as individual-level exposure estimates or evidence of causal relationships.

## Reproducibility

The analysis is implemented in R. Reproducing the results requires the EJScreen 2024 dataset and the dependencies referenced in the analysis scripts.

After obtaining the dataset, configure the input paths and execute the preprocessing, modeling, and visualization scripts in their required order.

## Data Source
Analysis of demographic disparities in environmental pollutant exposure

Data: https://zenodo.org/records/14767363?preview_file=2024.zip
