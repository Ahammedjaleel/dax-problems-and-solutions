#  Power BI DAX: High-Demand Products Over the Last 3 Weeks

This case study shows how to identify **high-demand products** that were ordered consistently over the **last 3 consecutive weeks** using DAX.

It's useful for demand forecasting, product lifecycle analysis, and inventory optimization.

---

##  What is a High-Demand Product?

A **High-Demand Product** is defined here as a product that was **ordered in all of the past 3 weeks**, including the current one (based on filter context).

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

## 💡 Problem Statements

>  Try solving the following DAX problems using the dataset before viewing the solutions.

---

### 🔹 Problem 17: Count of High-Demand Products (Last 3 Weeks)

**Objective:**  
Calculate how many products were sold **consistently in each of the last 3 weeks**.  
A product is considered **high demand** only if it was sold in **all three weeks** without missing any.

---

### 🔹 Problem 18: Product IDs of High-Demand Products (Last 3 Weeks)

**Objective:**  
Return a list of **Product IDs** that were sold **repeatedly in all of the last 3 weeks**.  
These are products with **continuous weekly demand**, indicating consistent popularity.


---

## 🔍 Heads-Up: Answers Incoming  

> 💡 **Think First!**  
> The following content contains complete DAX solutions.  
> If you haven’t tried solving the problems yourself yet, now’s a great time to pause and give it a go.


---
#### 📁 Power BI File

The Power BI file 06-HighDemandProducts-17-18.pbix includes:

✅ Final answers, Step-by-step logic,Visuals to validate output

---

## ✅ Solution 17: High-Demand Product Count

```dax
High Demand Product Count = 

VAR week1 = 
    VALUES(Orders[ProductID])

VAR week2 = 
    CALCULATETABLE(
        VALUES(Orders[ProductID]),
        DATESBETWEEN(
            'Calendar'[Date],
            MIN('Calendar'[Date]) - 7,
            MAX('Calendar'[Date]) - 7
        )
    )

VAR twoweeks =
    INTERSECT(week1, week2)

VAR week3 = 
    CALCULATETABLE(
        VALUES(Orders[ProductID]),
        DATESBETWEEN(
            'Calendar'[Date],
            MIN('Calendar'[Date]) - 14,
            MAX('Calendar'[Date]) - 14
        )
    )

VAR threeweeks =
    INTERSECT(twoweeks, week3)

RETURN
    IF(
        ISFILTERED('Calendar'[Week No]),
        COUNTROWS(threeweeks)
    )
```
#### Explanation:

Captures ProductIDs from the current week, previous week, and two weeks ago.

Uses INTERSECT to find common products across all 3 weeks.

Returns the count of such consistently ordered products.


## ✅ Solution 18: High-Demand Product IDs
```dax

High Demand Product ID = 

VAR CurrWeek = 
    VALUES(Orders[ProductID])

VAR PrevWeek = 
    CALCULATETABLE(
        VALUES(Orders[ProductID]),
        DATESBETWEEN(
            'Calendar'[Date],
            MIN('Calendar'[Date]) - 7,
            MAX('Calendar'[Date]) - 7
        )
    )

VAR Prev2Week = 
    CALCULATETABLE(
        VALUES(Orders[ProductID]),
        DATESBETWEEN(
            'Calendar'[Date],
            MIN('Calendar'[Date]) - 14,
            MAX('Calendar'[Date]) - 14
        )
    )

RETURN
    IF(
        ISFILTERED('Calendar'[Week No]),
        CONCATENATEX(
            INTERSECT(
                INTERSECT(CurrWeek, PrevWeek),
                Prev2Week
            ),
            Orders[ProductID],
            " , ",
            Orders[ProductID],
            DESC
        )
    )
```
#### Explanation:

Collects product IDs ordered in each of the last 3 weeks.

Uses nested INTERSECT to find products ordered in all three weeks.

CONCATENATEX returns a comma-separated list of those ProductIDs.

---
#### Let's Connect
[![github](https://img.shields.io/badge/github-181717?style=for-the-badge&logo=github&logoColor=white)](https://github.com/ahammedjaleel)
[![linkedin](https://img.shields.io/badge/linkedin-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/ahammed-jaleel-33772b5b/)
---
