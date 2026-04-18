# 🏙️ NYC Homeless Shelter Analysis (2015–2025)

**Author:** Alejandro Cespedes Fernandez  
**Last Updated:** February 2026  
**Data Source:** [NYC DHS Data Dashboard](https://catalog.data.gov/dataset/dhs-data-dashboard)

---

## Overview

This project analyzes a decade of NYC Department of Homeless Services (DHS) shelter census data, covering July 2015 through March 2025. The dataset tracks individuals in the shelter system at the time of each census, broken down by population type, age, ethnicity, and gender. The analysis concludes with Poisson regression models to identify which demographic factors are most predictive of shelter placement rates.

---

## Population Categories

| Abbreviation | Meaning |
|---|---|
| **FWC** | Families with Children |
| **AF** | Adult Families |
| **SA** | Single Adults |
| **HoH** | Head of Household |

---

## Key Findings

### Age
- Children aged **0–13** make up the largest share of the FWC homeless population.
- Among adult families, the **45–64** age group is most represented — likely because this is when individuals are fully independent but have the fewest social safety nets available.
- Younger adults (18–29, 30–44) tend to cycle in and out of homelessness, while those 45–64 tend to remain homeless for longer stretches, consistent with findings from the National Library of Medicine on chronic homelessness and adverse childhood experiences.

### COVID-19 Impact (2020)
- Homelessness among families with children dropped noticeably in 2020, likely correlated with pandemic-era mortality and shelter disruption.
- Single adults showed **less displacement** during COVID, suggesting they received fewer pandemic financial supports and were therefore less affected when those supports ended.

### Post-2022 Surge
- All groups saw a sharp increase starting in 2022, driven by two factors:
  1. **Immigration surge** — NYC experienced a major influx of asylum seekers, accounting for ~60% of the rise (per cited sources).
  2. **Housing inflation** — Housing prices rose ~7% in 2022, while wages did not keep pace, pushing more residents into homelessness.

### Ethnicity
- **Black Non-Hispanic** and **Hispanic** individuals are drastically overrepresented in the shelter population relative to their share of NYC's total population — consistent with research on structural racism in housing access (Molly K. Richard).
- The **Hispanic population** showed a sharp spike post-2022, driven primarily by the immigration surge.
- White Non-Hispanic individuals are significantly underrepresented compared to NYC demographics.

### Gender
- There are far more homeless **men** than women in the single adult category, and the male population is growing.
- The female homeless population is notably stable — likely because women have stronger informal support networks and government assistance access, and because women experiencing homelessness as mothers are classified under FWC rather than single adults.
- Veterans are cited as a significant driver of male homelessness, given insufficient reintegration support.

### Shelter Placement Rates
- Across all groups, shelter placement rates never exceed **~7%** of the total homeless population — a stark indicator of NYC's insufficient housing capacity.
- Single adults have higher placement rates than families, likely because they are easier to accommodate and cycle through homelessness more quickly.

---

## Regression Analysis

Poisson regression models were applied to each population group (FWC, AF, SA) to predict total shelter placements.

### Families with Children — Key Results
- Having more children in shelter is **negatively correlated** with placement likelihood.
- **Black Non-Hispanic** heads of household show a strong positive correlation with shelter placements.
- Age groups **18–20**, **45–64**, and **65+** are positively associated with placements.
- The model shows high multicollinearity (expected given correlated demographic variables); VIF values are very large across age and race predictors.

### Methodological Notes
- The dataset changed reporting frequency mid-2022; only the last observation per month was retained, yielding **121 data points**.
- No data points were removed, as all observations are considered analytically meaningful, even if they introduce skew.
- A Poisson family was chosen given the count-based nature of the outcome variable (shelter placements).

---

## Data & Tools

- **Language:** R
- **Libraries:** `dplyr`, `ggplot2`, `car`
- **Model type:** Generalized Linear Model (`glm`) with Poisson family
- **Dataset:** NYC DHS shelter census, monthly, July 2015 – March 2025

---

## Planned Improvements

- [ ] Separate race and age regressions using adults as the baseline for rate comparison
- [ ] Add citation for COVID mortality reduction among homeless persons
- [ ] Explore veteran homelessness angle further
- [ ] Address multicollinearity via ridge regression or PCA-based dimensionality reduction
- [ ] Apply time series modeling to quantify whether the 2022 immigration shock is permanent

---

## References

- NYC DHS Data Dashboard: https://catalog.data.gov/dataset/dhs-data-dashboard
- National Library of Medicine — chronic homelessness in older adults
- Molly K. Richard — structural racism and housing inequality
- American Institute for Boys and Men (AIBM) — gender disparities in homelessness