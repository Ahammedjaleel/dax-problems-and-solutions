# Power BI DAX: Identifying Regular Customers Over Last 3 Months

This section focuses on solving business questions related to **customer consistency** — identifying customers who have made purchases in each of the **last 3 consecutive months**.

---

## ❓ What is a Regular Customer?

A **Regular Customer** in this context is defined as a customer who has made **at least one purchase in each of the last 3 months** (including the current month in filter context).

---

## 📁 Dataset Tables

- `Calendar`  
- `Customers`  
- `Orders`  
- `Products`  

### 🔗 Relationships

- `Orders[CustomerID]` → `Customers[CustomerID]`  
- `Orders[ProductID]` → `Products[ProductID]`  
- `Orders[OrderDate]` → `Calendar[Date]`  

---

## Data Model Diagram

<img width="590" height="472" alt="image" src="https://github.com/user-attachments/assets/a8bf746f-40b2-4d31-8935-8c3f7a5046a9" />


This visual represents the **data model** used for these problems.  
The **Orders** table is the fact table, joined with dimensions: **Calendar**, **Customers**, and **Products**.  

---

## 💡 Problem Statements

> 🧠 Try solving the following DAX problems using the dataset before viewing the solutions.

---

### 🔹 Problem 15: Count of Regular Customers (Last 3 Months)

**Objective:**  
Create a measure that returns the **count of customers** who made purchases in each of the **last 3 months**.

---

### 🔹 Problem 16: ID and Name of Regular Customers (Last 3 Months)

**Objective:**  
Create a DAX measure that lists the **names and IDs** of customers who made purchases in **each of the last 3 months**.

---
## 📷 Output Screenshots
<img width="813" height="337" alt="image" src="https://github.com/user-attachments/assets/8b57c330-44c3-4477-b83a-d0be39cae388" />


---
## 🚨 Warning: Solutions Ahead

> ⚠️ **Spoiler Alert**  
> The following section includes the full DAX solutions.  
> Only continue if you've already attempted the problems.

---

## ✅ Solution 15: Regular Customer Count (Last 3 Months)

```dax
Regular Customer Count = 
VAR Month1 =
    CALCULATETABLE ( VALUES ( Orders[CustomerID] ) )

VAR Month2 =
    CALCULATETABLE (
        VALUES ( Orders[CustomerID] ),
        DATEADD ( 'Calendar'[Date], -1, MONTH )
    )

VAR Month1_2 =
    INTERSECT ( Month1, Month2 )

VAR Month3 =
    CALCULATETABLE (
        VALUES ( Orders[CustomerID] ),
        DATEADD ( 'Calendar'[Date], -2, MONTH )
    )

RETURN
    COUNTROWS ( INTERSECT ( Month1_2, Month3 ) )

```
Explanation:

Month1: Customer IDs for current month

Month2: Customer IDs for last month

Month3: Customer IDs for two months ago

Final result: Count of customers present in all 3 months

## ✅ Solution 16: Regular Customer Names and IDs (Last 3 Months)


```dax
Answer16_explanation_Regular CustomerName = 
VAR Month1 =
    CALCULATETABLE ( VALUES ( Orders[Customer name] ) )
    -- Creates a table of unique 'Customer name' values from the 'Orders' table for the current month (based on the filter context)

VAR Month2 =
    CALCULATETABLE (
        VALUES ( Orders[Customer name] ),
        DATEADD ( 'Calendar'[Date], -1, MONTH )
    )
    -- Creates a table of unique 'Customer name' values for the previous month (1 month before the current context)
    -- 'DATEADD' shifts the date by -1 month (relative to the current date in the 'Calendar' table)

VAR Month1_2 =
    INTERSECT ( Month1, Month2 )
    -- Finds the intersection (common customers) between the current month ('Month1') and the previous month ('Month2')
    -- The result is a table of 'Customer name's who have placed orders in both the current and the previous month

VAR Month3 =
    CALCULATETABLE (
        VALUES ( Orders[Customer name] ),
        DATEADD ( 'Calendar'[Date], -2, MONTH )
    )
    -- Creates a table of unique 'Customer name' values for the month before the previous month (i.e., two months ago)

RETURN
    CONCATENATEX ( INTERSECT ( Month1_2, Month3 ), Orders[Customer name], ", " )
    -- Finds the intersection (common customers) between the set of customers who ordered in both the current and previous month ('Month1_2') 
    -- and the customers who ordered two months ago ('Month3')
    -- The final result is a concatenated string of 'Customer name's who have placed orders in all three months (current, previous, and two months ago), 
    -- separated by commas

```
## 📁 Power BI File

The Power BI file 05- 15-16 Question_ANSWER_Explanation_.pbix includes:

✅ Both final solutions,Step-by-step logic, Output visuals

#### Let's Connect
[![github](https://img.shields.io/badge/github-181717?style=for-the-badge&logo=github&logoColor=white)](https://github.com/ahammedjaleel)
[![linkedin](https://img.shields.io/badge/linkedin-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/ahammed-jaleel-33772b5b/)

