# Budget Fields

## About Budget Fields

The cobud package uses sames set of fields across all the data,
templates, and outputs. Each field represents a quantifiable part of the
buget.

Budget data frames like `cobud_history` and the outputs of
[`cobud_forecast()`](../reference/cobud_forecast.md) contain data for
all the budget fields.

The forecast assumption templates (`very_simple_param_template`,
`simple_param_template`, and `detailed_param_template`) contain subsets
of the fields. The fields in the templates are the foundational fields
from which all the others can be calculated.

The forecasts (`cobud_revenue_forecast` and `cobud_spending_forecast`)
each contain a subset of the fields in the assumption templates. These
are fields that LCS and JBC staff actually forecast.

The `cobud_field_metadata` data frame has some helpful descriptions of
each field. More detailed documentation is provided here.

## Field Documentation

In the documentation below, each field is grouped and labeled with its
plain-language name and its code name (in `code font`). A small colored
tag next to the code name means that field is available in a forecast —
LCS or JBC — meaning you can set that field’s assumption method to “LCS
forecast” or “JBC forecast” instead of supplying a custom value or
generic method. Fields with no tag can still be set to any of the other
assumption options (Flat, Custom, Inflation, etc.), just not “LCS
forecast” or “JBC forecast.”

Any field with the Assumptions tag, means that it is set by the
assumption provided for it. These are the ones found in the templates.
Other fields are calculated by a formula.

### Economic Conditions

| Field | Code name | Description |
|----|----|----|
| General Fund starting balance | `gf_start_balance` | The General Fund balance at the start of the year, carried over from the prior year’s ending balance. |
| Inflation | `inflation_pct` LCS | The assumed rate of inflation for the year. Assumptions |
| State population | `population` LCS | Colorado’s population for the year. Assumptions |
| School district tax collections | `k12_property_tax` LCS | K-12 property tax revenue for the year. Assumptions |

### Revenue

| Field | Code name | Description |
|----|----|----|
| Individual income tax before triggered tax credits | `individual_income_tax_before_credits` LCS | Individual income tax revenue before triggered tax credits are subtracted. Assumptions |
| Triggered tax credits if all are on | `triggered_tax_credits_maximum` LCS | The maximum allowable amount of triggered tax credits for the year. Assumptions |
| Triggered tax credits | `triggered_tax_credits` | Total FATC and EITC (tax credits) that are triggered on. For the current year this is held fixed, for future years a complex calculation is used. See Appendix A for details. |
| Individual income tax | `individual_income_tax` | Individual income tax revenue after triggered tax credits: income tax before credits minus triggered tax credits. |
| Corporate income tax | `corporate_income_tax` LCS | Corporate income tax revenue. Assumptions |
| Total income tax | `total_income_tax` | Individual income tax plus corporate income tax. |
| Revenue diverted to the SEF | `sef_diversions` LCS | The amount of income tax revenue diverted to the State Education Fund. Assumptions |
| Revenue diverted to kids matter fund | `kids_matter_diversions` LCS | The amount of income tax revenue diverted to the Kids Matter fund. Assumptions |
| Revenue diverted to other funds | `other_diversions` LCS | Any other income tax diversions. Assumptions |
| Diverted income tax | `total_diversions` | The three diversion fields above added together, after the scaling adjustment described below. |
| Retained income tax | `retained_income_tax` | Income tax revenue retained by the General Fund after diversions: total income tax minus diverted income tax. |
| Sales tax | `sales_tax` LCS | Sales tax revenue. Assumptions |
| Use tax | `use_tax` LCS | Use tax revenue. Assumptions |
| Excise taxes exempt from TABOR | `exempt_excise_tax` LCS | The portion of excise tax revenue that is exempt from the TABOR limit. Assumptions |
| Excise taxes subject to TABOR | `tabor_excise_tax` LCS | The portion of excise tax revenue that counts against the TABOR limit. Assumptions |
| Excise taxes | `excise_tax` | Excise taxes exempt from TABOR plus excise taxes subject to TABOR. |
| Total sales, use, and excise tax | `total_sales_and_use_tax` | Sales tax plus use tax plus excise taxes. |

**Diversion scaling:** The three diversion fields (revenue diverted to
the SEF, kids matter fund, and other funds) are each scaled up or down
before being totaled, so that diversions stay proportional to income tax
collections in certain scenarios:

- If the “scale diversions with income tax” special instruction is set,
  the scaling factor is the ratio of this run’s combined
  individual-and-corporate income tax (before credits) to the LCS
  forecast’s combined figure for that year.
- If it’s the current year, the scaling factor is the ratio of this
  run’s combined income tax to the combined income tax at the start of
  the current-year calculation (before any recalculation).
- Otherwise, there is no scaling.

Total revenue is calculated in the TABOR section, since it depends on
other revenue.

### TABOR

