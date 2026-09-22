# Introduction to cobud

## About cobud

The goal of cobud is to make it easy to understand and forecast
Colorado’s General Fund budget. A forecast like that is hard for two
reasons.

1.  The budget calculations are complicated.
2.  It’s hard to make good assumptions about how revenue and spending
    will change in the future.

The cobud package completely takes care of the budget calculations.
Regarding assumptions, cobud offers a reasonable place to start based on
the Colorado Legislature’s nonpartisan staff estimates and lets you make
adjustments from there.

## Budget History

Before getting into the forecast, it’s helpful to understand what
Colorado’s General Fund budget has looked like in the past. First load
cobud along with dplyr to make it easy to work with the data.

``` r

library(cobud)
library(dplyr)
```

Included in cobud is a data frame called `cobud_history` with a detailed
description of the budget from FY 2015-16 to the current fiscal year.
Here we select a few key fields to get a sense of what this data looks
like. All budget values are in millions of dollars.

``` r

cobud_history |> select(
  year,
  gf_start_balance,
  total_revenue,
  total_expenditures,
  gf_end_balance
)
#>     year gf_start_balance total_revenue total_expenditures gf_end_balance
#> 1  15-16               NA        9971.4            10189.7          512.7
#> 2  16-17            512.7       10275.8            10424.7          614.5
#> 3  17-18            614.5       11723.9            11215.4         1366.0
#> 4  18-19           1366.0       12564.6            12857.3         1262.6
#> 5  19-20           1262.6       12868.0            12778.9         1825.7
#> 6  20-21           1825.7       14310.1            13327.1         3181.5
#> 7  21-22           3181.5       17697.9            17838.7         3203.2
#> 8  22-23           3203.2       17998.0            19027.2         2427.4
#> 9  23-24           2427.4       17251.4            16870.8         3153.5
#> 10 24-25           3153.5       17181.3            18572.8         2408.4
#> 11 25-26           2408.4       16870.3            18062.7         2045.8
```

## Forecast Assumptions

To forecast future years of the budget, you’ll first need to define a
number of assumptions about how things will change in the future. This
package includes three templates for doing that. Let’s start with
`very_simple_param_template`.

