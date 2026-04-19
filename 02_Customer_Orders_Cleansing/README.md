# 🧹 Customer Sales Dataset Cleansing

## 📌 Project Overview
A professional data cleaning project on a real-world sales dataset 
containing 20,000+ orders across 7 countries. Raw messy data was 
inspected, cleaned, validated and documented following industry 
best practices.

## 📊 Dataset
- **Source:** Kaggle (Orders.csv)
- **Size:** 20,004 rows × 19 columns (raw)
- **Domain:** Retail Sales — Electronics

## 🔍 Problems Found & Fixed

| Issue | Count | Action |
|---|---|---|
| Empty rows | 4 | Dropped |
| Duplicate rows | 3 | Dropped |
| Missing values | 1,187 | Filled / Dropped |
| Mixed date formats | 12,003 affected | Fixed with dayfirst=True |
| Phone prefix "Tel: " | All rows | Removed |
| Email inconsistent casing | All rows | Standardized to lowercase |
| City lowercase | All rows | Title Case applied |
| Discount > Unit Price | 121 rows | Flagged for client |

## ⚙️ Tools & Libraries
- Python
- Pandas
- NumPy
- Regex
- Jupyter Notebook

## 📁 Project Structure
```
customer-sales-cleansing/
│
├── Orders.csv                  # Raw dataset
├── orders_cleaned.csv          # Final clean dataset
├── Customer_Sales_Cleansing.ipynb       # Full notebook with steps
└── README.md
```

## ✅ Final Output
- **Rows:** 20,000 (clean)
- **Columns:** 24 (19 original + 5 added)
- **Missing Values:** 0
- **Duplicates:** 0

## 💡 Key Findings
- Saudi Arabia has highest orders (6,077)
- Jeddah is top performing city (3,186 orders)
- Laptops are most popular category (2,173 units)
- 121 discount anomalies flagged for business review
- Status column needs client clarification (True/False values)

## 🧠 What I Learned
- Always inspect fully before touching data
- Check nulls immediately after every operation
- Mixed date formats are common in real datasets
- dayfirst=True handles DD/MM/YYYY format
- Discount stored as money amount not percentage
- Professional analysts flag issues — not silently fix everything

## 👩‍💻 Author
**Umehabiba** — Data Cleaning Beginner  
BS Information Technology | Rawalpindi, Pakistan  
Available for freelance data cleaning projects on LinkedIn : www.linkedin.com/in/ume-habiba-88313537b
