# 09 - Top N Product Sales Analysis 

This project demonstrates how to identify the **Top 1** and **Top 10** best-selling products using DAX in Power BI. The approach includes solutions using both **calculated columns** and **measures**, with step-by-step DAX explanations.

The goal is to understand how to use `TOPN`, `SUMMARIZE`, and `CONCATENATEX` to dynamically extract and display top-performing products based on total sales.

---

## 📁 Dataset Tables Used

| Table     | Description                              |
|-----------|------------------------------------------|
| `Sales`   | Transaction data containing sales details |
| `Products`| Product information (e.g., names)         |
| `Dates`   | Calendar table for time intelligence      |

---

## 🔗 Relationships

- `Sales[ProductID]` → `Products[ProductID]`
- `Sales[OrderDate]` → `Dates[Date]`

---

##  What Are We Solving?

This analysis focuses on **Top N product identification**, using two DAX problem statements:

1. Find the **Top 1 product** based on total sales.
2. Find the **Top 10 products** and display them in a single visual, separated by line breaks.

Each is solved using:
- A **basic calculated Table/measure**, and
- A **detailed explanation version** of the same logic

---

##  Output Screenshots


> 
<img width="800" height="707" alt="image" src="https://github.com/user-attachments/assets/98fdb0fd-917a-4a17-a09b-106cc4d2b755" />



---

##  Real-World Use Case

This kind of **Top N Product analysis** is commonly used in:
- Executive sales dashboards
- Product performance summaries
- Inventory planning reports
- Monthly or quarterly business reviews

---

## 🧩 Problem Statements

> Try solving the following on your own in Power BI using DAX before viewing the solution at the bottom.

---

### 🔹 Problem 22: Identify the Top 1 Best-Selling Product

**Objective:**  
Create a **calculated table** and a **DAX measure** that return the **top-selling product** based on total sales.

- The **calculated table** should extract the product with the highest total sales.
- The **measure** should display the product name in visuals.
- If multiple products share the highest sales value, the measure should return `"Multiple Products"` to indicate a tie.

---

### 🔹 Problem 23: List the Top 10 Best-Selling Products

**Objective:**  
Create a **calculated table** and a **DAX measure** to retrieve the **Top 10 products** based on total sales.

- The **calculated table** should return the top 10 products sorted by sales (descending).
- The **measure** should concatenate and display all 10 product names, each on a new line.
- Use this measure in a card or table visual to present the results clearly.

---

## 📁 Files Included

| File Name | Description |
|-----------|-------------|
| `09 - Top N Product Sales Analysis -22-23 Question_ANSWER_Explanation_.pbix` | Power BI file containing problems, basic DAX answers, and explanation-enhanced answers. Designed to let users attempt the solution before reviewing the answer. |
| `README.md` | This documentation |

---

## ⚠️ Spoiler Alert: DAX Solutions Below

> The following section includes the full solutions.  
> If you're trying to learn, attempt solving the problems on your own first!

---

## ✅ Solutions

---

###  Solution 22A: Top 1 Product (Calculated table)

```dax
Answer 22_Top Product = 
TOPN (
    1,
    SUMMARIZE (
        'Product',
        'Product'[ProductName]
    ),
    [Total Sale]
)
```
### Solution 22B: Top 1 Product using Measure
```dax
Answer22_Explanation_Top Selling Product = 
CALCULATE (
    SELECTEDVALUE ( 'Product'[ProductName], "Multiple Products" ),  // Return top product name or "Multiple Products"
    TOPN (
        1,  // Get only the top 1 product
        SUMMARIZE (
            'Product',
            'Product'[ProductName]  // Group by product
        ),
        [Total Sale]  // Sort by total sales
    )
)
```
### Solution 23A: Top 10 Products (Calculated Table)
```dax

Answer 23_Top Product = 
TOPN (
    10,
    VALUES ( 'Product'[ProductName] ),
    [Total Sale],
    DESC
)




```


### Solution 23B: Top 10 Products( Measure)


```dax


Answer23_Explanation_Top10-selling products = 
CONCATENATEX (
    TOPN (
        10,  // Get top 10 products
        SUMMARIZE (
            'Product',
            'Product'[ProductName]
        ),
        [Total Sale]
    ),
    'Product'[ProductName],  // Values to concatenate
    UNICHAR(10),  // Use line break between products
    'Product'[ProductName], ASC  // Sort alphabetically
)


```



#### Let's Connect
[![github](https://img.shields.io/badge/github-181717?style=for-the-badge&logo=github&logoColor=white)](https://github.com/ahammedjaleel)
[![linkedin](https://img.shields.io/badge/linkedin-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/ahammed-jaleel-33772b5b/)

---
