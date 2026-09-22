# Param templates

Each budget forecast, or call to
[`cobud_forecast()`](cobud_forecast.md), requires the user to specify
the assumptions of the budget forecast run. These assumptions are
specified in a nested list called a param. The param templates are
examples of valid params.

See [cobud - Colorado's Budget Forecast Tool](../doc/cobud.md) and
[Budget Fields](../doc/budget-fields.md) for more details.

## Usage

``` r
detailed_param_template

simple_param_template

very_simple_param_template
```

## Format

### `detailed_param_template`

A nested list in the following format:

- 25-26:

  inflation_pct

  : 

  population

  : 

- 26-27:

  inflation_pct

  : 

  population

  : 

    method

    : "Custom change"

    value

    : 1.05

    adj

    : 0.1

An object of class `list` of length 2.

An object of class `list` of length 2.

## Source

<https://content.leg.colorado.gov/EconomicForecasts>

## See also

[cobud_field_metadata](cobud_field_metadata.md) for field-level
descriptions, [cobud_history](cobud_history.md) for the historical
series, [cobud_revenue_forecast](cobud_revenue_forecast.md) for the
accompanying revenue forecast, and
[`cobud_forecast()`](cobud_forecast.md) for the function that uses this
data to forecast the budget.
