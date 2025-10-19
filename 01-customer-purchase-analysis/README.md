
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
## ⚠️Reveal Zone: Answers Below

🚫 Spoiler Warning
You're about to enter the solution section.
These DAX answers are laid out in full — make sure you've given the challenge a solid try before proceeding!

---


1. **Customers with Only One Purchase**  
   > What is the count of customers who made just one purchase?

```dax
1E-SUMMARIZE-Customer only purchased one = 
COUNTROWS (
    FILTER (
        ADDCOLUMNS (
            SUMMARIZE ( Sales, Sales[CustomerKey] ),
            "No of Purchase", CALCULATE ( DISTINCTCOUNT ( Sales[SalesOrderNumber] ) )
        ),
        [No of Purchase] = 1
    )
)


```
2. **Churned Customers**  
   > How many customers did not return in the current year?
   
```dax
 
2E SUMMARIZE-Lost Customer(This year) 2 = 
COUNTROWS(
    FILTER(
        ADDCOLUMNS(
            SUMMARIZE(Sales, Sales[CustomerKey]),
            "Max Order Date",
            FIRSTNONBLANKVALUE(
                Sales[CustomerKey],
                MAX(Sales[OrderDate])
            )
        ),
        [Max Order Date] < DATE(2022, 1, 1)
    )
)
```


3. **New Customers in the Current Year**  
   > How many customers made their **first-ever** purchase in the current year?

```dax
3E SUMMARIZE-New customer in 2022 = 
COUNTROWS (
    FILTER (
        ADDCOLUMNS(
            SUMMARIZE(Sales, Sales[CustomerKey]),
            "First Purchase Date", 
            CALCULATE(MIN ( Sales[OrderDate] ))
        ),
        [First Purchase Date] >= DATE ( 2022, 1, 1 )
    )
)


```
4. **Repeat Customers (Year-over-Year)**  
   > What is the number of customers who made purchases in **both** the current year and the previous year?


```dax

4E SUMMARIZE-Repeat Customer 2 = 
COUNTROWS (
    FILTER (
        ADDCOLUMNS(
            SUMMARIZE(Sales, Sales[CustomerKey]),
            "First Purchase", 
            CALCULATE(MIN ( Sales[OrderDate] )),
            "Last Purchase", 
            CALCULATE(MAX ( Sales[OrderDate] ))
        ),
        [First Purchase] < DATE ( 2022, 1, 1 )
        && [Last Purchase] >= DATE ( 2022, 1, 1 )
    )
)

```
5. **Average Products per Sale**  
   > What is the average number of products purchased per transaction?


```dax
5E SUMMARIZE-Average Product Per Sale 2 = 
AVERAGEX (
    ADDCOLUMNS(
        SUMMARIZE(Sales, Sales[SalesOrderNumber]),
        "No Of Product", 
        CALCULATE(DISTINCTCOUNT(Sales[ProductKey]))
    ),
    [No Of Product]
)


```
#### Let's Connect
[![github](https://img.shields.io/badge/github-181717?style=for-the-badge&logo=github&logoColor=white)](https://github.com/ahammedjaleel)
[![linkedin](https://img.shields.io/badge/linkedin-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/ahammed-jaleel-33772b5b/)









