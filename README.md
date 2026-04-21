# Trip Duration Analysis — Chicago Cab Service

## Overview
This project analyzes urban mobility patterns in Chicago using taxi trip data,
combining SQL-based data extraction, exploratory data analysis, and statistical
hypothesis testing to determine whether weather conditions significantly impact
trip duration.

## Note on Language
The Jupyter notebook and internal comments are currently in Spanish.
An English version is in progress.

## Tools & Libraries
Python · Pandas · SciPy · Seaborn · Matplotlib · SQL (PostgreSQL)

## Methodology

### 1. SQL Data Extraction
Six queries were designed to extract and prepare the data:
- Trip volume per taxi company (Nov 15–16, 2017).
- Trip counts filtered by company name keywords ("Yellow", "Blue").
- Market share comparison: Flash Cab, Taxi Affiliation Services vs. all others.
- Neighborhood ID retrieval for O'Hare and Loop districts.
- Weather classification per hour using CASE logic (`Bad` = rain/storm, 
  `Good` = all others).
- Full trip records from Loop to O'Hare on Saturdays, joined with weather 
  conditions and duration.

### 2. Exploratory Data Analysis (Python)
- No missing values or type inconsistencies found across datasets.
- Flash Cab identified as the dominant company by trip volume, significantly 
  ahead of all competitors.
- Loop confirmed as the neighborhood with the highest average trip completions,
  validating it as the focal point for hypothesis testing.

### 3. Hypothesis Testing
**Hypothesis:** Average trip duration from Loop to O'Hare changes on rainy 
Saturdays.

- **H₀:** Average trip duration does not change on rainy Saturdays.
- **H₁:** Average trip duration changes on rainy Saturdays.

Welch's t-test selected due to significant difference in sample sizes between 
weather groups, despite similar standard deviations. Significance level: α = 0.05.

## Key Results

| | Good Weather | Bad Weather |
|---|---|---|
| Median duration | 1,800s (30 min) | 2,565s (42.7 min) |
| Sample size | Larger | Smaller |

- **t-statistic:** 7.478
- **p-value:** 1.11e-12 (≪ 0.05)
- **Result:** H₀ rejected. Rain produces a systemic increase in trip duration.

The difference in medians (12.7 min) exceeds the difference in means (7.2 min),
indicating that rain does not cause isolated delays but shifts the entire 
distribution — increasing typical trip duration by over 20% on rainy Saturdays.

## Conclusions
Weather conditions have a statistically significant and practically meaningful
impact on urban trip duration. Rain on Saturdays increases the typical Loop–O'Hare
trip by nearly 13 minutes, a finding relevant for dynamic pricing, driver 
allocation, and demand forecasting models.

## Project Structure
```
├── datasets/
│   ├── project_sql_result_01.csv   # Trip counts per company
│   ├── project_sql_result_04.csv   # Average trips per neighborhood
│   └── project_sql_result_07.csv   # Loop–O'Hare trips with weather data
├── cabs_company.ipynb                  # Full analysis (Spanish)
└── README.md
```
