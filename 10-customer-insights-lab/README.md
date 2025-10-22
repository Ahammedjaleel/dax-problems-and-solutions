# Customer-Product Insight

This repository contains a Power BI file (`DAX_Challenge_Solutions.pbix`) designed to help you **practice real-world DAX problems** and improve your analytical thinking in Power BI.

The file includes:

- **6 thoughtfully designed DAX problems** based on common business scenarios
- **Two solutions per problem**:
  - One with **clean final DAX code**
  - Another with **detailed, step-by-step explanations**
- **Sample output visuals** for verification and comparison
- **Clean question prompts** for practicing without peeking at answers

---
## ✨ Key Learnings

Use of VAR to improve readability and performance

Application of context transitions (e.g., CALCULATE, FILTER)

Aggregation techniques: SUM, AVERAGEX, DISTINCTCOUNT

Time intelligence: SAMEPERIODLASTYEAR

Logical grouping with SWITCH(TRUE())

Dynamic percentage contribution calculations

##  Problem Descriptions

> The dataset contains the following tables:  
> `Sales`, `Dates`, `Customer`, `Country`, `Product`, `Product Subcategory`, `Product Category`.

##  Data Model
<img width="800" height="672" alt="image" src="https://github.com/user-attachments/assets/95ef7089-0525-46d8-80af-85ea68020f38" />


###  Problem 1: What is the Average Sales per Customer?

We want to understand how much each customer spends on average. This metric helps evaluate customer value and guides marketing and retention strategies.

---

###  Problem 2: How to Calculate Year-over-Year Sales Growth for Each Product Category?

This question aims to analyze sales growth trends over time. Year-over-Year (YoY) growth helps us assess business performance and seasonality for each category.

---

###  Problem 3: What is the Average Number of Days it Takes to Ship Orders per Product Category?

Shipping efficiency is a key performance indicator. This problem calculates the average delivery time for each product category to help spot fulfillment delays or logistics issues.

---

###  Problem 4: How Can We Categorize Customers into Segments Based on Total Sales?

Customer segmentation is crucial for targeting and personalization. In this scenario, we classify customers into **Low**, **Medium**, or **High** value based on their total purchases.

---

###  Problem 5: How Can We Calculate Customer Retention Rate Based on Repeat Purchases?

Retention rate is a key customer success metric. This measure helps identify how many customers made more than one purchase, which indicates brand loyalty or satisfaction.

---

###  Problem 6: How to Calculate Each Product Category’s Sales Contribution Relative to Total Sales?

This KPI shows how much each category contributes to total revenue. It helps in identifying key drivers and underperformers within the product portfolio.

---
### ⭐⭐Bonus Problem – How can we calculate the number of repeat customers using different DAX approaches?
## Output Screenshots

<img width="800" height="600" alt="image" src="https://github.com/user-attachments/assets/7c5ca8f3-e09f-4f79-a866-15823708be23" />

<img width="771" height="681" alt="image" src="https://github.com/user-attachments/assets/b507e2eb-139f-4a42-bea9-5c342ca0bfc7" />



##  How to Use

1. **Open the `.pbix` file** in Power BI Desktop.
2. Each page contains:
   - The problem description
   - A section for you to try solving it
   - A final DAX solution
   - An explanation of each step in the DAX logic
3. **Compare your answer** with both the raw solution and the explained version.
4. Use the screenshots folder to verify if your result matches expected output.

---

## ✅ Solutions (DAX Code)

> Below are the final DAX measures used for each problem. Full explanations are included in the `.pbix` file.

---

### 🔹 Solution 1 – Average Sales per Customer

