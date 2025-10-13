# 🧩 Problem 02 – Top 5 Customers with "Others" Group

## 📝 Objective

Identify the **Top 5 Customers by Total Sales** and group **all remaining customers** into a single row labeled **"Remaining Customers"**.

The output should show **6 rows** in total:

- Top 5 customers (individually listed)
- 6th row = All other customers combined, shown as `"Remaining Customers"`

---

## 🎯 Requirements

- Use the **Customers**, **Orders**, and **Products** tables.
- Calculate **Total Sales** per customer.
- Display only the **Top 5 customers** individually.
- Combine all **other customers** into one group labeled `"Remaining Customers"`.
- **Sort the results in descending order of total sales**,  
  ➤ but ensure the **"Remaining Customers" row always appears last**,  
  even if its total is higher than some of the top 5.

---

## 🧠 DAX Challenge

For learning purposes, this problem has been solved using **three different DAX approaches**:

- **Two methods** using **calculated tables**, showcasing different ways to build the result table.
- **One method** using a **calculated column** approach, demonstrating an alternative technique.

Try implementing the logic yourself and compare your solutions with these methods to deepen your understanding of DAX.

---

## 🧩 Expected Output (Example)

<img width="800" height="450" alt="image" src="https://github.com/user-attachments/assets/4d412fde-e1c8-4262-bdc1-eaf1ea938037" />

---

## 📁 Dataset Tables

- `Customers`
- `Orders`
- `Products`

Ensure relationships are correctly defined:

- `Orders[CustomerID]` → `Customers[CustomerID]`
- `Orders[ProductID]` → `Products[ProductID]`

---

## 💡 Goal

This is a common DAX pattern used in Power BI dashboards where stakeholders want to:

- Highlight **top-performing customers**
- Group the **long tail** into a single "Others" category
- Maintain clean, focused visuals while retaining total values

---

## 🧩 Bonus: DAX Logic Hint

If you're stuck or want to validate your approach, you can refer to the DAX logic below as a guide.

> 💡 Try solving the problem in your own Power BI file first.  
> If needed, you can explore the DAX code provided below — or check the **solution Power BI file** included in the folder.

---

### Method 1: Calculated Table Using `TOPN`, `EXCEPT`, and `UNION`

```dax
Topcustomer1 = 
VAR Nvalue = 5 
VAR Allcustomer = 
    ADDCOLUMNS(
        VALUES(Customers[CustomerName]),
        "Totalsale", [CustomerSale]
    )

VAR TopNcustomer = 
    TOPN(Nvalue, Allcustomer, [Totalsale], DESC)

VAR Remainingcustomer = 
    EXCEPT(Allcustomer, TopNcustomer)

VAR Remainingcustomersale =
    ADDCOLUMNS(
        DATATABLE("CustomerName", STRING, {{"Remaining Customers"}}),
        "Totalsale", SUMX(Remainingcustomer, [Totalsale]),
        "Ranking", Nvalue + 1
    )

VAR topnranking = 
    ADDCOLUMNS(
        TopNcustomer,
        "Ranking", RANKX(TopNcustomer, [Totalsale], , DESC)
    )

VAR topnwithremaining = 
    UNION(topnranking, Remainingcustomersale)

RETURN
    topnwithremaining
```
### Method 2: Calculated Table Using ADDCOLUMNS and RANKX with Conditional Grouping
```dax
Topcustomer2 = 
VAR AllCustomer =
    ADDCOLUMNS(
        VALUES(Customers[CustomerName]),
        "Customers", IF(RANKX(ALL(Customers), [CustomerSale], , DESC) <= 5, Customers[CustomerName], "RemainingCustomer"),
        "Totalsale", [CustomerSale]
    )

VAR CustomerRanking = 
    ADDCOLUMNS(
        AllCustomer,
        "Ranking", IF([Customers] = "RemainingCustomer", 6, RANKX(ALL(Customers), [CustomerSale], , DESC))
    )

RETURN
    CustomerRanking
```

