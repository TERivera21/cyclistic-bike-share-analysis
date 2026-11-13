# Cyclistic Bike-Share Analysis
### How annual members and casual riders use bikes differently

**By Teresa E. Rivera | Google Data Analytics Capstone**  
**Tools:** SQL (SQLite), SQLiteStudio, Excel  
**Data:** September 2025–August 2026 monthly files | **6,115,947 cleaned ride records**

For my Google Data Analytics capstone, I analyzed more than **6.1 million bike-share rides** to understand how annual members and casual riders use the service differently.

I used Excel and SQL in SQLiteStudio to prepare and validate the data, investigate duplicate records and unusual ride durations, and compare riding patterns. My goal was to use those findings to recommend ways Cyclistic could encourage casual riders to become annual members.

[View the presentation](Cyclistic%20Bike-Share%20Analysis.pdf) · [Explore the SQL analysis](Cyclistic%20Data%20Analysis) · [Review data validation and cleaning](Cyclistic%20Data%20Validation)

## Business question

**How do annual members and casual riders use Cyclistic bikes differently?**

I compared ride duration, day-of-week patterns, and weekday start times to identify opportunities for membership messaging. Cyclistic is the fictional company in the Google Data Analytics case study; I used public Divvy trip data for the analysis.

## Key findings

Casual riders took longer rides on average—**20.70 minutes compared with 12.37 minutes** for members, a difference of **8.33 minutes**. Casual rides peaked on **Saturday, with 456,660 rides**, while member rides peaked on **Wednesday, with 631,952 rides**. Tuesday and Thursday member volumes were close behind.

During the week, members showed peaks at **8 a.m. and 5 p.m.**, suggesting that some may use the service for commuting. Casual rides also peaked at **5 p.m.** These patterns helped me identify opportunities to test weekend and commuting-focused membership messages.

Duration averages include positive-duration rides only. Counts describe **rides, not unique riders**. The hourly weekday comparison covers Monday–Friday.

## Recommendations

Based on these findings, I recommend:

1. **Testing membership offers after weekend rides**, especially on Saturdays, using in-app messaging where targeting is available.
2. **Reviewing pricing to determine when a membership would benefit frequent casual riders.** This would require pricing and rider-frequency data to calculate a break-even point.
3. **Comparing commuting-focused messages with general membership messages** for eligible casual riders taking weekday rides between 5:00 and 5:59 p.m.

These recommendations would need to be tested. The analysis shows differences in riding behavior, but it does not tell us why someone rides or whether they would purchase a membership. I would measure results using **membership conversion rates** before expanding successful campaigns.

## Data preparation and quality checks

- I preserved source CSV files separately from working copies.
- I compared record counts and start/end timestamps between CSV and Excel copies.
- I combined 12 monthly files in SQLite.
- I prepared ride-duration and day-of-week fields for analysis.
- I investigated repeated ride IDs and removed **35 duplicate records** when creating `cyclistic_clean` with distinct combinations of the selected fields.
- I retained **29 negative-duration records** in the clean dataset but excluded them from average-duration calculations.
- I used explicit numeric casts for duration calculations and inspected unusually long rides.

I also explored whether a one-hour clock change could explain the negative durations by adding 60 minutes in a diagnostic query. I kept the original values; that calculation does not confirm the cause. Very long positive rides remain in the averages.

## Repository contents

| File | Purpose |
| --- | --- |
| [Cyclistic Bike-Share Analysis.pdf](Cyclistic%20Bike-Share%20Analysis.pdf) | Presentation covering the business task, preparation, findings, recommendations, and next steps. |
| [Cyclistic Data Validation](Cyclistic%20Data%20Validation) | Raw-table inspection, date-coverage checks, duplicate investigation, and clean-table creation. |
| [Cyclistic Data Analysis](Cyclistic%20Data%20Analysis) | Clean-table quality checks and rider comparisons by duration, day, and start hour. |

The two code files contain SQLite SQL, with comments explaining the original exploratory queries.

## How to follow the analysis

The published scripts start **after data import and derived-field preparation**; they are not a complete automated pipeline from the original CSV files.

1. Obtain the September 2025–August 2026 monthly files from the [Divvy trip-data archive](https://divvy-tripdata.s3.amazonaws.com/index.html).
2. Prepare and combine the files into a SQLite table named `cyclistic`. The validation script's final `SELECT` lists the required columns. These include the derived fields `ride_length`, `ride_length_minutes`, and `day_of_week`.
3. Use timestamps beginning with a consistent `YYYY-MM-DD` date and day codes **1 = Sunday through 7 = Saturday**, matching the weekday filter in the analysis.
4. Run the queries in **Cyclistic Data Validation** in order to inspect the raw table and create `cyclistic_clean`. The clean-table creation statement requires that the destination table does not already exist.
5. Run the queries in **Cyclistic Data Analysis** to review quality checks, duration averages, and ride counts.
6. Compare the outputs with the findings in the presentation.

The original queries are preserved, including exploratory checks that revisit similar questions. The preparation formulas and import steps are not included in these scripts. The public repository contains the code and presentation rather than the full CSV collection or SQLite database.

## Scope and limitations

- Aggregate ride patterns do not identify individual riding frequency, motivations, or membership-conversion likelihood.
- Commuting is an interpretation of timing patterns, not a measured trip purpose.
- The analysis does not establish that any proposed marketing strategy will increase conversions.
- Membership value requires pricing and rider-level frequency information beyond the comparisons presented here.
- Very long positive rides can influence mean duration; this analysis does not apply an upper-duration cutoff.
- The period refers to the selected monthly files. The validation script investigates rides starting before September 2025; it does not apply a strict start-date exclusion.
- SQL annotations explain query behavior; they do not represent a new execution of the full source database.

## Sources and attribution

- **Trip data:** [Divvy historical trip-data archive](https://divvy-tripdata.s3.amazonaws.com/index.html), September 2025–August 2026 monthly files.
- **Data terms:** [Divvy Data License Agreement](https://divvybikes.com/data-license-agreement).
- **Case-study framework:** *Case Study 1: How does a bike-share navigate speedy success?*, Google Data Analytics Professional Certificate.
- **Presentation imagery:** Microsoft PowerPoint stock images.
- **Analysis and visualizations:** Teresa E. Rivera, using SQLiteStudio and Excel.

This is an independent educational portfolio project and does not imply affiliation with or endorsement by Divvy.

## More of my work

[SQL portfolio](https://github.com/TERivera21/SQL) · [Tableau dashboards](https://public.tableau.com/app/profile/teresa.rivera2171/vizzes)
