# Cyclistic Bike-Share Analysis
### How annual members and casual riders use bikes differently

**By Teresa E. Rivera | Google Data Analytics Capstone**  
**Tools:** SQL (SQLite), SQLiteStudio, Excel  
**Data:** September 2025–August 2026 monthly files | **6,115,947 cleaned ride records**

Casual rides averaged **20.70 minutes**, compared with **12.37 minutes** for annual members. Casual ride volume peaked on Saturdays, while member rides peaked midweek and showed weekday morning and evening peaks. This analysis translates those differences into membership-marketing hypotheses to test.

[View the presentation](Cyclistic%20Bike-Share%20Analysis.pdf) · [Explore the SQL analysis](Cyclistic%20Data%20Analysis) · [Review data validation and cleaning](Cyclistic%20Data%20Validation)

## Business question

**How do annual members and casual riders use Cyclistic bikes differently?**

The goal is to identify differences in ride duration and usage patterns that can inform strategies for converting casual riders into annual members. Cyclistic is the fictional company in the Google Data Analytics case study; the analysis uses public Divvy trip data.

## Key findings

| Area | Finding | Business interpretation |
| --- | --- | --- |
| Ride duration | Casual rides averaged **20.70 minutes**, versus **12.37 minutes** for member rides—an **8.33-minute difference**. | Different ride patterns provide a basis for testing tailored membership messages. Duration alone does not establish trip purpose. |
| Day of week | Casual rides peaked on **Saturday: 456,660 rides**. Member rides peaked on **Wednesday: 631,952 rides**, with Tuesday and Thursday close behind. | Weekend rides offer a potential opportunity to test membership messaging for casual riders. |
| Weekday start hour | Member rides had a morning peak at **8 a.m.** and their highest peak at **5 p.m.** Casual rides also peaked at **5 p.m.** | Member patterns are consistent with possible commuting use; weekday evening casual rides provide an audience for testing commuting-focused messages. |

Duration averages include positive-duration rides only. Counts describe **rides, not unique riders**. Hourly weekday findings cover Monday–Friday.

## Recommendations

1. **Test weekend membership messaging.** Present an in-app annual-membership offer after a casual weekend ride, especially on Saturday, subject to available targeting capabilities.
2. **Evaluate value for frequent riders.** Use current pricing and rider-frequency data to calculate a membership break-even point, then test relevant value messaging.
3. **Test weekday commuting messages.** Compare commuting-focused and general membership messages for eligible casual riders taking weekday rides between 5:00 and 5:59 p.m.

Use **membership conversion rates** to evaluate pilot results before expanding campaigns. These are proposed tests, not implemented campaigns or demonstrated conversion gains.

## Data preparation and quality checks

- Preserved source CSV files separately from working copies.
- Compared record counts and start/end timestamps between CSV and Excel copies.
- Combined 12 monthly files in SQLite.
- Prepared ride-duration and day-of-week fields for analysis.
- Investigated repeated ride IDs and removed **35 duplicate records** when creating `cyclistic_clean` with distinct combinations of the selected fields.
- Retained **29 negative-duration records** in the clean dataset but excluded them from average-duration calculations.
- Used explicit numeric casts for duration calculations and inspected unusually long rides.

The SQL includes a diagnostic calculation adding 60 minutes to negative durations to explore a possible clock-change explanation. It does **not** alter the records or establish that explanation as confirmed. Positive extreme durations remain in the averages.

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
