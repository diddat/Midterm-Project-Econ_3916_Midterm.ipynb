# Midterm-Project-Econ_3916_Midterm.ipynb
Project overview
This project examines whether U.S. places with higher housing vacancy rates had lower median monthly gross rents in 2025, after accounting for median household income and unemployment. It uses data from the U.S. Census Bureau's 2025 American Community Survey (ACS) 1-year estimates. The final analysis includes 672 large U.S. places.

Research question
Are higher housing vacancy rates associated with lower median monthly rents across large U.S. places, controlling for median household income and unemployment?

The outcome is median monthly gross rent in dollars. The main explanatory variable is total housing vacancy as a percentage of housing units. The two controls are median annual household income (scaled to $10,000 units) and unemployment rate (percentage points).

Data and source
- Provider: U.S. Census Bureau, American Community Survey (ACS) 2025 1-Year Estimates.
- API endpoint: https://api.census.gov/data/2025/acs/acs1
- Unit of observation: Census place (primarily places with populations of 65,000 or more, as covered by ACS 1-year estimates).
- Variables: Median gross rent (B25064_001E), median household income (B19013_001E), civilian labor force (B23025_003E), unemployed civilians (B23025_005E), total housing units (B25002_001E), and vacant housing units (B25002_003E).
- Constructed measures: vacancy_pct = 100 × vacant_units / housing_units; unemployment_pct = 100 × unemployed / labor_force.
- Saved working dataset: data/housing_vacancy_rents_2025.csv.

Method
The primary specification is an ordinary least squares (OLS) regression:

Median rent = β₀ + β₁(Vacancy rate) + β₂(Income / 10,000) + β₃(Unemployment rate) + error

The project first examines rent distributions and a bivariate scatter plot. It then estimates a multivariable regression, checks residual plots and heteroskedasticity with the Breusch–Pagan test, measures multicollinearity using variance inflation factors (VIFs), and inspects influential observations using Cook's distance. Because the Breusch–Pagan test rejects constant error variance, the final inference uses HC3 robust standard errors.

Main findings
- Sample size: 672 places.
- Unadjusted vacancy slope: about −$38.31 in monthly median rent per additional percentage point of vacancy; raw correlation approximately −0.36.
- Adjusted vacancy slope: approximately −$3.89 per percentage point after controlling for income and unemployment.
- HC3 robust 95% confidence interval for vacancy: approximately −$9.28 to $1.51; this includes zero, so the adjusted association is not statistically significant at the 5% level.
- Income coefficient: approximately +$133.74 in monthly median rent per $10,000 increase in median annual household income, holding the other variables fixed.
- Model R²: approximately 0.667, so the included variables explain 66.7% of observed cross-place variation in rent.
- Diagnostics: Breusch–Pagan p < 0.001 indicates heteroskedasticity; VIFs are low (roughly 1.13–1.38); 42 observations exceed the common Cook's distance cutoff of 4/n.
- 
Limitations
This is a cross-sectional, observational study and does not identify a causal effect of vacancy on rent. Income, unemployment, local growth, construction, amenities, and housing quality may be correlated with both vacancy and rent. Reverse causality is possible, and the measure of total vacancy does not isolate homes currently offered for rent. Future work could use rental-specific vacancy rates, multiple years of data, local construction and population measures, and a credible quasi-experimental design.
