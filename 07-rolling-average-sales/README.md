# 07- Rolling Average Sales Analysis

Calculate rolling average sales over time using DAX in Power BI — including yearly and 6-month rolling windows — to identify sales trends and smooth out seasonal fluctuations.

---

## 📁 Dataset Tables

- `Calendar`
- `Customers`
- `Sales`
- `Products`

---

### 🔗 Relationships

- `Sales[CustomerID]` → `Customers[CustomerID]`  
- `Sales[ProductID]` → `Products[ProductID]`  
- `Sales[OrderDate]` → `Calendar[Date]`

---

##  What is a Rolling Average?

A **rolling average** (also called a **moving average**) is a technique used to smooth out fluctuations in time-series data by calculating the average value over a specific number of past periods (like months or years).

This approach:
- Reduces noise in volatile data
- Highlights long-term trends
- Helps with forecasting and planning

---
##  Output Screenshots
<img width="800" height="500" alt="image" src="https://github.com/user-attachments/assets/de25c704-1ab3-4d95-b3bf-7369a17d3afd" />
<img width="800" height="500" alt="image" src="https://github.com/user-attachments/assets/859fba89-c87d-439a-86ba-e22bd3ed16a4" />


---

## 📁 Data Model Diagram

<img width="700" height="600" alt="image" src="https://github.com/user-attachments/assets/7e37e18c-c53c-4367-9d44-20ab1faa1013" />



---


##  Problem Statements

> Solve these using DAX to better understand rolling window calculations.

---

### 🔹 Problem 19: Rolling Average Sales (Last 12 Months)

**Objective:**  
Calculate the **rolling average of sales over the past 12 months** for any selected date in the report.

This helps in tracking year-long trends while minimizing the effect of seasonal spikes.

---

### 🔹 Problem 20: Rolling Average Sales (Last 6 Months)

**Objective:**  
Calculate the **rolling average of sales over the last 6 months**, dynamically based on the selected date range.

This is useful to monitor recent performance without daily/monthly fluctuations.

---
## 📁 Files Included

| File | Description |
|------|-------------|
| `03-RunningTotal-8-12 Question_ANSWER_Explanation_.pbix` | Power BI file with **fully implemented DAX solutions** for each problem. Use this to validate your approach or learn new techniques. |
| `README.md` | This documentation, including problem descriptions and all DAX solutions. |


## 🚨 Warning: Solutions Ahead

> ⚠️ **Spoiler Alert**  
> The following section includes the full DAX solutions.  
> Try solving the problems on your own first!

---

## ✅ Solution 19: Rolling Average for the Year

```dax
Yearly RollingAverage = 
VAR Periods =
    DATESBETWEEN (
        'Calendar'[Date],
        EOMONTH ( MIN ( 'Calendar'[Date] ), -12 ) + 1,
        MAX ( 'Calendar'[Date] )
    ) 
RETURN
    IF (
        MAX ( Sales[OrderDate] ) <> BLANK (),
        DIVIDE (
            CALCULATE ( [TotalSale], Periods ),
            CALCULATE (
                DISTINCTCOUNT ( 'Calendar'[MonthName] ),
                Periods
            )
        )
    )
```

## ✅ Solution 20: Rolling Average Sales (Last 6 Months)

```dax
Answer20_6Months RA = 
VAR Periods =
    DATESBETWEEN (
        'Calendar'[Date],
        EOMONTH ( MIN ( 'Calendar'[Date] ), -6 ) + 1,
        MAX ( 'Calendar'[Date] )
    )
VAR Runnintotal =
    CALCULATE ( [TotalSale], Periods )
VAR MOnths =
    CALCULATE ( DISTINCTCOUNT ( 'Calendar'[MonthName] ), Periods )
RETURN
    IF ( [TotalSale] <> BLANK (), DIVIDE ( Runnintotal, MOnths ) )

```
---
#### Let's Connect
[![github](https://img.shields.io/badge/github-181717?style=for-the-badge&logo=github&logoColor=white)](https://github.com/ahammedjaleel)
[![linkedin](https://img.shields.io/badge/linkedin-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/ahammed-jaleel-33772b5b/)



