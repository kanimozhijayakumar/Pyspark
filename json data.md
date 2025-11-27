# JSON Processing, Compression, Table Output & SQL Generation  

This project demonstrates how to work with JSON data in Python by performing the following operations:

✅ Read a JSON file  
✅ Compress the JSON using GZIP  
✅ Read decompressed JSON  
✅ Display JSON data as a formatted table  
✅ Auto-generate a SQL `CREATE TABLE` statement  
✅ Print clear output for analysis  

---

## 📁 Project Files

```
data.json             → Input JSON file  
process_json.py       → Python script  
data.json.gz          → Auto-generated compressed JSON  
README.md             → Project documentation  
```

---

## 🧠 **Project Explanation**

This project showcases essential data engineering and Python skills:

### 1️⃣ Reading JSON  
Python's built-in `json` module is used to load structured data.

### 2️⃣ GZIP Compression  
We compress the JSON file using the `gzip` module to reduce size — used commonly in big-data pipelines.

### 3️⃣ Decompression  
We read back the `.json.gz` file to check correctness.

### 4️⃣ Table Format Output  
Using **pandas**, we convert JSON into a dataframe and print it neatly.

### 5️⃣ SQL Table Generation  
Based on JSON keys and values, we automatically infer SQL column types and generate a database-ready DDL script.

---

## 🐍 **Python Code (process_json.py)**

```python
import json
import gzip
import pandas as pd


# Step 1: Read JSON file
print("Reading JSON file...")
with open("data.json", "r") as f:
    data = json.load(f)

print("\nOriginal JSON Data (first 3 records):")
print(data[:3])


# Step 2: Compress JSON
print("\nCompressing JSON to data.json.gz ...")
with gzip.open("data.json.gz", "wt") as gz:
    json.dump(data, gz)
print("Compression completed!")


# Step 3: Read compressed JSON
print("\nReading compressed JSON file...")
with gzip.open("data.json.gz", "rt") as gz:
    compressed = json.load(gz)
print("\nCompressed File Data (first 3 records):")
print(compressed[:3])


# Step 4: Table Output
print("\nJSON Data in Table Format:\n")
df = pd.DataFrame(compressed)
print(df.to_string(index=False))


# Step 5: CREATE TABLE SQL
print("\nGenerated SQL CREATE TABLE Statement:\n")

sample = compressed[0]
sql_fields = []

for key, value in sample.items():
    if isinstance(value, int):
        dtype = "INT"
    elif isinstance(value, float):
        dtype = "FLOAT"
    elif isinstance(value, bool):
        dtype = "BOOLEAN"
    else:
        dtype = "VARCHAR(255)"
    
    sql_fields.append(f"    {key} {dtype}")

sql_query = "CREATE TABLE employees (\n" + ",\n".join(sql_fields) + "\n);"
print(sql_query)

print("\nProcess Completed Successfully!")
```

---

## 📄 **Sample Output**

```
Reading JSON file...

Original JSON Data (first 3 records):
[{'id': 1, 'name': 'Rita', 'age': 22, 'city': 'Chennai', 'email': 'rita@example.com', 'salary': 50000, 'department': 'IT'},
 {'id': 2, 'name': 'Arun', 'age': 25, 'city': 'Coimbatore', 'email': 'arun@example.com', 'salary': 52000, 'department': 'Finance'},
 {'id': 3, 'name': 'Siva', 'age': 28, 'city': 'Madurai', 'email': 'siva@example.com', 'salary': 48000, 'department': 'HR'}]

Compressing JSON to data.json.gz ...
Compression completed!

Reading compressed JSON file...

Compressed File Data (first 3 records):
[ ...same as above... ]

JSON Data in Table Format:

 id   name  age       city               email  salary department
  1   Rita   22    Chennai    rita@example.com   50000         IT
  2   Arun   25 Coimbatore    arun@example.com   52000    Finance
  3    Siva   28    Madurai    siva@example.com   48000         HR
  ... (full 20 rows)

Generated SQL CREATE TABLE Statement:

CREATE TABLE employees (
    id INT,
    name VARCHAR(255),
    age INT,
    city VARCHAR(255),
    email VARCHAR(255),
    salary INT,
    department VARCHAR(255)
);

Process Completed Successfully!
```

---

## ▶️ **How to Run**

### Install pandas
```bash
pip install pandas
```

### Run the script
```bash
python process_json.py
```

---

## 📌 Technologies Used
- Python  
- JSON  
- gzip  
- pandas  
- SQL  

---

## 📜 License
This project is free to use for learning and academic purposes.

---

# 🎉 Ready for Upload!

You can directly copy this full README.md into your GitHub repository.

If you want, I can also:

✅ Generate a ZIP with README + code + JSON  
✅ Make a better project title  
✅ Add badges for GitHub  
✅ Create a screenshot image for your table  

Just tell me!
