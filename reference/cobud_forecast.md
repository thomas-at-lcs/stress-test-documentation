# Forecast Colorado's General Fund budget

Projects Colorado's General Fund budget forward from historical data,
using a set of user-specified assumptions (`params`) and, optionally,
outside revenue and spending forecasts. This is the main entry point for
the package. See [cobud - Colorado's Budget Forecast
Tool](../doc/cobud.md) and [Budget Fields](../doc/budget-fields.md) for
more details.

## Usage

``` r
cobud_forecast(
  params,
  historical_data = cobud_history,
  revenue_forecast = cobud_revenue_forecast,
  spending_forecast = cobud_spending_forecast
)
```

## Arguments

- params:

  A nested list of forecast assumptions, one element per fiscal year to
  forecast, in the format of
  [detailed_param_template](param_templates.md),
  [simple_param_template](param_templates.md), or
  [very_simple_param_template](param_templates.md). Years must be
  consecutive and may include the final year of `historical_data` (the
  current, in-progress year) plus any number of future years.

- historical_data:

  A data frame of historical budget data in the format of
  [cobud_history](cobud_history.md). Defaults to the package's
  [cobud_history](cobud_history.md) data.

- revenue_forecast:

  An optional data frame of forecasted revenue and TABOR fields in the
  format of [cobud_revenue_forecast](cobud_revenue_forecast.md).
  Required if any element of `params` uses the `"LCS forecast"`
  calculation method for a revenue field. Defaults to the package's
  [cobud_revenue_forecast](cobud_revenue_forecast.md) data.

- spending_forecast:

  An optional data frame of forecasted spending fields in the format of
  [cobud_spending_forecast](cobud_spending_forecast.md). Required if any
  element of `params` uses the `"JBC forecast"` calculation method for a
  spending field. Defaults to the package's
  [cobud_spending_forecast](cobud_spending_forecast.md) data.

## Value

A data frame with the same columns as `historical_data`, containing the
historical years plus the forecasted years specified in `params`.

## See also

[cobud_history](cobud_history.md),
[cobud_revenue_forecast](cobud_revenue_forecast.md),
[cobud_spending_forecast](cobud_spending_forecast.md), and
[cobud_field_metadata](cobud_field_metadata.md) for the data this
function consumes and produces.

## Examples

``` r
# run a forecast using default data and assumptions
custom_forecast = cobud_forecast(params = very_simple_param_template)
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
```
