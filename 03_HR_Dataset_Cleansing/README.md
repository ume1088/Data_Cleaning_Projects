# 🧹 HR Dataset Cleaning Project

A professional data cleaning project on a real-world HR dataset using Python and Pandas — handling messy, inconsistent, and hidden dirty data end to end.

---

## 📌 Project Overview

| Property | Details |
|---|---|
| **Dataset** | HR Dataset |
| **Rows** | 1000 |
| **Columns** | 10 |
| **Tools** | Python, Pandas, word2number, NumPy |
| **Level** | Data Cleaning & Preprocessing |

---

## 📂 Dataset Columns

```
Name, Age, Salary, Gender, Department, Position,
Joining Date, Performance Score, Email, Phone Number
```

---

## 🔍 Problems Found During Inspection

| Column | Issue |
|---|---|
| Age | String dtype, 335 word-form values (e.g. "twenty five"), 159 nulls |
| Salary | String dtype, 310 word-form values, 167 hidden nulls (' NAN ' string) |
| Joining Date | Mixed date formats |
| Phone Number | 185 nulls + 191 hidden nulls (blank spaces) |
| Email | 390 nulls |
| All Columns | Incorrect dtypes — everything loaded as string |

---

## 🧹 Cleaning Steps

### Step 1: Word to Number Conversion
Detected word-form values using `.str.isdigit()` negation, then converted using `word2number`. Used `try-except` to handle invalid strings like `' NAN '` gracefully.

```python
from word2number import w2n

# Age
df['Age'] = df['Age'].apply(lambda x: w2n.word_to_num(x) if isinstance(x, str) else x)

# Salary
def convert_salary(x):
    if isinstance(x, str):
        if x.strip().isdigit():
            return int(x)
        else:
            try:
                return w2n.word_to_num(x)
            except:
                return None
    return x

df['Salary'] = df['Salary'].apply(convert_salary)
```

---

### Step 2: Dtype Conversion

```python
# Category columns
for col in ['Gender', 'Department', 'Position', 'Performance Score']:
    df[col] = df[col].astype('category')

# Datetime
df['Joining Date'] = pd.to_datetime(df['Joining Date'], format='mixed', dayfirst=True, errors='coerce')

# Int — after null handling
df['Age'] = df['Age'].astype(int)
df['Salary'] = df['Salary'].astype(int)
```

---

### Step 3: Null Handling

| Column | Strategy | Reason |
|---|---|---|
| Age | Position-wise mean | Age varies by seniority level |
| Salary | Department-wise mean | Pay scale varies by department |
| Email | Left as NaN | Cannot be guessed — contact via phone |
| Phone Number | Left as NaN | Cannot be guessed — contact via email |

```python
df['Age'] = df['Age'].fillna(df.groupby('Position')['Age'].transform('mean'))
df['Salary'] = df['Salary'].fillna(df.groupby('Department')['Salary'].transform('mean'))
```

---

### Step 4: Formatting & Standardization

```python
df['Name'] = df['Name'].str.strip().str.title()
df['Email'] = df['Email'].str.strip().str.lower()
df['Phone Number'] = df['Phone Number'].str.strip()
df['Phone Number'] = df['Phone Number'].replace('', np.nan)
```

---

### Step 5: Save Cleaned Data

```python
df.to_csv('hr_cleaned.csv', index=False)
```

---

## 📊 Final Dataset Status

| Column | Dtype | Nulls | Status |
|---|---|---|---|
| Name | str | 0 | ✅ Clean |
| Age | int64 | 0 | ✅ Clean |
| Salary | int64 | 0 | ✅ Clean |
| Gender | category | 0 | ✅ Clean |
| Department | category | 0 | ✅ Clean |
| Position | category | 0 | ✅ Clean |
| Joining Date | datetime64 | 0 | ✅ Clean |
| Performance Score | category | 0 | ✅ Clean |
| Email | str | 390 | ✅ Intentional |
| Phone Number | str | 376 | ✅ Intentional |

---

## 💡 Key Decisions & Lessons

- **Convert, don't drop** — word-form values are recoverable, dropping = unnecessary data loss
- **Inspect before cleaning** — hidden nulls (`' NAN '`, blank spaces) are invisible to `.isna()`
- **Smart null filling** — position-wise and department-wise means are more realistic than overall averages
- **Dtype order matters** — int cannot hold NaN, so null handling must come before int conversion
- **Save df_before** — always keep a copy of raw data before cleaning begins

---

## 🛠️ Libraries Used

```python
import pandas as pd
import numpy as np
from word2number import w2n
```

---

## 👩‍💻 Author

**Ume Habiba**  
BS Information Technology | Data Cleaning Specialist  
[LinkedIn](www.linkedin.com/in/ume-habiba-88313537b) 
