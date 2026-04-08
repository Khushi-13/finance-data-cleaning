# finance-data-cleaning
# Watch Me Do Data Analysis — Cleaning Messy Financial Data in SQL

## Overview

In this project, I took a real-world financial dataset with 10,000+ rows and a completely broken `amount` column — containing dollar signs, commas, and random text like "Declined" and "Pending" — and cleaned it using just 3 SQL functions in SQL Server. I then answered one business question:

> **Which spending category grew the fastest over 5 years?**

---

## Tools & Environment

- **Database**: SQL Server (SSMS)
- **Dataset**: `finance.dbo.raw_transactions_final` — 10,000+ rows of raw transaction data

---

## What I Did

### Step 1 — Clean the messy `amount` column

The `amount` column had mixed content: dollar signs, commas, and non-numeric values like "Declined", "Pending", and "Refunded". I used three functions to handle this:

- **`REPLACE`** — stripped `$` and `,` from numeric strings
- **`TRIM`** — removed hidden whitespace that causes silent query failures
- **`TRY_CAST`** — safely converted text to `DECIMAL(10,2)`, returning `NULL` for bad values instead of crashing

### Step 2 — Aggregate spend by category and year

Used `SUM()` with `GROUP BY category, year` inside a CTE to get total annual spend per category.

### Step 3 — Calculate year-over-year % change

Used the `LAG()` window function partitioned by `category` and ordered by `year` to pull each category's prior year spend, then calculated:

![Over year change] (https://github.com/Khushi-13/finance-data-cleaning/blob/main/over_year_change.png)
