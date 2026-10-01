# Methods

Climatic stressors such as heatwaves and droughts can affect food insecurity through several pathways. These include effects on crop yields, agricultural labour, agricultural income, non-agricultural labour and income, health, food prices and food supply chains. Together, these pathways influence both food supply and access to food.

This indicator uses a panel data regression with **time-varying coefficients** to estimate how changes in heatwaves and droughts are associated with food insecurity over time.

## Climate variables

The analysis focuses on climatic conditions during the four major crop-growing seasons in each region.

A **heatwave** is defined as a period of at least two consecutive days when daily maximum temperature exceeds the **95th percentile** of the regional climatology.

Temperature data are obtained from the **ERA5-Land hourly dataset**.

For each year from **2014 to 2024**, the analysis uses:

- one-year lagged number of heatwave days
- one-year lagged number of drought months

Drought is measured using **SPEI-12**. SPEI-12 is calculated using precipitation data from the ERA5-Land monthly averaged dataset and the `SPEI` package in R.

The heatwave and drought variables represent the difference between the observed number of heatwave days or drought months during the crop-growing seasons and the corresponding **95th percentile frequency during the 1981–2010 reference period**.

## Food insecurity

The outcome is the probability of experiencing **moderate or severe food insecurity**, based on the FAO **Food Insecurity Experience Scale (FIES)**.

FIES is based on responses to eight questions about people's experiences of constrained access to enough safe and nutritious food to support normal growth, development and an active and healthy life.

## Econometric framework

To account for differences between countries and changes over time, the model includes location fixed effects and additional socioeconomic variables.

Standard errors are clustered at the country level.

The panel data model is specified as:

```math
FIES_{it}
=
\beta_t V_{(it)}
+
\gamma'(\tau_t)X_{(it)}
+
\alpha_{(i)}
+
\mu_{(it)}
```

where:

- `FIES_{it}` is the probability of moderate or severe food insecurity, or the probability of severe food insecurity, in location `i` and year `t`
- `V_{(it)}` is a vector representing heatwave-day and drought-month anomalies during the four major crop-growing seasons, relative to the 95th percentile frequency during the 1981–2010 reference period
- `\beta_t` is the time-varying coefficient describing the effect of a heatwave-day or drought-month anomaly on food insecurity in year `t`
- `X_{(it)}` is a vector containing household income and a dummy variable representing the COVID-19 pandemic in 2020
- `\gamma'(\tau_t)` represents the coefficients associated with these additional variables
- `\alpha_{(i)}` is the location fixed effect
- `\mu_{(it)}` is the error term

The time-varying coefficients allow the relationship between climatic stressors and food insecurity to change from year to year.

For the final indicator, each estimated climate coefficient is multiplied by the share of the population experiencing moderate or severe food insecurity in that year.

## Interpretation

The analysis estimates how the relationship between changing weather conditions and food insecurity evolves over time.

The time-varying approach is useful because the effects of climate stress may accumulate. Repeated heatwaves and droughts can interact with existing vulnerabilities such as:

- income inequality
- weak links between economic growth and food security
- reduced effectiveness of social protection and safety nets
- repeated exposure to climate-related shocks

Unlike models that assume a constant relationship between climate variables and food insecurity over time, this approach allows the estimated effect to strengthen or weaken as socioeconomic conditions and vulnerability change.

# Data

The indicator uses the following data sources:

- **Temperature and drought:** ERA5-Land, ECMWF
- **Food insecurity:** FAO Food Insecurity Experience Scale

# Caveats and Limitations

The main limitation is possible **recall bias** in the food insecurity survey data.

There may also be additional bias related to changes in survey collection during the COVID-19 pandemic, when interviews were conducted by telephone rather than through in-person visits.
