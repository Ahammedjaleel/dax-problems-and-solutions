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

##  Problem Descriptions

> The dataset contains the following tables:  
> `Sales`, `Dates`, `Customer`, `Country`, `Product`, `Product Subcategory`, `Product Category`.

### 💡 Problem 1: What is the Average Sales per Customer?

We want to understand how much each customer spends on average. This metric helps evaluate customer value and guides marketing and retention strategies.

---

### 💡 Problem 2: How to Calculate Year-over-Year Sales Growth for Each Product Category?

This question aims to analyze sales growth trends over time. Year-over-Year (YoY) growth helps us assess business performance and seasonality for each category.

---

### 💡 Problem 3: What is the Average Number of Days it Takes to Ship Orders per Product Category?

Shipping efficiency is a key performance indicator. This problem calculates the average delivery time for each product category to help spot fulfillment delays or logistics issues.

---

### 💡 Problem 4: How Can We Categorize Customers into Segments Based on Total Sales?

Customer segmentation is crucial for targeting and personalization. In this scenario, we classify customers into **Low**, **Medium**, or **High** value based on their total purchases.

---

### 💡 Problem 5: How Can We Calculate Customer Retention Rate Based on Repeat Purchases?

Retention rate is a key customer success metric. This measure helps identify how many customers made more than one purchase, which indicates brand loyalty or satisfaction.

---

### 💡 Problem 6: How to Calculate Each Product Category’s Sales Contribution Relative to Total Sales?

This KPI shows how much each category contributes to total revenue. It helps in identifying key drivers and underperformers within the product portfolio.

---

## 📂 File Structure

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
```dax



```

```dax



```

```dax


```

```dax




```


```dax


```
