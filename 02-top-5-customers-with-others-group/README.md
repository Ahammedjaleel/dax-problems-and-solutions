# 🧩 Problem 02 – Top 5 Customers with "Others" Group

## 📝 Objective

Identify the **Top 5 Customers by Total Sales** and group **all remaining customers** into a single row labeled **"Remaining Customers"**.

The output should show **6 rows** in total:

- Top 5 customers (individually listed)
- 6th row = All other customers combined, shown as `"Remaining Customers"`

---

## 🎯 Requirements

- Use the **Sales** and **Customer** tables to calculate **Total Sales** per customer.
- Sort the customers in **descending order of sales**.
- Display only the **Top 5 customers** individually.
- Combine all **other customers** into one group and display as `"Remaining Customers"`.

---

## 🧠 DAX Challenge

Implement this logic using **three different DAX methods**:

### 🔹 Method 1: Using `RANKX` and `SWITCH`
- Rank customers by sales
- Use `SWITCH(TRUE(), ...)` to assign names or group into "Remaining Customers"

### 🔹 Method 2: Using `TOPN` and `UNION`
- Create two separate tables:
  - Top 5 customers
  - Group of remaining customers (aggregated)
- Combine them using `UNION`

### 🔹 Method 3: Using Calculated Table or Virtual Table Logic
- Use `ADDCOLUMNS` or `SUMMARIZE` with custom logic to build a virtual table that includes the "Remaining Customers" row.

---

## 🧩 Expected Output (Example)

| Customer Name       | Total Sales |
|---------------------|-------------|
| Customer A          | 120,000     |
| Customer B          | 110,000     |
| Customer C          | 105,000     |
| Customer D          | 102,000     |
| Customer E          | 100,000     |
| **Remaining Customers** | **300,000**   |

---

## 📁 Dataset Tables

- `Customer`
- `Sales`

Ensure relationships are correctly set between `Customer[CustomerID]` and `Sales[CustomerID]`.

---

## 💡 Goal

This is a common real-world DAX use case for dashboards where stakeholders want to:

- Highlight the top performers
- Combine the "long tail" customers under a single row
- Keep visuals clean and informative

---