This is a [`list()`](https://rdrr.io/r/base/list.html) object with
budget assumptions for the current fiscal year and the upcoming fiscal
year. Each fiscal year has about thirty assumptions within it.

``` r

names(very_simple_param_template)
#> [1] "25-26" "26-27"

# look at current year assumptions
very_simple_param_template[[1]] |> head(3)
#> $inflation_pct
#> $inflation_pct$method
#> [1] "Current"
#> 
#> 
#> $population
#> $population$method
#> [1] "Current"
#> 
#> 
#> $k12_property_tax
#> $k12_property_tax$method
#> [1] "Current"

# look at next year assumptions
very_simple_param_template[[2]] |> head(3)
#> $inflation_pct
#> $inflation_pct$method
#> [1] "LCS forecast"
#> 
#> 
#> $population
#> $population$method
#> [1] "LCS forecast"
#> 
#> 
#> $k12_property_tax
#> $k12_property_tax$method
#> [1] "LCS forecast"
```

But don’t be intimidated! Each assumption simply specifies how a field
in the budget should be calculated. For the current fiscal year, every
assumption is exactly the same: `list(method = "Current")`. For future
years, the format is the same but the default assumptions are different.
For example, inflation is based on the “LCS forecast”.

A full list of valid methods and what each one means is provided here.

| Option | What it does |
|----|----|
| Current | Use the true, actual value. Can only be used for the current fiscal year. See `cobud_history`. |
| Flat | Use the same value as the previous year. |
| LCS forecast | Use the value from the LCS forecast. Only applies to fields included in the LCS forecast. See `cobud_revenue_forecast`. |
| JBC forecast | Use the value from the JBC forecast. Only applies to fields included in the JBC forecast. See `cobud_spending_forecast`. |
| Custom | Use a custom value that you supply. |
| Custom change | Adjust the previous year’s value by a custom percent change that you supply. |
| Inflation | Adjust the previous year’s value by the assumed rate of inflation. |
| Prior year | Adjust the previous year’s value by the same percent change it saw from the year before. |
| 10-year average | Adjust the previous year’s value by the 10-year average percent change. |

`very_simple_param_template` is the simplest way to specify budget
assumptions. If you want to work with a more detailed breakdown of state
spending, you can use the more detailed templates
`simple_param_template` and `detailed_param_template`. They have the
same format but require more spending assumptions to be specified.

## Adjusting Assumptions

Any assumption specified in the template can also be changed. The
primary way to change an assumption is by adjusting the `method`.

``` r

# make a copy of the template
custom_params = very_simple_param_template

# assume sales tax will remain flat next year
custom_params[[2]][["sales_tax"]] = list(
  method = "Flat"
)
```

If the `method` is set to “Custom” or “Custom change”, a custom `value`
must also be provided. It should always be a number. It is a dollar
amount when “Custom” is selected, and a multiplicative factor when
“Custom change” is selected.

``` r

# assume corporate income tax will be $2.2 billion
custom_params[[2]][["corporate_income_tax"]] = list(
  method = "Custom",
  value = 2200
) 

# assume population will grow by 3% from the previous year
custom_params[[2]][["population"]] = list(
  method = "Custom change",
  value = 1.03
) 
```

Dollar amount adjustments (additions or subtractions) can also be
provided for any assumption by adding `adj` to the list. These additions
or subtractions will be added after the specified calculation method is
used.

``` r

# assume General Fund appropriations will be the same as the current year
# plus $800 million
custom_params[[2]][["gf_appropriations"]] = list(
  method = "Flat",
  adj = +800
)
```

## Budget Forecast

Now that we’ve built out a set of custom assumptions, it’s time to run
the forecast. [`cobud_forecast()`](../reference/cobud_forecast.md) is a
function that takes in your assumptions (params) and returns a data
frame like `cobud_history` but with forecasted data added based on the
params provided.

``` r

# run the forecast
custom_forecast = cobud_forecast(custom_params)
#> inputs validated
#> preparing tax credit triggers...
#>    for 25-26 ...
#>    for 26-27 ...
#> calculating 25-26 budget...
#>    using very simple appropriations...
#> calculating 26-27 budget...
#>    using very simple appropriations...
#> budget calculation successful
#> outputs validated

# preview the resulting forecast
custom_forecast |>
  select(
    year,
    gf_start_balance,
    total_revenue,
    total_expenditures,
    gf_end_balance
  ) |>
  tail()
#>     year gf_start_balance total_revenue total_expenditures gf_end_balance
#> 7  21-22         3181.500      17697.90            17838.7       3203.200
#> 8  22-23         3203.200      17998.00            19027.2       2427.400
#> 9  23-24         2427.400      17251.40            16870.8       3153.500
#> 10 24-25         3153.500      17181.30            18572.8       2408.400
#> 11 25-26         2408.400      16870.30            18062.7       2045.795
#> 12 26-27         2045.795      17939.63            18604.9       1434.918
```

## Forecasting Two Years

That forecast only covers one future fiscal year. If we want it to cover
two, we can add another year to the param.

``` r

# start with the param template
two_year_params = very_simple_param_template

# copy the 26-27 params for 27-28
two_year_params[["27-28"]] = two_year_params[["26-27"]]

# customize the sales tax assumptions for both years
two_year_params[["26-27"]][["sales_tax"]] = list(
   method = "Flat",
   adj = +100 # increase by $100 million from 25-26
)
two_year_params[["27-28"]][["sales_tax"]] = list(
   method = "Custom change",
   value = 1.07 # increase 7% from 26-27
)

# run the forecast 
two_year_forecast = cobud_forecast(two_year_params)
#> inputs validated
#> preparing tax credit triggers...
#>    for 25-26 ...
#>    for 26-27 ...
#>    for 27-28 ...
#> calculating 25-26 budget...
#>    using very simple appropriations...
#> calculating 26-27 budget...
#>    using very simple appropriations...
#> calculating 27-28 budget...
#>    using very simple appropriations...
#> budget calculation successful
#> outputs validated

# preview the resulting forecast
two_year_forecast |>
  select(year, sales_tax, gf_end_balance)
#>     year sales_tax gf_end_balance
#> 1  15-16  2585.300       512.7000
#> 2  16-17  2727.700       614.5000
#> 3  17-18  2926.000      1366.0000
#> 4  18-19  3054.000      1262.6000
#> 5  19-20  3196.000      1825.7000
#> 6  20-21  3418.100      3181.5000
#> 7  21-22  4089.000      3203.2000
#> 8  22-23  4301.600      2427.4000
#> 9  23-24  4362.600      3153.5000
#> 10 24-25  4441.100      2408.4000
#> 11 25-26  4600.100      2045.7950
#> 12 26-27  4700.100      1113.1521
#> 13 27-28  5029.107      -103.8884
```

## Forecasting More Than Two Years

If we want to do more than two years, we can just add more years to the
param. An important limitation is that **the LCS forecast and the JBC
forecast only cover two future years**. For any years beyond that, the
param cannot use the “LCS forecast” or “JBC forecast” methods.

``` r

# start with the param template
three_year_params = very_simple_param_template

# copy the 26-27 params twice
three_year_params[["27-28"]] = three_year_params[["26-27"]]
three_year_params[["28-29"]] = three_year_params[["26-27"]]

# try to run the forecast 
try(
  cobud_forecast(three_year_params)
)
#> Error in validate_revenue_forecasts(params, rev, spend) : 
#>   validate_revenue_forecasts error: year '28-29' field 'inflation_pct' uses method 'LCS forecast' but revenue_forecast has no non-missing value for that field and year

# observe that "LCS forecast" was invoked but no forecast data was provided
three_year_params[["28-29"]][["inflation_pct"]]
#> $method
#> [1] "LCS forecast"
cobud_revenue_forecast |> select(year, inflation_pct)
#>    year inflation_pct
#> 1 26-27         0.025
#> 2 27-28         0.031
```

“LCS forecast” is heavily used in these templates, so if we want to
forecast more than two years, we need to specify lots of assumptions.

One simple options is to take anything forecasted and instead grow it by
inflation in FY 2028-29.

``` r

# set a custom inflation assumption
three_year_params[["28-29"]][["inflation_pct"]] = list(
  method = "Custom",
  value = 0.042 # 4.2% inflation
)

# change any "LCS forecast" or "JBC forecast" uses to "Inflation" 
use_inf <- function(x) {
  if("LCS forecast" %in% x$method | "JBC forecast" %in% x$method) {
    x$method = "Inflation"
  } 
  return(x)
}
three_year_params[["28-29"]] = lapply(three_year_params[["28-29"]], use_inf)

# tweak a few options that rely on the LCS forecast
three_year_params[["28-29"]]$options$`scale diversions with income tax` = FALSE
three_year_params[["28-29"]]$options$`scale exempt portion of other revenue` = FALSE

# run the three year forecast
three_year_forecast = cobud_forecast(three_year_params)
#> inputs validated
#> preparing tax credit triggers...
#>    for 25-26 ...
#>    for 26-27 ...
#>    for 27-28 ...
#>    for 28-29 ...
#> calculating 25-26 budget...
#>    using very simple appropriations...
#> calculating 26-27 budget...
#>    using very simple appropriations...
#> calculating 27-28 budget...
#>    using very simple appropriations...
#> calculating 28-29 budget...
#>    using very simple appropriations...
#> budget calculation successful
#> outputs validated
three_year_forecast |>
  select(year, sales_tax, gf_end_balance)
#>     year sales_tax gf_end_balance
#> 1  15-16  2585.300       512.7000
#> 2  16-17  2727.700       614.5000
#> 3  17-18  2926.000      1366.0000
#> 4  18-19  3054.000      1262.6000
#> 5  19-20  3196.000      1825.7000
#> 6  20-21  3418.100      3181.5000
#> 7  21-22  4089.000      3203.2000
#> 8  22-23  4301.600      2427.4000
#> 9  23-24  4362.600      3153.5000
#> 10 24-25  4441.100      2408.4000
#> 11 25-26  4600.100      2045.7950
#> 12 26-27  4798.500      1113.1521
#> 13 27-28  5046.000      -103.8884
#> 14 28-29   211.932    -19095.7767
```
