# LA Crime Insights Dashboard

## Description
**LA Crime Insights Dashboard**: Analyze 2020 Los Angeles crime data with an interactive Excel dashboard featuring slicers, charts, and hyperlinks to uncover crime patterns, 
victim demographics, and spatial-temporal trends using pivot tables and formulas.

## Overview
The **LA Crime Insights Dashboard** is an Excel-based project that analyzes crime data from Los Angeles in 2020. It features an interactive dashboard with slicers, charts, and hyperlinks, 
providing insights into crime patterns, victim demographics, and spatial-temporal trends. Built using Excel's powerful features like pivot tables, formulas, and VBA (optional), this project 
aims to deliver a user-friendly tool for exploring crime statistics.

## Dataset
- **Scope**: Crime incidents in Los Angeles reported in 2020.
- **Key Columns**:
  - `DR_NO`: Incident ID
  - `DATE OCC`: Date of occurrence
  - `AREA NAME`: Geographic area (e.g., Southwest, Hollywood)
  - `Crm Cd Desc`: Crime description (e.g., Robbery, Battery)
  - `Vict Age`, `Vict Sex`, `Vict Descent`: Victim demographics
  - `Weapon Desc`: Weapon used
  - `Premis Desc`: Location of crime
  - `LAT`, `LON`: Geographic coordinates

## Features
- **Data Cleaning**:
  - Standardized dates (`DATE OCC`) and times ('TIME OCC').
  - Handled missing values: `Vict Age` (0 or blank) replaced with "N/A".
- **Analyses**:
  - Crime frequency by area, crime type, and time (day/hour).
  - Victim demographics (age groups, sex).
  - Premises and weapons used in crimes.
- **Interactive Dashboard**:
  - Slicers for filtering by `AREA NAME`, `Crm Cd Desc`, `Vict Sex`, and `Date Occurred`.
  - Charts: Bar (area-wise crimes), Pie (crime types), Histogram (victim age), Line (hourly trends).
- **Navigation**:
  - Hyperlinks via a Table of Contents (TOC) sheet to jump between raw data, cleaned data, analysis, and dashboard.
- **Optional VBA**: Macro to refresh all pivot tables with a button click.

## Progress Log
- **Day 1 (2025-04-02)**: Initialized repository, imported raw crime data into Excel as 'Raw Data' sheet.
- **Day 2 (2025-04-02)**: Cleaned the dataset in a new `Cleaned Data` sheet to prepare it for analysis. Steps included:
  - Copied all data from `Raw Data` to `Cleaned Data` for processing.
  - Standardized `DATE OCC` (column C) into a `Date Occurred` column using `=DATEVALUE(LEFT(C2,10))` to extract the date (e.g., "2020-01-01") from the full timestamp (e.g., "2020-01-01 12:30:00"), formatted as 
    MM/DD/YYYY.
  - Converted `TIME OCC` (column D) from numeric format (e.g., 1340 for 1:40 PM) to a `Time Occurred` column with `=TIME(INT(D2/100),MOD(D2,100),0)`, formatted as HH:MM AM/PM for time-based analysis.
  - Handled missing values:
    - `Vict Age` (column L): Added `Cleaned Vict Age` (column M) with `=IF(OR(L2=0,L2=""),"N/A",L2)` to replace 0 or blank entries with "N/A", preserving valid ages (e.g., 23, 55).
    - `Vict Sex` (column M): Added `Cleaned Vict Sex` (column N) with `=IF(M2="X","Unknown",M2)` to replace "X" (unknown) with "Unknown", keeping "M" or "F" as-is.
    - `Vict Descent` (column N): Added `Cleaned Vict Descent` (column O) with `=IF(N2="X","Unknown",N2)` to mark "X" as "Unknown", retaining valid descent codes (e.g., "H", "W").
  - Formatted the cleaned dataset as an Excel table named `CrimeData` (Ctrl+T) to enable dynamic referencing for pivot tables and slicers.
  - Verified data integrity by filtering for "N/A" and "Unknown" values to ensure proper handling of missing entries.
- **Day 3 (2025-04-03)**: Enhanced `Analysis` sheet in `la_crime_insights_dashboard.xlsx` with 6 pivot tables and charts for valuable dashboard insights. Steps included:
  - Added pivot tables:
    - **Crime by Area**: Rows = `AREA NAME`, Values = Count of `DR_NO` (A3).
    - **Top 5 Crime Types**: Rows = `Crm Cd Desc`, Values = Count of `DR_NO`, filtered top 5 (G3).
    - **Victim Age**: Rows = `Age Group` (helper column: `=IF(M2="N/A","Unknown",IF(M2<=18,"0-18",IF(M2<=30,"19-30",IF(M2<=50,"31-50","51+"))))`), Values = Count of `DR_NO` (M3).
    - **Crime by Hour**: Rows = `Hour` (`=HOUR([@[Time Occurred]])`), Values = Count of `DR_NO` (S3).
    - **Crime by Sex and Age**: Rows = `Age Group`, Columns = `Cleaned Vict Sex`, Values = Count of `DR_NO` (Y3).
    - **Top 5 Weapons**: Rows = `Weapon Desc`, Values = Count of `DR_NO`, filtered top 5 (AE3).
  - Created charts:
    - Bar: “Crime Distribution by Area” (A25).
    - Pie: “Top 5 Crime Types” (G25).
    - Histogram: “Victim Age Distribution” (M25, Gap Width = 0%).
    - Line: “Crime Trends by Hour of Day” (S25).
    - Stacked Bar: “Crime by Victim Sex and Age Group” (Y25).
    - Column: “Top 5 Weapons Used in Crimes” (AE25).
  - Positioned charts below pivot tables for clarity.
  - Updated the Excel file in the repository with these analyses.
 
  
## Key Insights
- Highest crime area: Southwest (based on initial analysis).
- Most common crime: Battery - Simple Assault.
- Peak crime hours: Evening (6 PM - 10 PM).

## Tools Used
- **Microsoft Excel**: Data cleaning, pivot tables, charts, slicers, and hyperlinks.
- **GitHub**: Version control and project showcase.

## Future Improvements
- Add geographic mapping using `LAT` and `LON` (requires Power BI or external tools).
- Expand VBA for more automation (e.g., custom filters).
- Include 2021+ data for trend analysis.

## Credits
- Developed by [Madhav Jee].
- Dataset provided by [Data.gov].

## License
This project is for educational purposes and not licensed for commercial use. Feel free to fork and explore!
