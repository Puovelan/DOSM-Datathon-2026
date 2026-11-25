# Data inventory and notes

This folder separates supplied source/reference data, prepared dimensions, and final analytical outputs. The CSV files are preserved as supplied; this repository does not silently modify their values.

## `source/`

| File | Description |
|---|---|
| `arrivals_quarterly_clean.csv` | 93 quarterly national-arrival records, 2000-Q1 to 2023-Q1. |
| `Hotel_Inventory.xlsx` | 112 rows across 16 state/federal-territory units, 2019-2025; includes hotel and room counts. |
| `fact_aor_annual_clean.csv` | 128 annual average-occupancy records across 16 units, 2015-2022. |

## `processed/`

| File | Description |
|---|---|
| `arrivals_calendar_merged.csv` | Quarterly arrivals joined to calendar fields. The calendar fields are missing for earlier quarters before the supplied calendar coverage begins. |
| `dim_calendar_quarterly.csv` | 40 quarterly calendar records, 2018-Q1 to 2027-Q4. |
| `dim_spatial_weights.csv` | 16 rows containing room counts, annual AOR, and fixed state demand-share weights. |

## `outputs/`

| File | Description |
|---|---|
| `fact_historical_state_tpi.csv` | 272 state-quarter TPI records, 2019-Q1 to 2023-Q1. |
| `fact_forecast_state_tpi.csv` | 368 state-quarter forecast TPI records, 2023-Q2 to 2028-Q4. Includes lower/upper forecast bounds. |
| `fact_policy_simulation.csv` | 736 records comparing `BAU` and `SeasonShift_Policy`, across 16 units and 23 quarters (2023-Q2 to 2028-Q4). |

## Important interpretation notes

- The 16 reporting units represent Malaysia's 13 states and 3 federal territories.
- State-level tourist demand is derived from national arrivals using fixed state demand-share weights; it is not a directly observed state-level arrivals dataset.
- The report confirms TPI inputs but does not provide a fully recoverable closed-form weighting formula. The original upstream Python/Excel calculation workflow was not supplied.
- The policy CSV includes the scenarios `BAU` and `SeasonShift_Policy`. The policy outputs should be interpreted as scenario estimates under the assumptions in the report.
- The policy dashboard's gross spending, waste, and carbon movement indicators sum absolute state-level changes, including both reductions in source hubs and increases in receiving states. They are not net national savings.
- `arrivals_calendar_merged.csv` contains missing calendar values in the earlier part of the series because the supplied calendar dimension starts in 2018-Q1. Do not automatically treat these missing values as zero.

Check the final report and `../docs/METHODOLOGY_AND_LIMITATIONS.md` for additional context.
