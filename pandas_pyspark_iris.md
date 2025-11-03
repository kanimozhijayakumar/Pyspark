
## 🧩 Step 1: Install Dependencies

```python
!apt-get install openjdk-8-jdk-headless -qq > /dev/null  # Install Java for Spark
!pip install -q datasets pyspark                        # Install Hugging Face datasets and PySpark
````

---

## 🧠 Step 2: Import Libraries

```python
from datasets import load_dataset
import pandas as pd
from pyspark.sql import SparkSession
```

---

## 🌸 Step 3: Load Dataset from Hugging Face

```python
# Load the Iris dataset from Hugging Face
iris_dataset = load_dataset("scikit-learn/iris")  # Returns a DatasetDict with a 'train' split
```

---

## 🐼 Step 4: Convert to Pandas DataFrame

```python
# Convert the dataset to a Pandas DataFrame
iris_df = iris_dataset['train'].to_pandas()

# Display the first few rows
iris_df.head()
```

**Output:**

| Id | SepalLengthCm | SepalWidthCm | PetalLengthCm | PetalWidthCm | Species     |
| -- | ------------- | ------------ | ------------- | ------------ | ----------- |
| 1  | 5.1           | 3.5          | 1.4           | 0.2          | Iris-setosa |
| 2  | 4.9           | 3.0          | 1.4           | 0.2          | Iris-setosa |
| 3  | 4.7           | 3.2          | 1.3           | 0.2          | Iris-setosa |
| 4  | 4.6           | 3.1          | 1.5           | 0.2          | Iris-setosa |
| 5  | 5.0           | 3.6          | 1.4           | 0.2          | Iris-setosa |

---

## 🔥 Step 5: Create Spark Session

```python
# Start Spark
spark = SparkSession.builder.appName("IrisDataset").getOrCreate()
```

---

## ⚡ Step 6: Convert Pandas DataFrame to Spark DataFrame

```python
# Convert to Spark DataFrame
spark_df = spark.createDataFrame(iris_df)

# Show first few rows
spark_df.show(5)
```

**Output:**

```
+---+-------------+------------+-------------+------------+-----------+
| Id|SepalLengthCm|SepalWidthCm|PetalLengthCm|PetalWidthCm|    Species|
+---+-------------+------------+-------------+------------+-----------+
|  1|          5.1|         3.5|          1.4|         0.2|Iris-setosa|
|  2|          4.9|         3.0|          1.4|         0.2|Iris-setosa|
|  3|          4.7|         3.2|          1.3|         0.2|Iris-setosa|
|  4|          4.6|         3.1|          1.5|         0.2|Iris-setosa|
|  5|          5.0|         3.6|          1.4|         0.2|Iris-setosa|
+---+-------------+------------+-------------+------------+-----------+
```

---

## ✅ **Summary**

| Task | Description                             | Status |
| ---- | --------------------------------------- | ------ |
| 1    | Loaded dataset from Hugging Face        | ✅      |
| 2    | Displayed data using Pandas             | ✅      |
| 3    | Loaded same data into PySpark DataFrame | ✅      |

---