| Field | Code name | Description |
|----|----|----|
| Other revenue | `other_revenue` LCS | Miscellaneous General Fund revenue not otherwise categorized above. Assumptions |
| Total revenue | `total_revenue` | Retained income tax plus total sales, use, and excise tax plus other revenue. |
| Cigarette Rebate | `cig_rebate` LCS | The cigarette tax rebate amount. Assumptions |
| Cash fund revenue subject to TABOR | `cf_tabor_revenue` LCS | Cash fund revenue that counts against the TABOR limit. Assumptions |
| Other revenue exempt from TABOR | `exempt_other_revenue` LCS | The portion of other revenue that is exempt from TABOR after the scaling adjustment described below. Assumptions |
| General Fund revenue exempt from TABOR | `total_exempt_revenue` | Excise taxes exempt from TABOR plus other revenue exempt from TABOR. |
| General Fund revenue subject to TABOR | `gf_tabor_revenue` | Total income tax plus total sales, use, and excise tax plus other revenue, minus diverted income tax, minus General Fund revenue exempt from TABOR, minus the cigarette rebate. |
| Accounting adjustment to TABOR limit base | `tabor_accounting_adjustment` LCS | A one-time or technical adjustment to the TABOR limit base. Assumptions |
| TABOR limit adjustment | `tabor_limit_adjustment` LCS | An adjustment added to the TABOR limit after the inflation/population growth calculation. Assumptions |
| TABOR revenue limit | `tabor_limit` | The constitutional TABOR revenue limit for the year: the prior year’s limit (plus the accounting adjustment) grown by inflation plus population growth, plus the TABOR limit adjustment. |
| TABOR refunds | `tabor_refunds` | The amount of revenue that must be refunded under TABOR: General Fund TABOR revenue plus cash fund TABOR revenue, minus the TABOR limit, floored at zero. |
| General Fund revenue within the TABOR limit | `gf_revenue_within_tabor_limit` | General Fund revenue subject to TABOR, minus TABOR refunds. |

**TABOR limit growth:** The TABOR limit grows from the prior year’s
limit by the sum of the inflation rate and the percentage change in
population.

**Exempt-other-revenue scaling:** Similar to the diversion scaling
above, other revenue exempt from TABOR is scaled up or down:

- If the “scale exempt portion of other revenue” special instruction is
  set, the scaling factor is the ratio of this run’s other revenue to
  the LCS forecast’s other revenue for that year.
- If it’s the current year, the scaling factor is the ratio of this
  run’s other revenue to other revenue at the start of the current-year
  calculation.
- Otherwise, there is no scaling.

### Appropriations

There are multiple ways General Fund appropriations can be calculated,
depending on what’s supplied in the assumptions:

1.  **If General Fund appropriations is supplied directly** in the
    assumptions, the engine skips all appropriations calculations and
    simply uses that value as-is.
2.  **If department totals are supplied** in the assumptions (identified
    by whether a total for human services is present), the engine adds
    up each department’s total to build General Fund appropriations.
    This is the calculation covered below.
3.  **Otherwise, appropriations are calculated in detail**,
    sub-department by sub-department. Documentation for that process is
    still in the works.

**Department totals**

| Field | Code name | Description |
|----|----|----|
| Total General Fund spending on K-12 | `k12_total` | General Fund spending on K-12, Assumptions |
| Total higher education | `higher_ed_total` | General Fund spending on higher education, Assumptions |
| Total HCPF | `hcpf_total` | General Fund spending on HCPF (Medicaid and related programs), Assumptions |
| Total human services | `dhs_total` | General Fund spending on human services, Assumptions |
| Total corrections | `corrections_total` | General Fund spending on corrections, Assumptions |
| Total judicial | `judicial_total` | General Fund spending on judicial, Assumptions |
| Other departments total | `other_departments_total` | General Fund spending on all other departments, Assumptions |
| Other departments treasury | `other_departments_treasury` | Treasury department spending, held flat at the prior year’s value. |
| Other appropriations (inc. 1331s) | `other_appropriations` | Last-minute emergency appropriations. These are unpredictable, so they’re assumed to be \$0 for all future years. |
| General Fund appropriations | `gf_appropriations` | The sum of all department totals above: K-12, higher education, HCPF, human services, corrections, judicial, other departments, other departments treasury, and other appropriations. |

### Other Expenditures

**Transfers**

| Field | Code name | Description |
|----|----|----|
| Transfers in | `transfers_in` LCS | Transfers into the General Fund. Assumptions |
| Capital construction | `capital_construction` JBC | Capital construction spending. Assumptions |
| IT capital | `capital_it` JBC | Capital IT spending. Assumptions |
| Capital construction and IT capital | `capital_total` | Capital construction plus IT capital. |
| Transfers out | `transfers_out` LCS | Transfers out of the General Fund, excluding capital spending. Assumptions |
| Net transfers out | `net_transfers_out` | Capital construction and IT capital, plus transfers out. Note that this does not include PERA direct distributions or property tax exemptions. |

