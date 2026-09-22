# A revenue forecast for Colorado's budget

A forecast of revenue and TABOR fields that impact Colorado's General
Fund budget calculations. The forecast extends two fiscal years into the
future. Assembled by the LCS economics team and contained in the LCS
economic forecasts. See [cobud - Colorado's Budget Forecast
Tool](../doc/cobud.md) and [Budget Fields](../doc/budget-fields.md) for
more details.

## Usage

``` r
cobud_revenue_forecast
```

## Format

### `cobud_revenue_forecast`

A data frame with 2 rows and 29 columns:

- year:

  Fiscal year

- inflation_pct:

  Inflation

- population:

  State population

- k12_property_tax:

  School district tax collections

- individual_income_tax_before_credits:

  Individual income tax before triggred tax credits

- triggered_tax_credits_maximum:

  Triggered tax credits if all are on

- corporate_income_tax:

  Corporate income tax

- sef_diversions:

  Revenue diverted to the SEF

- kids_matter_diversions:

  Revenue diverted to kids matter fund

- other_diversions:

  Revenue diverted to other funds

- sales_tax:

  Sales tax

- use_tax:

  Use tax

- exempt_excise_tax:

  Excise taxes exempt from TABOR

- tabor_excise_tax:

  Excise taxes subject to TABOR

- other_revenue:

  Other revenue

- tabor_accounting_adjustment:

  Accounting adjustment to TABOR limit base

- tabor_limit_adjustment:

  TABOR limit adjustment

- cig_rebate:

  Cigarette Rebate

- cf_tabor_revenue:

  Cash fund revenue subject to TABOR

- exempt_other_revenue:

  Other revenue exempt from TABOR

- k12_funding_formula:

  K-12 funding formula

- k12_other_programs:

  Other K-12 programs for districts

- k12_spending_from_spsf:

  K-12 spending from the SPSF

- transfers_in:

  Transfers in

- transfers_out:

  Transfers out

- rebates:

  Required rebates and expenditures

- property_tax_exemptions:

  Property tax exemptions

- pera_dd:

  PERA direct distributions

- reserve_requirement_percentage:

  Reserve requirement as a percentage of appropriations

## Source

<https://content.leg.colorado.gov/EconomicForecasts>

## See also

[cobud_field_metadata](cobud_field_metadata.md) for field-level
descriptions, [cobud_history](cobud_history.md) for the historical
series, [cobud_spending_forecast](cobud_spending_forecast.md) for the
accompanying spending forecast, and
[`cobud_forecast()`](cobud_forecast.md) for the function that uses this
data.
