

## 🧠 PySpark Window Functions Example (Employee Sales)

### **Step 1: Setup PySpark**

```python
from pyspark.sql import SparkSession
from pyspark.sql.functions import (
    col, rank, dense_rank, row_number, ntile,
    percent_rank, cume_dist, sum, avg, max, min,
    first, last, nth_value
)
from pyspark.sql.window import Window
```

---

### **Step 2: Create SparkSession**

```python
spark = SparkSession.builder.appName("EmployeeWindowFunctions").getOrCreate()
```

---

### **Step 3: Create Sample Data**

```python
from pyspark.sql import Row

departments = spark.createDataFrame([
    Row(dept_id=10, dept_name="Sales"),
    Row(dept_id=20, dept_name="Engineering"),
    Row(dept_id=30, dept_name="HR")
])

employees = spark.createDataFrame([
    Row(emp_id=1, emp_name="John", dept_id=10),
    Row(emp_id=2, emp_name="Sara", dept_id=10),
    Row(emp_id=3, emp_name="Mike", dept_id=20),
    Row(emp_id=4, emp_name="Lily", dept_id=20),
    Row(emp_id=5, emp_name="Tom", dept_id=30),
])

sales = spark.createDataFrame([
    Row(sale_id=1, emp_id=1, sale_amount=5000, sale_date="2024-01-01"),
    Row(sale_id=2, emp_id=1, sale_amount=7000, sale_date="2024-01-05"),
    Row(sale_id=3, emp_id=2, sale_amount=4000, sale_date="2024-01-03"),
    Row(sale_id=4, emp_id=2, sale_amount=9000, sale_date="2024-01-10"),
    Row(sale_id=5, emp_id=3, sale_amount=12000, sale_date="2024-01-02"),
    Row(sale_id=6, emp_id=4, sale_amount=11000, sale_date="2024-01-08"),
    Row(sale_id=7, emp_id=5, sale_amount=3000, sale_date="2024-01-04"),
])
```

---

### **Step 4: Define Window Specification**

```python
window_spec = Window.partitionBy("emp_id").orderBy("sale_date")
```

---

### **Step 5: Apply Window Functions**

```python
sales_windowed = sales.withColumn("rank", rank().over(window_spec)) \
    .withColumn("dense_rank", dense_rank().over(window_spec)) \
    .withColumn("row_number", row_number().over(window_spec)) \
    .withColumn("cumulative_sales", sum("sale_amount").over(window_spec.rowsBetween(Window.unboundedPreceding, Window.currentRow))) \
    .withColumn("percent_rank", percent_rank().over(window_spec)) \
    .withColumn("cume_dist", cume_dist().over(window_spec)) \
    .withColumn("ntile_3", ntile(3).over(window_spec)) \
    .withColumn("first_sale", first("sale_amount").over(window_spec)) \
    .withColumn("last_sale", last("sale_amount").over(window_spec)) \
    .withColumn("second_sale", nth_value("sale_amount", 2).over(window_spec))
```

---

### **Step 6: Join with Employees and Departments**

```python
final_df = sales_windowed.join(employees, "emp_id").join(departments, "dept_id")

final_df.select(
    "dept_name", "emp_name", "sale_id", "sale_amount", "sale_date",
    "rank", "percent_rank", "cume_dist", "first_sale", "last_sale", "second_sale"
).show()
```

---

### **Explanation of New Functions**

| Function            | Description                                                 |
| ------------------- | ----------------------------------------------------------- |
| `first()`           | First value in the window (e.g., first sale).               |
| `last()`            | Last value in the window (e.g., latest sale).               |
| `nth_value(col, n)` | Returns the *nth* value within the window (e.g., 2nd sale). |

---

### **Expected Output (Simplified)**

| dept_name | emp_name | sale_id | sale_amount | rank | percent_rank | cume_dist | first_sale | last_sale | second_sale |
| --------- | -------- | ------- | ----------- | ---- | ------------ | --------- | ---------- | --------- | ----------- |
| Sales     | John     | 1       | 5000        | 1    | 0.0          | 0.5       | 5000       | 5000      | null        |
| Sales     | John     | 2       | 7000        | 2    | 1.0          | 1.0       | 5000       | 7000      | 7000        |
| Sales     | Sara     | 3       | 4000        | 1    | 0.0          | 0.5       | 4000       | 4000      | null        |
| Sales     | Sara     | 4       | 9000        | 2    | 1.0          | 1.0       | 4000       | 9000      | 9000        |

