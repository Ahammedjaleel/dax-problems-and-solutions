# 📊 Power BI DAX Running Totals — Practice Problems & Solutions

This repository provides a hands-on learning experience to master **DAX running total calculations** in Power BI. It includes **interview-style DAX challenges** and their solutions using different DAX functions and logic.

Ideal for Power BI learners, data analysts, or interview candidates who want to understand and implement **Running Totals** in multiple ways.

---

## 📁 Files Included

| File | Description |
|------|-------------|
| `Running_Total_Solutions.pbix` | Power BI file with **fully implemented DAX solutions** for each problem. Use this to validate your approach or learn new techniques. |
| `README.md` | This documentation, including problem descriptions and all DAX solutions. |

---

## 🎯 DAX Running Total Problems

Below are the challenges you'll be solving. All problems are based on a calendar table and a basic measure `[Total Sales]`.

### 📌 Problem 8: Running Total using `MAX`  
Calculate a cumulative total of sales up to the current date using the `MAX` function for context transition.

---

### 📌 Problem 9: Running Total using `ISONORAFTER`  
Create a running total using the `ISONORAFTER` function to define the date comparison logic within a filter.

---

### 📌 Problem 10: Running Total for Last 3 Months  
Compute a moving total that only includes the last **3 complete months** from the current row context.

---

### 📌 Problem 11: Year-to-Date Running Total using `MAX`  
Use `MAX` to calculate a running total **within the same year only** (yearly cumulative total).

---

### 📌 Problem 12: Year-to-Date (YTD) using `TOTALYTD`  
Use the built-in `TOTALYTD` function to calculate the cumulative total from the beginning of the year to the current date.

---
## 📷 Output Screenshots

<img width="800" height="450" alt="image" src="https://github.com/user-attachments/assets/77eda32f-e875-43f8-a335-1b0181226e8c" />

<img width="800" height="450" alt="image" src="https://github.com/user-attachments/assets/16ae7d95-1a5c-4224-9f79-a0f6d187f19c" />

---

## 🧠 Key Learning Points

- Use of different DAX functions (`MAX`, `ISONORAFTER`, `DATESBETWEEN`, `TOTALYTD`) to compute running totals  
- Understanding context transition in `CALCULATE` and `FILTER`  
- Working with custom date intervals and yearly constraints  
- Use of time intelligence functions in real-world scenarios  

---

## 🛠 Requirements

- Power BI Desktop (recommended: latest version)  
- A date/calendar table with `Date`, `Month`, and `Year` columns  
- A measure named `[Total Sales]` for aggregation  

---

## 🚀 How to Use

1. **Download or clone** this repository.  
2. Open `Running_Total_Problems.pbix` and try solving the problems yourself.  
3. Open `Running_Total_Solutions.pbix` to check and study the official solutions.  
4. Refer to this `README.md` for all DAX code and explanations.  
5. Explore the `screenshots/` folder to see expected outputs for each solution.  

## ✅ DAX Solutions

Here are the complete DAX solutions for each of the above problems.

### 🔹 Solution 8: Running Total using `MAX`
```DAX
Answer8-ExplanationAnswer-Running Total = 
CALCULATE([Total sales],      // CALCULATE changes the context in which the expression [Total sales] is evaluated
    FILTER(ALL('Calendar'[Date]),  // FILTER function modifies the context for 'Calendar'[Date], removing any filters applied to the Date column
        MAX('Calendar'[Date]) >= 'Calendar'[Date]))  // This condition ensures that the running total is calculated for all dates up to and including the maximum date in the current context.

```
### 🔹 Solution 9: Running Total using ISONORAFTER
```DAX
Answer9_Explanation-RT_ISONORAFTER = 
CALCULATE([Total sales],  // The CALCULATE function is used to evaluate the expression [Total sales] in a modified filter context
    FILTER(ALL('Calendar'[Date]),  // FILTER removes any existing filters on the 'Calendar'[Date] column and returns all date values
    ISONORAFTER(MAX('Calendar'[Date]), 'Calendar'[Date])))  // The ISONORAFTER function checks if the 'Calendar'[Date] is on or after the maximum date in the current context


```
### 🔹 Solution 10: Running Total for Last 3 Months
```DAX
Answer10_Explanation-RT_Last3Months = 
CALCULATE([Total sales],  // The CALCULATE function is used to evaluate the expression [Total sales] in a modified filter context
    DATESBETWEEN('Calendar'[Date],  // The DATESBETWEEN function filters the date column between two date values
        EOMONTH(MAX('Calendar'[Date]), -3),  // EOMONTH(MAX('Calendar'[Date]), -3) calculates the end of the month, 3 months before the maximum date in the current context
        MAX('Calendar'[Date])))  // MAX('Calendar'[Date]) returns the maximum date in the current context (i.e., the latest date)


```
### 🔹 Solution 11: Yearly Running Total using MAX
```DAX
Answer11_Explanation-RT_YAERLY = 
CALCULATE([Total sales],  // The CALCULATE function is used to evaluate the expression [Total sales] in a modified filter context
    FILTER(ALL('Calendar'[Date]),  // The FILTER function removes any existing filters on the 'Calendar'[Date] column and returns all date values
        MAX('Calendar'[Date]) >= 'Calendar'[Date]),  // This condition ensures that only dates up to and including the maximum date in the current context are included in the calculation
        MAX('Calendar'[Year]) = 'Calendar'[Year])  // This condition ensures that only dates from the current year (based on the latest date in the context) are included in the calculation



```
### 🔹 Solution 12: YTD Running Total using TOTALYTD
```DAX
Answer12_Explanation-RT_YTD = TOTALYTD([Total sales], 'Calendar'[Date])  // This  calculates the Year-To-Date (YTD) total sales.

```

