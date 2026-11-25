# Methodology, assumptions, and limitations

## Analytical design

The submitted project follows a sequence of data collection, cleaning/integration, TPI construction, time-series forecasting, and policy simulation. Outputs are presented in a four-page Power BI report.

### Inputs described in the report

1. **Tourist arrivals:** quarterly national arrivals, 2000-2023, used as the demand input and forecasting history.
2. **Hotel inventory:** state-level hotel and room counts, 2019-2025, used as an accommodation-capacity input.
3. **Average occupancy rate (AOR):** state-level annual average occupancy, 2015-2022, used as a baseline utilisation input.
4. **Calendar and spatial reference data:** public-holiday counts, school-holiday density, monsoon flags, and fixed state demand-share weights.

The report describes state demand as being derived by applying each state's fixed demand-share weight to national quarterly arrivals. Hotel inventory is joined by state and year, and AOR is used as a state baseline. The inputs are organised in Power BI with a shared calendar dimension.

## Tourism Pressure Index

The report describes TPI as a quarterly, state-level composite intended to represent visitor pressure relative to accommodation capacity and baseline occupancy. Confirmed inputs include state-level allocated demand, room capacity, baseline AOR, and seasonal context.

The report explicitly states that the exact closed-form weighting formula was not recoverable from the packaged Power BI file because the calculation occurred upstream in Python/Excel. For that reason, this repository does not invent or reverse-engineer a formula. The original calculation notebook or workbook would be needed to document the exact formula and reproduce the TPI from base inputs.

The report's approximate classification bands are:

- **Green:** TPI below 60.
- **Yellow:** TPI approximately 60-80.
- **Red:** TPI above 80.

## Forecasting

The submitted dashboard guide identifies Python 3.12, pandas, and Prophet. The report states that state-level TPI was forecast from 2023-Q2 through 2028-Q4, a 23-quarter horizon. The forecast output includes `yhat_lower` and `yhat_upper` fields.

The report does not provide forecast backtesting metrics or a documented train/test evaluation. Forecasts should therefore be presented as model outputs under the project's assumptions, not as validated guarantees.

## Policy simulation

The policy scenario compares `BAU` with `SeasonShift_Policy`. It models visitor demand moving away from three selected source hubs — Kuala Lumpur, Pahang, and Pulau Pinang — toward four receiving corridors — Kedah, Kelantan, Perak, and Terengganu.

The report and dashboard guide describe a baseline redistribution policy and a what-if slider. The guide says the slider scales a fixed baseline linearly. This is a scenario-scaling mechanism, not a fresh optimisation or independent recalculation at every slider value.

The report identifies the following reference assumptions:

- Tourist expenditure per arrival: RM4,276 (DOSM/MBSB reference in the project guide).
- Waste per person per day: 1.17 kg (SWCorp Malaysia reference).
- Water per room-night: 840 litres (SPAN MSIG, Section 2.2 reference).
- Carbon per room-night: 61.5 kg CO2e (DEFRA/DESNZ reference).
- Average length of stay: 2.82 nights (Tourism Malaysia reference).

The receiving destinations are assumed to have sufficient infrastructure capacity to absorb additional visitors. This assumption is not independently validated by the supplied data.

### Interpreting policy dashboard indicators

The dashboard displays approximately RM49.33 billion in redistributed spending, 38.07 thousand tonnes of waste change, and 1.18 million tonnes CO2e of carbon-footprint change. Inspection of the supplied policy CSV shows these correspond to gross absolute state-level changes: decreases in source states plus increases in receiving states are both counted.

The national BAU and policy totals for spending, waste, and carbon are effectively unchanged in the supplied CSV. Accordingly, the dashboard indicators should not be described as net nationwide savings or net new national spending. They represent the scale of redistribution across states under the model assumptions.

The report describes approximately 5.79 million visitor movements. The supplied policy CSV implies approximately 5.77 million one-way reallocations when absolute state-level arrival changes are summed and divided by two. The difference should be checked against the original upstream workbook if an exact headline figure is required.

## Limitations

1. **Missing source code:** no original Python notebook or scripts were supplied. The final data outputs and Power BI file are included, but the upstream cleaning, TPI calculation, and Prophet fitting cannot be fully rerun from this repository alone.
2. **TPI formula not documented:** the exact weighting/scaling formula is unavailable in the submitted files.
3. **Allocated state demand:** state demand is estimated from fixed shares of national arrivals, not observed state-level tourist arrival counts.
4. **No forecast validation metrics:** the report does not include backtesting errors or a held-out evaluation.
5. **Policy scenario assumptions:** receiving capacity is assumed, and policy outcomes are modelled estimates rather than observed effects.
6. **Linear slider scaling:** the what-if slider scales a fixed baseline rather than re-solving an optimisation model.
7. **External shocks:** the forecast does not account for black-swan events such as pandemics.
8. **Different data coverage windows:** arrivals, hotel inventory, AOR, and calendar features cover different periods. See `../data/README.md`.
9. **Slider range discrepancy:** the supplied dashboard guide describes a 5%-50% range, while the report text describes a different range. Verify the actual limits in the PBIX before quoting them.

## Responsible presentation

When using this project in a portfolio or interview:

- Separate historical observations, forecasts, and hypothetical policy scenarios.
- Describe the three policy source hubs as selected case-study targets, not as three historically Red-zone TPI units.
- Do not claim the policy simulation proves national waste or carbon reductions.
- Do not claim the full pipeline is reproducible until the original notebook/calculation workbook is recovered.
- Clearly state your own contribution separately from the team's collective work; the submitted report lists the team but does not allocate individual tasks.
