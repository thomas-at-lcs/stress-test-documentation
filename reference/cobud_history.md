# A 10-year history of Colorado's budget

Historical data describing Colorado's General Fund budget going back to
FY 2015-16. These are all the fields used by and forecasted in
[`cobud_forecast()`](cobud_forecast.md). Assembled by the LCS economics
team and contained in the LCS economic forecasts. See [cobud -
Colorado's Budget Forecast Tool](../doc/cobud.md) and [Budget
Fields](../doc/budget-fields.md) for more details.

## Usage

``` r
cobud_history
```

## Format

### `cobud_history`

A data frame with 11 rows and 156 columns:

- year:

  Fiscal year

- gf_start_balance:

  General Fund starting balance

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

- triggered_tax_credits:

  Triggered tax credits

- individual_income_tax:

  Individual income tax

- corporate_income_tax:

  Corporate income tax

- total_income_tax:

  Total income tax

- sef_diversions:

  Revenue diverted to the SEF

- kids_matter_diversions:

  Revenue diverted to kids matter fund

- other_diversions:

  Revenue diverted to other funds

- total_diversions:

  Diverted income tax

- retained_income_tax:

  Retained income tax

- sales_tax:

  Sales tax

- use_tax:

  Use tax

- exempt_excise_tax:

  Excise taxes exempt from TABOR

- tabor_excise_tax:

  Excise taxes subject to TABOR

- excise_tax:

  Excise taxes

- total_sales_and_use_tax:

  Total sales, use, and excise tax

- other_revenue:

  Other revenue

- total_revenue:

  Total revenue

- cig_rebate:

  Cigarette Rebate

- cf_tabor_revenue:

  Cash fund revenue subject to TABOR

- exempt_other_revenue:

  Other revenue exempt from TABOR

- total_exempt_revenue:

  General Fund revenue exempt from TABOR

- gf_tabor_revenue:

  General Fund revenue subject to TABOR

- tabor_accounting_adjustment:

  Accounting adjustment to TABOR limit base

- tabor_limit_adjustment:

  TABOR limit adjustment

- tabor_limit:

  TABOR revenue limit

- tabor_refunds:

  TABOR refunds

- gf_revenue_within_tabor_limit:

  General Fund revenue within the TABOR limit

- comp_base_salary:

  Base salary

- comp_across_the_board_pct:

  Across the board salary change percentage

- comp_across_the_board:

  Across the board salary change

- comp_step_pay:

  Step pay salary change

- comp_shift_differential:

  Shift differential pay

- comp_total_salary:

  Total salary

- comp_health_life_dental_pct:

  Health/life/dental insurance chnages

- comp_health_life_dental_index:

  Health/life/dental insurance index

- state_insurance_pct:

  Health/life/dental insurance state share

- comp_state_health_life_dental:

  Health/life/dental insurance state cost

- comp_employee_health_life_dental:

  Health/life/dental insurance employee contribution

- comp_medicare:

  Medicare

- comp_famli:

  Family and medical leave insurance (FAMLI)

- comp_disability:

  Short-term disability

- comp_total_insurance:

  Total insurance

- comp_pera_standard_pct:

  PERA standard as a percentage of salary

- comp_pera_standard:

  PERA standard contributions

- comp_pera_unfunded_liability_pct:

  PERA unfunded liability as a percentage of salary

- comp_pera_unfunded_liability:

  PERA unfunded liability contributions

- comp_pera_dd:

  PERA direct distributions

- comp_total_pera:

  Total PERA

- comp_total:

  Total compensation

- comp_change:

  –intentionally blank–

- rates_medicaid_index:

  Provider rates index (Medicaid)

- rates_medicaid_change:

  Provider rates changes (Medicaid)

- rates_other_index:

  Provider rates index (non-Medicaid)

- rates_other_change:

  Provider rates changes (non-Medicaid)

- rates_hcpf:

  Medicaid provider rates

- rates_dhs:

  Human services provider rates

- rates_corrections:

  Corrections provider rates

- rates_other:

  All other provider rates

- rates_total:

  Total provider rates

- k12_funding_formula:

  K-12 funding formula

- k12_categorical:

  Categorical K-12 spending

- k12_other_programs:

  Other K-12 programs for districts

- k12_total_spending:

  Total K-12 spending on districts

- k12_state_spending:

  K-12 state spending from all sources

- k12_spending_from_gf:

  K-12 spending from the General Fund

- k12_spending_from_sef:

  K-12 spending from the SEF

- k12_spending_from_spsf:

  K-12 spending from the SPSF

- k12_sef_end_balance:

  SEF ending balance

