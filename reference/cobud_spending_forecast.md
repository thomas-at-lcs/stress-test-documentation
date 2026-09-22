# An expenditure forecast for Colorado's budget

A forecast of a few spending fields that impact Colorado's General Fund
budget calculations. The forecast extends two fiscal years into the
future. Provided by JBC staff; its effects are folded into the LCS
economic forecasts but are not broken out separately there, so they are
assembled here as their own table by the LCS economics team. See
[cobud - Colorado's Budget Forecast Tool](../doc/cobud.md) and [Budget
Fields](../doc/budget-fields.md) for more details.

## Usage

``` r
cobud_spending_forecast
```

## Format

### `cobud_spending_forecast`

A data frame with 2 rows and 12 columns:

- year:

  Fiscal year

- comp_across_the_board_pct:

  Across the board salary change percentage

- comp_step_pay:

  Step pay salary change

- comp_shift_differential:

  Shift differential pay

- comp_pera_standard_pct:

  PERA standard as a percentage of salary

- comp_pera_unfunded_liability_pct:

  PERA unfunded liability as a percentage of salary

- rates_medicaid_change:

  Provider rates changes (Medicaid)

- rates_other_change:

  Provider rates changes (non-Medicaid)

- hcpf_medicaid:

  Medicaid

- corrections_adjustment:

  Corrections funding adjustment

- capital_construction:

  Capital construction

- capital_it:

  IT capital

## Source

<https://content.leg.colorado.gov/EconomicForecasts>

## See also

[cobud_field_metadata](cobud_field_metadata.md) for field-level
descriptions, [cobud_history](cobud_history.md) for the historical
series, [cobud_revenue_forecast](cobud_revenue_forecast.md) for the
accompanying revenue forecast, and
[`cobud_forecast()`](cobud_forecast.md) for the function that uses this
data.
