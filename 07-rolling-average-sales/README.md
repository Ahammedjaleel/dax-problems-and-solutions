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
## 📊 Output Screenshots

---

## 📁 Data Model Diagram




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