```dax
Average Sales per Customer = 
VAR TotalSales = SUM(Sales[SalesAmount])
VAR CustomerCount = DISTINCTCOUNT(Sales[CustomerKey])
RETURN
    IF(CustomerCount > 0, TotalSales / CustomerCount, BLANK())

```
### 🔹 Solution 2 – Year-over-Year Sales Growth (%)
```dax

YoY Sales Growth (%) = 
VAR CurrentYearSales =
    SUM ( Sales[SalesAmount] )
VAR LastYearSales =
    CALCULATE (
        SUM ( Sales[SalesAmount] ),
        SAMEPERIODLASTYEAR ( 'Date'[FullDateAlternateKey] )
    )
RETURN
    DIVIDE ( CurrentYearSales - LastYearSales, LastYearSales, 0 )


```
### 🔹 Solution 3 – Average Days to Ship
```dax
Average Days to Ship = 
VAR DaystoShip = 
DATEDIFF(MIN(Sales[OrderDate]),MIN(Sales[ShipDate]), DAY)
Return

AVERAGEX(
    Sales,
   DaystoShip
)



```
### 🔹 Solution 4 – Customer Segmentation by Sales
```dax
Customer Segment = 
SWITCH(
    TRUE(),
    [Total Sale] < 500, "Low Value",
    [Total Sale] >= 500 && [Total Sale] < 25000, "Medium Value",
    [Total Sale] >= 25000, "High Value",
    "Uncategorized"
)


```
### 🔹 Solution 5 – Customer Retention Rate
```dax

Customer Retention Rate = 
DIVIDE(CALCULATE(
    DISTINCTCOUNT(Sales[CustomerKey]),
    FILTER(
        Sales,
        COUNTROWS(
            FILTER(Sales, Sales[CustomerKey] = EARLIER(Sales[CustomerKey]))
        ) > 1
    )
)
,DISTINCTCOUNT(Sales[CustomerKey]),0)



```
### 🔹 Solution 6 – Sales Contribution per Product Category (%)

```dax
Category Sales Contribution (%) = 
DIVIDE(
    SUM(Sales[SalesAmount]),
    CALCULATE(SUM(Sales[SalesAmount]), ALL('Product Subcategory'[ProductSubcategory])),
    0
) 


```


### Bonus Problem – Repeat Customer Calculation (3 Methods)
## 🔁  – Repeat Customer Calculation Methods

We want to calculate how many **repeat customers** exist — i.e., customers who have made **more than one purchase**.

---

###  Method 1: Using `SUMMARIZE`

```dax
Repeat Customer = 
CALCULATE(
    DISTINCTCOUNT(Sales[CustomerKey]),
    FILTER(
        SUMMARIZE(Sales, Sales[CustomerKey], "CustomerCount", COUNTROWS(Sales)),
        [CustomerCount] > 1
    )
)

```
#### Explanation:

SUMMARIZE creates a virtual table summarizing the number of sales (CustomerCount) per customer.

We filter this table to keep only customers with more than 1 purchase.

Then, DISTINCTCOUNT(Sales[CustomerKey]) counts how many such customers exist in the original data context.

### Method 2: Using EARLIER
```dax

Repeat Customers = 
CALCULATE(
    DISTINCTCOUNT(Sales[CustomerKey]),
    FILTER(
        Sales,
        COUNTROWS(
            FILTER(Sales, Sales[CustomerKey] = EARLIER(Sales[CustomerKey]))
        ) > 1
    )
)




```
#### Explanation:

For each row in the Sales table, we use EARLIER to refer to the outer row context.

Then, we filter for customers whose total purchases (COUNTROWS) are greater than 1.

Finally, DISTINCTCOUNT returns the number of such unique customers.
### Method 3: Using VAR (Modern, Readable)
```dax

Variable Repeat Customer = 
CALCULATE(
    DISTINCTCOUNT(Sales[CustomerKey]),
    FILTER(
        Sales,
        VAR CurrentCustomerKey = Sales[CustomerKey]
        RETURN
            COUNTROWS(
                FILTER(Sales, Sales[CustomerKey] = CurrentCustomerKey)
            ) > 1
    )
)




```
#### Explanation:

Uses a VAR to store the current customer key, making the logic cleaner and easier to follow.

We filter for customers who appear more than once in the dataset.

Then, DISTINCTCOUNT returns the total number of unique repeat customers.
