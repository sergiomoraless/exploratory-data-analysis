# Exploratory Data Analysis in MySQL — Tech Layoffs Dataset

## Overview
SQL exploratory analysis on a cleaned dataset of tech company layoffs.
The goal was to find patterns and trends: which companies, countries,
and time periods were most affected.

## Dataset
- **Source**: Tech layoffs data (cleaned in the companion project)
- **Period covered**: Queried using MIN/MAX date from the dataset
- **Table used**: `layoffs_staging2` (post-cleaning)

## Questions Explored

### Scale of layoffs
- Maximum employees laid off in a single event
- Companies that laid off 100% of their workforce (`percentage_laid_off = 1`)
  ordered by funding raised — to identify well-funded companies that still shut down

### By company
- Total layoffs per company (all-time ranking)
- Top 5 companies with most layoffs per year using `DENSE_RANK()`
  partitioned by year

### By geography & stage
- Total layoffs by country
- Total layoffs by company funding stage (Series A, B, Post-IPO, etc.)

### Over time
- Layoffs grouped by year
- Layoffs grouped by month using `SUBSTRING(date, 1, 7)`
- Rolling monthly total using `SUM() OVER(ORDER BY month)` window function

## Key Techniques Used
- Aggregate functions: `SUM()`, `MAX()`, `MIN()`
- `GROUP BY` with `ORDER BY` for rankings
- `SUBSTRING()` for extracting year-month from dates
- Window functions: `SUM() OVER()` for rolling totals, `DENSE_RANK() OVER(PARTITION BY)` for yearly rankings
- Multiple CTEs chained together (`Company_Year` → `Company_Year_Rank`)

## Files
```
eda-layoffs/
├── README.md
└── scripts/
    └── eda.sql
```

## Tools
- MySQL 8.0
- MySQL Workbench

## Related Project
[Data Cleaning — same dataset](https://github.com/TU_USUARIO/data-cleaning-layoffs)