- k12_comp:

  CDE staff compensation

- k12_other:

  Other CDE spending

- k12_total:

  Total General Fund spending on K-12

- k12_overall_total:

  K-12 spending including all state funds and local taxes

- tuition:

  Higher education tuition revenue

- higher_ed_institutions:

  Higher education state funding

- higher_ed_comp:

  CDHE staff compensation

- higher_ed_other:

  Other higher education

- higher_ed_total:

  Total higher education

- higher_ed_total_and_tuition:

  Total higher education funding and tuition

- hcpf_medicaid:

  Medicaid

- hcpf_rates:

  Medicaid provider rates

- hcpf_medicaid_non_rates:

  Medicaid non provider rates

- hcpf_comp:

  HCPF staff compensation

- hcpf_other:

  Other HCPF

- hcpf_total:

  Total HCPF

- dhs_behavior_comp:

  Behavioral health staff compensation

- dhs_behavior_rates:

  Behavioral health provider rates

- dhs_behavior_non:

  Behavioral health program costs

- dhs_behavior:

  Behavioral health

- dhs_child_comp:

  Child welfare staff compensation

- dhs_child_rates:

  Child welfare provider rates

- dhs_child_non:

  Child welfare program costs

- dhs_child:

  Child welfare

- dhs_assistance_comp:

  Public assistance staff compensation

- dhs_assistance_rates:

  Public assistance provider rates

- dhs_assistance_non:

  Public assistance program costs

- dhs_assistance:

  Public assistance (SNAP, TANF, and others)

- dhs_other_comp:

  Other DHS staff compensation

- dhs_other_rates:

  Other DHS provider rates

- dhs_other_non:

  Other DHS program costs

- dhs_other:

  Other DHS

- dhs_comp:

  Human services staff compensation

- dhs_rates:

  Human services provider rates

- dhs_non:

  Human services program costs

- dhs_total:

  Total human services

- corrections_adjustment:

  Corrections funding adjustment

- corrections_comp:

  Corrections staff compensation

- corrections_rates:

  Corrections provider rates

- corrections_other:

  Corrections programs

- corrections_total:

  Total corrections

- judicial_courts_comp:

  State courts staff compensation

- judicial_courts_non_comp:

  State courts non-compensation

- judicial_courts:

  State courts

- judicial_defense_comp:

  Public defense staff compensation

- judicial_defense_non_comp:

  Public defense non-compensation

- judicial_defense:

  Public defense

- judicial_other_comp:

  Probation and other programs staff compensation

- judicial_other_non_comp:

  Probation and other programs non-compensation

- judicial_other:

  Probation and other programs

- judicial_comp:

  Judicial staff compensation

- judicial_non_comp:

  Judicial non-compensation

- judicial_total:

  Total judicial

- other_departments_comp:

  Other departments staff compensation

- other_departments_rates:

  Other departments provider rates

- other_departments_other:

  Other departments programs

- other_departments_treasury:

  Other departments treasury

- other_departments_total:

  Other departments total

- other_appropriations:

  Other appropriations (inc. 1331s)

- gf_appropriations:

  General Fund appropriations

- adjusted_salary:

  Adjusted salary

- adjusted_insurance:

  Adjusted insurance

- adjusted_pera:

  Adjusted retirement benefits (PERA)

- transfers_in:

  Transfers in

- capital_construction:

  Capital construction

- capital_it:

  IT capital

- capital_total:

  Capital construction and IT capital

- transfers_out:

  Transfers out

- net_transfers_out:

  Net transfers out

- rebates:

  Required rebates and expenditures

- property_tax_exemptions:

  Property tax exemptions

- property_tax_exemptions_paid:

  Property tax exemptions not covered by TABOR refunds

- pera_dd:

  PERA direct distributions

- budget_expenditures:

  Budget expenditures

- total_expenditures:

  Total expenditures

- accounting_adjustments:

  Accounting adjustments

- gf_end_balance:

  General Fund ending balance

- reserve_requirement_percentage:

  Reserve requirement as a percentage of appropriations

- reserve_requirement:

  Statutory reserve requirement

- excess_reserve:

  Excess reserve

- reserve_percentage:

  Reserve as a percentage of appropriations

## Source

<https://content.leg.colorado.gov/EconomicForecasts>

## See also

[cobud_field_metadata](cobud_field_metadata.md) for field-level
descriptions, [cobud_revenue_forecast](cobud_revenue_forecast.md) and
[cobud_spending_forecast](cobud_spending_forecast.md) for the
forward-looking counterparts, and
[`cobud_forecast()`](cobud_forecast.md) for the function that uses this
data.
