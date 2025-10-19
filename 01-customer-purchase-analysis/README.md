
# DAX Problem & Solution –01- Customer Purchase Analysis

This repository contains a Power BI case study focused on solving key customer analytics problems using DAX functions such as `ADDCOLUMNS`, `SUMMARIZE`, and `SUMMARIZECOLUMNS`.




---

##  Dataset Overview

The dataset consists of the following tables:

- `Customer`  
- `Product`  
- `Region`  
- `Sales`  

These tables are related appropriately in the Power BI data model to perform sales and customer analysis.

---
## Power BI Data Model Diagram
<img width="600" height="500" alt="image" src="https://github.com/user-attachments/assets/42c34238-a33a-4263-b420-246adbd50b2d" />


This visual represents the Power BI data model used in this case study. It illustrates the relationships between the key tables: Customer, Product, Region, and Sales.

➡️ The Sales table serves as the central fact table, containing transaction-level data.

➡️ It connects to the Customer, Product, and Region tables via one-to-many relationships, enabling efficient filtering and aggregation.

➡️ This star schema design supports optimal DAX performance and simplifies complex analytical calculations.

➡️ The well-structured data model ensures accurate and efficient customer purchase analysis using DAX measures and calculated tables.

---
##  DAX Problems to Solve

Using **`ADDCOLUMNS`** and **`SUMMARIZE`**, solve the following:

## ❓01 - Customer Purchase Analysis

This section focuses on analyzing customer purchasing behavior using DAX in Power BI. Below are the key sub-questions explored in this analysis:

1. **Customers with Only One Purchase**  
   > What is the count of customers who made just one purchase?

2. **Churned Customers**  
   > How many customers did not return in the current year?

3. **New Customers in the Current Year**  
   > How many customers made their **first-ever** purchase in the current year?

4. **Repeat Customers (Year-over-Year)**  
   > What is the number of customers who made purchases in **both** the current year and the previous year?

5. **Average Products per Sale**  
   > What is the average number of products purchased per transaction?

6. **Re-solve All of the Above Using `SUMMARIZECOLUMNS`**  
   > Re-implement the above calculations using the `SUMMARIZECOLUMNS` function  
   > (instead of `SUMMARIZE` or `ADDCOLUMNS`) to improve performance or clarity.




---



## 📁 Files Included

01-1-6 Question_ANSWER_Explanation_.pbix – This Power BI file contains six DAX-based business questions along with their solutions and explanations. 

- ✅ **Solution**: Contains two versions for each problem:
  - One with just the **final DAX answer**.
  - Another with **step-by-step explanation** .


---


## ✅ Requirements

- Power BI Desktop (latest version recommended)

---

## 📸 Sample Output

<img width="800" height="450" alt="image" src="https://github.com/user-attachments/assets/83dd82b3-a9f3-4c33-9467-8ee5dd2a8f24" />


---
