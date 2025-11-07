

## 1️⃣ Introduction

In modern data science and machine learning workflows, datasets are often downloaded, preprocessed, and analyzed using various tools and libraries.
This exercise demonstrates how to:

* Load a dataset using **Hugging Face Datasets**
* Handle data using **Pandas**
* Process and visualize it using **PySpark**

The dataset used here is the **Iris Dataset**, one of the most famous datasets in machine learning.

---

## 2️⃣ What is the Iris Dataset?

The **Iris Dataset** contains information about **150 flowers** from three species:

* *Iris-setosa*
* *Iris-versicolor*
* *Iris-virginica*

Each flower sample has **four features**:

1. Sepal Length (cm)
2. Sepal Width (cm)
3. Petal Length (cm)
4. Petal Width (cm)

The goal is often to classify a flower’s species based on these four features.

---

## 3️⃣ What is Hugging Face?

**Hugging Face** is an open-source platform that provides:

* Datasets for machine learning and NLP
* Pre-trained models (Transformers)
* APIs for model sharing and experimentation

In this task, we used **`load_dataset()`** from `datasets` library to fetch the Iris dataset directly from Hugging Face’s repository.

### 📘 Function used:

```python
from datasets import load_dataset
iris_dataset = load_dataset("scikit-learn/iris")
```

**Explanation:**

* The dataset `"scikit-learn/iris"` comes from the `scikit-learn` dataset collection.
* It automatically downloads and loads the data in a dictionary-like structure called a **DatasetDict** with one key `'train'`.

---

## 4️⃣ What is Pandas?

**Pandas** is a Python library used for data manipulation and analysis.
It provides a powerful data structure called **DataFrame**, which represents data in tabular form (rows and columns).

### ✅ Key Advantages:

* Easy data filtering, grouping, and aggregation
* Simple syntax for cleaning and transforming data
* Integration with visualization libraries (like Matplotlib or Seaborn)

### 📘 Conversion to Pandas:

```python
iris_df = iris_dataset['train'].to_pandas()
```

This converts the Hugging Face dataset to a **Pandas DataFrame** so we can view and manipulate it easily.

### 📘 Displaying data:

```python
iris_df.head()
```

This shows the first 5 rows of the dataset.

---

## 5️⃣ What is PySpark?

**PySpark** is the **Python API for Apache Spark**, a powerful distributed computing engine used for processing large-scale data.

### ✅ Why use PySpark?

* Handles **big data** efficiently across multiple machines.
* Performs operations like filtering, grouping, and aggregation **in parallel**.
* Integrates easily with Hadoop and cloud platforms.

### 📘 Starting Spark Session:

```python
from pyspark.sql import SparkSession
spark = SparkSession.builder.appName("IrisDataset").getOrCreate()
```

This initializes a Spark application named “IrisDataset”.

---

## 6️⃣ Creating a Spark DataFrame

Spark also uses **DataFrames**, similar to Pandas, but optimized for distributed processing.

### 📘 Conversion:

```python
spark_df = spark.createDataFrame(iris_df)
```

### 📘 Display data:

```python
spark_df.show(5)
```

**Output:**
Displays the top 5 rows of the dataset in a formatted table using Spark.

---

## 7️⃣ Comparison between Pandas and PySpark

| Feature       | Pandas                            | PySpark                                     |
| ------------- | --------------------------------- | ------------------------------------------- |
| **Scale**     | Works best with small/medium data | Designed for large-scale distributed data   |
| **Execution** | Runs on a single machine          | Runs on multiple nodes (distributed)        |
| **Speed**     | Slower for big datasets           | Highly optimized for parallel processing    |
| **Syntax**    | Simple and user-friendly          | Similar syntax but requires Spark setup     |
| **Use Case**  | Ideal for local data analysis     | Ideal for big data and production pipelines |

---

## 8️⃣ Steps Recap

| Step | Description                             | Tool         |
| ---- | --------------------------------------- | ------------ |
| 1    | Install Java, Hugging Face, and PySpark | OS + pip     |
| 2    | Load dataset from Hugging Face          | Hugging Face |
| 3    | Convert to DataFrame and view           | Pandas       |
| 4    | Initialize Spark                        | PySpark      |
| 5    | Convert and display in Spark            | PySpark      |

---

## 9️⃣ Output Summary

**Sample Output (Pandas & Spark):**

| Id | SepalLengthCm | SepalWidthCm | PetalLengthCm | PetalWidthCm | Species     |
| -- | ------------- | ------------ | ------------- | ------------ | ----------- |
| 1  | 5.1           | 3.5          | 1.4           | 0.2          | Iris-setosa |
| 2  | 4.9           | 3.0          | 1.4           | 0.2          | Iris-setosa |
| 3  | 4.7           | 3.2          | 1.3           | 0.2          | Iris-setosa |
| 4  | 4.6           | 3.1          | 1.5           | 0.2          | Iris-setosa |
| 5  | 5.0           | 3.6          | 1.4           | 0.2          | Iris-setosa |

---

