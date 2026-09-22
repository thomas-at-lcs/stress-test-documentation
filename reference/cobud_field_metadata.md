# Metadata for each field in the Colorado budget

Metadata for the many fields that exist in
[cobud_history](cobud_history.md) or are calculated by
[`cobud_forecast()`](cobud_forecast.md). Manually assembled and
maintained by the LCS economics team. See [cobud - Colorado's Budget
Forecast Tool](../doc/cobud.md) and [Budget
Fields](../doc/budget-fields.md) for more details.

## Usage

``` r
cobud_field_metadata
```

## Format

### `cobud_field_metadata`

A data frame with 155 rows and 7 columns:

- display_name:

  a nice readable name for the field

- source:

  a hint at where this data can be located

- category:

  a high level category: "revenue", "tabor", "expenditure", "context",
  or "other"

- order:

  a sensible order to present the fields

- download_group:

  a simple, user friendly grouping of the fields

- needs_param:

  a logical indicating if it needs to be specified in the param when
  running [`cobud_forecast()`](cobud_forecast.md)

- field_name:

  the column header in [cobud_history](cobud_history.md)

## Source

LCS economics team

## See also

[cobud_history](cobud_history.md),
[cobud_revenue_forecast](cobud_revenue_forecast.md),
[cobud_spending_forecast](cobud_spending_forecast.md)
