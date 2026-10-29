# Household Energy Consumption Dashboard (Power BI)

A one-page Power BI dashboard that shows a household's average power use over about two years, built from the UCI Individual Household Electric Power Consumption dataset.

![Dashboard](images/dashboard.png)

## About the data

The full dataset has 2,075,259 measurements, one per minute, from a house in Sceaux (7 km from Paris, France) between December 2006 and November 2010 (47 months). Besides the total active power, it has three sub-meters:

- **Sub_1:** kitchen (dishwasher, oven, microwave)
- **Sub_2:** laundry room (washing machine, tumble dryer, refrigerator, light)
- **Sub_3:** electric water heater and air conditioner

About 1.25% of the rows have missing values.

This dashboard uses the first 1,048,576 measurements, which cover December 2006 to December 2008. The file was cut at that point because it had been opened in Excel, whose row limit is 1,048,576.

**Source and license:** Hebrail, G. & Berard, A. (2006). Individual Household Electric Power Consumption [Dataset]. UCI Machine Learning Repository. https://doi.org/10.24432/C58K54. Licensed under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/).

The raw file (about 127 MB) is not included in this repository because of its size.

## What the dashboard shows

- Average power in kW, as a total and per circuit
- Power by hour of day, stacked by circuit. Each bar is the average over all the minutes at that hour, across every day of the selected year
- Monthly trend of the average power for the selected year
- A year slicer that filters the whole page. Clicking a bar or a point on a chart also filters the other visuals

## How it was built

**Power Query**
- Replaced the `?` missing-value marker with null and removed the empty rows
- Set the data types, reading the dates with the correct day/month/year locale
- Added helper columns for Hour, Year and Month

**DAX measures**
- Average total power in kW: `AVERAGE(Global_active_power)`
- Average per sub-meter in kW: `AVERAGE(Sub_metering_x) * 60 / 1000`
- Remaining power not covered by the sub-meters: total minus the three sub-meters

**Visuals**
- Cards, a stacked column chart by hour, an area chart by month and a year slicer
- Custom layout, colors and header image

## Notes

- `Global_active_power` is in kW and the sub-meters are in Wh per minute. The measures convert the sub-meters to kW, so all values use the same unit and can be compared.
- The "Other" part of each column is the power that none of the three sub-meters measure.

## Files

- `household_energy_dashboard_2.pbix`: the Power BI report (open with Power BI Desktop)
- `images/dashboard.png`: screenshot of the report
