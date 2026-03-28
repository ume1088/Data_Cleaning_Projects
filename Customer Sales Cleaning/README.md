
# Cafe Sales Data Cleaning

## Overview
Real-world messy cafe sales dataset cleaned using Python and Pandas.
Dataset contains 10,000 transactions with multiple data quality issues.

## Problems Found & Solved

| Problem | Detail | Solution |
|---|---|---|
| Missing values | Location 32.65%, Payment Method 25.79% | Filled with 'unknown' |
| Dirty values | 3,256 ERROR and UNKNOWN entries | Replaced with NaN |
| Wrong data types | 3 numeric columns stored as string | Converted to float64 |
| Date as string | Transaction Date unreadable | Converted to datetime64 |
| Total Spent errors | Inconsistent with Quantity × Price | Recalculated from scratch |

## Dataset
- Source: Kaggle — Cafe Sales Dirty Data
- Raw: 10,000 rows × 8 columns
- Cleaned: 10,000 rows × 11 columns

## New Features Added
- Month, Day, Year extracted from Transaction Date

## Tools Used
- Python, Pandas, NumPy, Matplotlib, Seaborn

## Files
- `cafe_sales.csv` — original dirty dataset
- `Customer_Analysis.ipynb` — full cleaning notebook
- `cleaned_cafe_sales.csv` — cleaned output

## How to Run
```bash
pip install pandas numpy matplotlib seaborn
jupyter notebook Customer_Analysis.ipynb
```

## Author

**Ume Habiba**
- LinkedIn: www.linkedin.com/in/ume-habiba-88313537b
- GitHub: https://github.com/ume1088
- Email: umehabiba1088@gmail.com

---
*This project was completed as part of self-learning data cleaning techniques 
using Python and Pandas.*
