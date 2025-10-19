# Power BI DAX: Running Total by Non-Date Fields

This repository contains practical DAX examples for calculating **running totals based on non-date fields**, such as **Customer Name** or **Category ID**.

These scenarios are useful when you want to calculate cumulative values in cases **where dates aren't involved** — instead, we rely on ranking, text fields, or category-based ordering.

---

##  What is a Running Total?

A **running total** (also called a **cumulative total**) adds up values **sequentially based on a defined order**.

---

### ❓ Is a Running Total Always Based on Dates?

**No.**  
A running total needs a consistent **order**, but **not necessarily a date**.

---

---

##  Problem Statements

> 💡 Try solving the following DAX problems on your own using the dataset before viewing the solutions below.

---

### 🔹 Problem 1: Running Total by Customer

**Objective**:  
Create a measure that calculates the **running total of sales by customer**, ranked by total sales (highest to lowest).  
This will help visualize how top customers contribute cumulatively to total revenue.

---

### 🔹 Problem 2: Running Total by Category

**Objective**:  
Create a DAX measure that calculates the **running total of sales by product category**, using `CategoryID` as the sort key.  
This running total is based on the numeric or business-defined order of the category, not dates.

---

##  Output Screenshots

You can find visual results of the solutions below:

<img width="600" height="500" alt="image" src="https://github.com/user-attachments/assets/da688228-a543-49ae-9779-ed229aa5cd0e" />


Use these to verify your own implementation.

---

##  Power BI File

The Power BI file `04-Running Total-13-14 Question_ANSWER_Explanation_.pbix` includes:

- ✅ **Solution**: Contains two versions for each problem:
  - One with just the **final DAX answer**.
  - Another with **step-by-step explanation** .

---

## 🚨 Warning: Solutions Ahead

> ⚠️ **Spoiler Alert**  
> The following section contains the full DAX solutions.  
> Only continue if you've already attempted to solve the problems yourself.  

---



### ✅ Solution 1: Running Total by Customer (Ranked by Total Sales)

```dax
Customer Running Total = 
VAR Custrank =
    RANKX ( ALL ( Customers ), [TotalSales], , DESC )
VAR RTCustomer =
    CALCULATE (
        [TotalSales],
        FILTER (
            ALL ( Customers ),
            Custrank >= RANKX ( ALL ( Customers ), [TotalSales], , DESC )
        )
    )
RETURN
    RTCustomer
```

RANKX(...) assigns a descending rank based on total sales.

CALCULATE + FILTER accumulates total sales from all customers with a rank equal to or better than the current one.

### ✅ Solution 2: Running Total by Category (Using CategoryID)
```dax
RunningTotal by Category = 
VAR CatID =
    SELECTEDVALUE ( Products[CategoryID] )
RETURN
    CALCULATE ( 
        [TotalSales], 
        Products[CategoryID] <= CatID
    )
```
- SELECTEDVALUE pulls the current CategoryID in row context.

- FILTER + CALCULATE adds up sales from all categories with IDs less than or equal to the current one.