**Rebates**

| Field | Code name | Description |
|----|----|----|
| Required rebates and expenditures | `rebates` LCS | General Fund rebate spending, excluding PERA direct distributions and property tax exemptions. Assumptions |
| Property tax exemptions | `property_tax_exemptions` LCS | The total cost of property tax exemptions for the year. Assumptions |
| Property tax exemptions not covered by TABOR refunds | `property_tax_exemptions_paid` | The portion of property tax exemptions actually paid from the General Fund: property tax exemptions minus the prior year’s TABOR refunds, floored at zero. This reflects that property tax exemptions can be funded either from the General Fund or from the prior year’s TABOR refunds. |
| PERA direct distributions | `pera_dd` LCS | The PERA direct distribution amount. Assumptions |

### Reserve

| Field | Code name | Description |
|----|----|----|
| Budget expenditures | `budget_expenditures` | General Fund appropriations plus net transfers out plus required rebates and expenditures plus property tax exemptions not covered by TABOR refunds plus PERA direct distributions. |
| Total expenditures | `total_expenditures` | Budget expenditures plus TABOR refunds. |
| Accounting adjustments | `accounting_adjustments` | End of year accounting adjustments. These are unpredictable, so they’re assumed to be \$0 for all future years. |
| General Fund ending balance | `gf_end_balance` | The General Fund balance at the end of the year: starting balance plus total revenue plus transfers in, minus total expenditures, plus accounting adjustments, plus a one-time \$500M addition in FY 25-26 (see note below). |
| Reserve requirement as a percentage of appropriations | `reserve_requirement_percentage` LCS | The statutory reserve requirement, expressed as a percentage of appropriations. Assumptions |
| Statutory reserve requirement | `reserve_requirement` | Reserve requirement percentage times General Fund appropriations, minus \$41.25 million. That subtraction reflects a loan that doesn’t count against the reserve requirement (expected to be temporary). |
| Excess reserve | `excess_reserve` | General Fund ending balance minus the statutory reserve requirement. |
| Reserve as a percentage of appropriations | `reserve_percentage` | General Fund ending balance divided by General Fund appropriations. |

**FY 25-26 note:** Starting in FY 25-26, \$500M that was moved to PERA
is added to the General Fund ending balance and counted toward the
reserve.

### Appendix A: Triggered Tax Credits

A fiscal year’s triggered tax credits (`triggered_tax_credits`) is a
combined FATC (Family Affordability Tax Credit) and EITC (Earned Income
Tax Credit) amount that increases in steps as forecasted General Fund
revenue growth crosses set thresholds.

A major complication is that tax credits actually trigger for by
calendar year, while the state budget uses a fiscal year (July-June). To
account for that, triggered tax credits are first calculated for both
associated calendar years, and then averaged. For example, forecasting
FY27-28 requires forecasting tax credits in both 2027 and 2028.

For each calendar year, there are two steps to calculate triggered tax
credits:

1.  **CAGR:** First, calculate the compound annual growth rate (CAGR) of
    revenue subject to TABOR. Again, this is awkward because revenue
    subject to TABOR data only exists for fiscal years. To resolve this,
    the CAGR for the fiscal year beginning during the year is always
    used. For example, 2027 tax credits use the expected FY27-28 CAGR.
    The CAGR baseline is fixed at \$20,415.2M in FY24-25.
2.  **Triggered On Percentage:** Second, use the CAGR to select a
    triggered on percentage for the credits. The CAGR is mapped to a
    FATC percentage and an EITC percentage using the following tiers:

| CAGR range   | FATC % | EITC % |
|--------------|--------|--------|
| below 3.00%  | 0%     | 0%     |
| 3.00%–3.18%  | 11.7%  | 20%    |
| 3.18%–3.37%  | 29.05% | 40%    |
| 3.37%–3.56%  | 50.6%  | 60%    |
| 3.56%–3.75%  | 75.9%  | 80%    |
| 3.75% and up | 100%   | 100%   |

The FATC and EITC percentages are blended into a single triggered on
percentage using a weighted average. They are weighted by the relative
size of each tax credit: `(FATC % × 0.79444) + (EITC % × 0.20556)`.

**Final Percentage:** Then the triggered on percentage for the two
relevant calendar years are combined to create a single triggered on
percentage for the fiscal year. They are weighted by previous fiscal
year’s max possible credit amount and the following fiscal year’s max
credit amount. For example:

    Final FY27-28 % = 
        2027 % × [FY26-27 max / (FY26-27 max + FY28-29 max)] + 
        2028 % × [FY28-29 max / (FY26-27 max + FY28-29 max)]

I don’t know why these weights are used.

**Triggered Tax Credits:** Lastly, the triggered tax credits forecast is
simply the final percentage multiplied by the max possible credit
amount. In our example, that would be `Final FY27-28 % × FY27-28 max`.
