# Global Layoffs Data Analysis

## Executive Summary

This project analyzes global layoff trends across companies, industries, countries, and time periods using SQL and Tableau. The workflow includes data cleaning, data standardization, exploratory analysis, time-series analysis, company ranking, and dashboard development.

Using SQL, I cleaned and transformed the raw layoffs dataset by removing duplicates, standardizing text fields, resolving missing industry values, converting date fields, and removing records without usable layoff information. I then used SQL analysis to identify layoff trends by industry, company, year, and month.

The final Tableau dashboard visualizes total layoffs, company-level impact, industry trends, monthly layoff patterns, and the relationship between company funding and layoffs.

## Business Questions

- Which industries experienced the highest number of layoffs?
- Which companies reported the most layoffs overall?
- How did layoffs trend over time?
- Which companies had the highest layoffs by year?
- Which companies raised significant funding while reporting relatively fewer layoffs?
- What patterns can be identified across industries, companies, and time periods?

## Tools Used

- SQL: data cleaning, transformation, exploratory analysis, ranking, and time-series analysis
- Tableau: dashboard development and data visualization
- CSV/Excel: source dataset review

## Dataset

- Source: [Layoffs Dataset](https://github.com/AlexTheAnalyst/MySQL-YouTube-Series/blob/main/layoffs.csv)
- Rows before cleaning: 2,361
- Columns: 9
- Time period: March 2020 to March 2023

Note: In this dataset, `percentage_laid_off` is stored as a ratio where `1` represents 100% of the workforce laid off.

## Project Structure

- data
  - raw data.csv
  - cleaned data.csv

- sql
  - Data Cleaning.sql
  - Exploratory Data Analysis.sql

- tableau
  - global layoffs dashboard.twbx
  - dashboard_screenshot.png

## Data Cleaning Summary

The raw dataset was cleaned and prepared for analysis using SQL.

Cleaning steps included:

- Created staging tables to preserve the raw dataset
- Removed duplicate records using `ROW_NUMBER`
- Trimmed whitespace from company names
- Standardized inconsistent industry values, including crypto-related categories
- Standardized country names, including removing trailing punctuation
- Converted the `date` field from text to a proper SQL date format
- Filled missing industry values where another record from the same company had a known industry
- Removed records where both `total_laid_off` and `percentage_laid_off` were missing
- Removed temporary cleaning columns after validation

## Key Metrics And Analyses

- Total layoffs by industry
- Total layoffs by company
- Monthly layoff totals
- Rolling total layoffs over time
- Top companies by layoffs per year
- Companies ranked by funding raised
- Company-level comparison of funding raised and layoffs reported

## SQL Techniques Used

- Staging table creation
- Duplicate detection with `ROW_NUMBER`
- Text cleaning with `TRIM`
- Data standardization with `UPDATE`
- Date conversion with `STR_TO_DATE`
- Self-joins to fill missing values
- Aggregations with `SUM` and `MAX`
- Time-series analysis with `DATE_FORMAT`
- Window functions including `ROW_NUMBER`, `RANK`, `DENSE_RANK`, and `SUM OVER`
- CTEs for multi-step analysis

## SQL Files

- [Data Cleaning.sql](sql/Data%20Cleaning.sql)
- [Exploratory Data Analysis.sql](sql/Exploratory%20Data%20Analysis.sql)

## Tableau Dashboard

View the interactive dashboard on Tableau Public: [Global Layoffs Dashboard](https://public.tableau.com/app/profile/kevin.lim7109/viz/globallayoffsdashboard/layoffsdashboard)

The dashboard includes:

- KPI cards for total layoffs and company count
- Monthly layoff trend analysis
- Industry-level layoff breakdown
- Company-level layoff comparison
- Funding vs layoffs analysis
- Interactive filters for exploring layoff patterns

![Dashboard Screenshot](tableau/dashboard_screenshot.png)

## Key Insights

- Consumer and retail were among the industries with the highest total layoffs during the analyzed period.
- Layoffs peaked during specific periods, reflecting major shifts in economic conditions and company cost-cutting behavior.
- In 2020, travel and transportation-related companies appeared heavily impacted, likely reflecting the effect of COVID-19 on mobility and consumer activity.
- In 2023, major technology companies such as Google, Microsoft, and Amazon appeared among the companies with the highest reported layoffs.
- Some companies raised high levels of funding while reporting comparatively lower layoffs, making them useful cases for further business review.

## Funding vs Layoffs Scoring Model

A weighted ranking model was created to compare companies by funding raised and total layoffs reported.

The model ranks companies using:

- Funding rank: companies with higher total funding receive stronger funding ranks
- Layoff rank: companies with lower total layoffs receive stronger layoff ranks
- Weighted score: funding rank weighted at 70% and layoff rank weighted at 30%

Note: This model is not intended to measure profitability or overall company health. It is a simple analytical framework for identifying companies that raised significant funding while reporting relatively fewer layoffs. I assigned a higher weight to fundraising (70%) because the primary objective was to identify companies that successfully attracted capital while still considering layoffs as an indicator of operational efficiency. The weights can be adjusted depending on the business objective.

## Recommendations

- Use industry-level layoff trends to identify sectors most affected by economic downturns or market corrections.
- Review companies with high layoffs and high funding separately, as funding alone does not guarantee workforce stability.
- Track monthly layoff trends to identify periods of increased labor market pressure.
- Compare layoff trends across industries to better understand which sectors may be more sensitive to macroeconomic changes.
- Treat the funding vs layoffs score as a starting point for deeper research, not a final measure of company performance.

## Limitations

- The dataset may not include every layoff event globally.
- Funding raised is not the same as revenue, profit, or financial stability.
- Layoff totals do not account for company size unless percentage laid off is available.
- Some records have missing values, which limits certain comparisons.
- The analysis is descriptive and does not prove why layoffs occurred.
- The scoring model is a simplified ranking method and should not be interpreted as a complete company performance metric.

## What I Learned

- How to clean and standardize messy real-world data using SQL
- How to use window functions to remove duplicates and rank results
- How to perform time-series analysis using SQL date functions
- How to create rolling totals with `SUM OVER`
- How to use self-joins to fill missing values
- How to translate SQL analysis into a Tableau dashboard for business storytelling
