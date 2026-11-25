# Power BI Dashboard — SeasonShift

This folder contains the submitted Power BI report and page previews.

## File

- `SeasonShift_Dashboard.pbix` — Power BI Desktop report.

## Pages

1. **Overview:** baseline national tourist arrivals, summary cards, BAU versus SeasonShift trend, and state selection.
2. **Heatmap:** quarterly historical Tourism Pressure Index (TPI) by state for 2019-Q1 to 2023-Q1. The report classifies TPI below 60 as Green, approximately 60-80 as Yellow, and above 80 as Red.
3. **Forecast:** Prophet-based state-level TPI forecast from 2023-Q2 to 2028-Q4, with state and year filters.
4. **Policy:** BAU versus SeasonShift redistribution scenario, state-level movements, policy indicators, and a shift-rate control.

## Open the dashboard

1. Install Microsoft Power BI Desktop.
2. Open `SeasonShift_Dashboard.pbix`.
3. Use the page tabs at the bottom of the report.
4. Interact with the state/date/year selectors and policy control.

The submitted guide identifies Power BI Desktop (version 2.13x, 2026 release), native Power BI visuals, and embedded data. No custom visual, API key, or external data connection is required to view the packaged report.

## Important interpretation notes

- Kuala Lumpur, Pahang, and Pulau Pinang are the three selected policy source hubs. The historical TPI output identifies **Pahang alone** as having Red-zone records; do not call all three Red-zone states.
- The policy dashboard's spending, waste, and carbon cards reflect gross state-level changes. They should not be interpreted as net nationwide savings because the scenario redistributes demand between states.
- The policy slider scales a fixed baseline scenario linearly, according to the submitted guide; it is not a live optimisation engine.
- The guide describes the slider range as 5%-50%, while the narrative report describes a different range. Check the actual slider limits in Power BI Desktop before quoting the exact range.
- Forecast outputs are scenario/model estimates. The submitted report does not provide backtesting error metrics.

## Screenshots

- `screenshots/overview.png`
- `screenshots/historical-tpi-heatmap.png`
- `screenshots/prophet-forecast.png`
- `screenshots/policy-simulation.png`
