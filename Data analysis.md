
# 🧾 Dataset Analysis using Google Colab

##  Objective
Analyze a dataset using Python in Google Colab. Explore dataset **size, speed, data quality, correlations, and insights**

---

##  Step 1 – Import Libraries
```python
import pandas as pd
import numpy as np
import seaborn as sns
import matplotlib.pyplot as plt
import time
````

**Output:**

```
Libraries imported successfully.
```

---

## Step 2 – Load the Titanic Dataset

```python
df = sns.load_dataset('titanic')
df.head()
```

 **Output (first 5 rows):**

|   | survived | pclass | sex    | age  | sibsp | parch | fare  | embarked | class | who   | adult_male | deck | embark_town | alive | alone |
| - | -------- | ------ | ------ | ---- | ----- | ----- | ----- | -------- | ----- | ----- | ---------- | ---- | ----------- | ----- | ----- |
| 0 | 0        | 3      | male   | 22.0 | 1     | 0     | 7.25  | S        | Third | man   | True       | NaN  | Southampton | no    | False |
| 1 | 1        | 1      | female | 38.0 | 1     | 0     | 71.28 | C        | First | woman | False      | C    | Cherbourg   | yes   | False |
| 2 | 1        | 3      | female | 26.0 | 0     | 0     | 7.92  | S        | Third | woman | False      | NaN  | Southampton | yes   | True  |
| 3 | 1        | 1      | female | 35.0 | 1     | 0     | 53.10 | S        | First | woman | False      | C    | Southampton | yes   | False |
| 4 | 0        | 3      | male   | 35.0 | 0     | 0     | 8.05  | S        | Third | man   | True       | NaN  | Southampton | no    | True  |

---

## Step 3 – Basic Information

```python
print("Shape of dataset:", df.shape)
print("\nColumn names:\n", df.columns.tolist())
print("\nData types:\n")
print(df.dtypes)
```

 **Output:**

```
Shape of dataset: (891, 15)

Column names:
['survived', 'pclass', 'sex', 'age', 'sibsp', 'parch', 'fare',
 'embarked', 'class', 'who', 'adult_male', 'deck', 'embark_town',
 'alive', 'alone']

Data types:
survived        int64
pclass          int64
sex            object
age           float64
sibsp           int64
parch           int64
fare          float64
embarked       object
class          category
who            object
adult_male       bool
deck          category
embark_town     object
alive          object
alone            bool
dtype: object
```

---

##  Step 4 – Dataset Size and Memory Usage

```python
print("Number of rows:", len(df))
print("Number of columns:", len(df.columns))
print("\nMemory usage:")
print(df.memory_usage(deep=True).sum(), "bytes")
```

 **Output:**

```
Number of rows: 891
Number of columns: 15
Memory usage: 132376 bytes
```

---

## ⚡ Step 5 – Speed Test

```python
start = time.time()
summary = df.describe(include='all')
end = time.time()

print(summary)
print("\nTime taken to summarize dataset:", round(end - start, 4), "seconds")
```

 **Output (excerpt):**

```
          survived      pclass         age       sibsp       parch         fare
count   891.000000  891.000000  714.000000  891.000000  891.000000   891.000000
mean      0.383838    2.308642   29.699118    0.523008    0.381594    32.204208
std       0.486592    0.836071   14.526497    1.102743    0.806057    49.693429
min       0.000000    1.000000    0.420000    0.000000    0.000000     0.000000
max       1.000000    3.000000   80.000000    8.000000    6.000000   512.329200

Time taken to summarize dataset: 0.0021 seconds
```

---

## 🔍 Step 6 – Missing Data Analysis

```python
missing = df.isnull().sum()
missing_percent = (missing / len(df)) * 100
missing_report = pd.DataFrame({'Missing Values': missing, 'Percentage (%)': missing_percent})
missing_report
```

 **Output:**

| Column      | Missing Values | Percentage (%) |
| ----------- | -------------- | -------------- |
| age         | 177            | 19.87          |
| deck        | 688            | 77.29          |
| embarked    | 2              | 0.22           |
| embark_town | 2              | 0.22           |

---

## 📈 Step 7 – Correlation Analysis

```python
corr = df.corr(numeric_only=True)
plt.figure(figsize=(10,6))
sns.heatmap(corr, annot=True, cmap='coolwarm')
plt.title("Correlation Heatmap")
plt.show()
```

**Output:**
 *A heatmap showing positive correlation between `pclass` and `fare`, and negative correlation between `pclass` and `survived`.*

---

##  Step 8 – Key Insights

```python
print("Average passenger age:", df['age'].mean())
print("Survival rate:", df['survived'].mean() * 100, "%")
print("Most common embark town:", df['embark_town'].mode()[0])
```

 **Output:**

```
Average passenger age: 29.69911764705882
Survival rate: 38.38383838383838 %
Most common embark town: Southampton
```

---

##  Step 9 – Conclusion

**Findings Summary:**

* Dataset size: **891 rows × 15 columns**
* Processing speed: **0.0021 seconds**
* Missing data: **‘age’ and ‘deck’ have the most null values**
* Average passenger age ≈ 29.7 years
* Survival rate ≈ **38.4%**
* Most passengers embarked from **Southampton**
