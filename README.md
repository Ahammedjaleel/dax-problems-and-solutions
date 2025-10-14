
# 🧠 DAX Practice Problems & Solutions

Welcome to this Power BI DAX practice repository — designed for anyone who wants to **learn, practice, and master DAX** through real-world scenarios.

If you're wondering how to approach business problems using DAX, think logically, and choose the right functions — this repository is for you.

---

# 🎯 Purpose of This Repository

This project is designed to help you:

-  Practice solving real-world **DAX** problems  
-  Develop **logical thinking skills** for approaching DAX challenges  
-  Learn how to **break down business scenarios** methodically  
-  Understand which **DAX** functions to use — and why  
-  Enhance your **Power BI** data modeling and problem-solving abilities


---

## 📂 What's Inside

Each folder in this repository represents a unique DAX problem or case study.

### 🧩 Each folder includes:

- A `README.md` explaining the problem in detail
- 📁 **One Power BI files**:
  ## Power BI (.pbix) — Problem + Solution File

- Includes the full **problem statement**
- Provides a dedicated page for you to **build your own solution**
- The solution is available in **two formats**:
  1. **Solution Only** – for quick reference or validation  
  2. **Solution with Explanations** – includes detailed DAX comments and step-by-step breakdowns
- Ideal for both **self-practice** and **in-depth learning**


- 📸 Screenshots showing expected outputs (optional but included in many folders)

---

## 🔗 How to Navigate

- Scroll down to the list of problems below
- **Click any problem title** — it will take you to that problem's folder
- Open the folder's `README.md` for more details, and download the `.pbix` files to start practicing
- Few problems also have a **YouTube video walkthrough** available on my channel
---

## 🧩 Power BI DAX Challenges and Solutions ✅

[❓**01 - Customer Purchase Analysis**](https://github.com/Ahammedjaleel/dax-problems-and-solutions/tree/main/01-customer-purchase-analysis)



> This section focuses on analyzing customer purchasing behavior using DAX in Power BI. Below are the key sub-questions explored in this analysis:

1. ##### Customers with Only One Purchase
   What is the count of customers who made just one purchase?

2. ##### Churned Customers  
   How many customers did not return in the current year?

3. ##### New Customers in the Current Year 
   How many customers made their **first-ever** purchase in the current year?

4. ##### Repeat Customers (Year-over-Year)
   What is the number of customers who made purchases in **both** the current year and the previous year?

5. ##### Average Products per Sale
   What is the average number of products purchased per transaction?

6. ##### Re-solve All of the Above Using `SUMMARIZECOLUMNS` 
   Re-implement the above calculations using the `SUMMARIZECOLUMNS` function  
   (instead of `SUMMARIZE` or `ADDCOLUMNS`) to improve performance or clarity.
   
[❓**02 – Top 5 Customers with "Others" Group**](https://github.com/Ahammedjaleel/dax-problems-and-solutions/tree/main/02-top-5-customers-with-others-group)

> Identify the Top 5 Customers by Total Sales and group all remaining customers into a single row labeled "Remaining Customers".





[❓**03: Different Ways to Calculate Running Totals in Power BI Using DAX**](https://github.com/Ahammedjaleel/dax-problems-and-solutions/tree/main/dax-running-total-problems-solutions)

> Explore multiple techniques to calculate **Running Totals** using DAX functions. Each sub-question challenges you to apply a different method or logic to achieve a cumulative sales calculation.

##### 🔹 3.1: Calculate Running Total using `MAX`

Use the `MAX` function within a `FILTER` context to accumulate sales up to the current date.

---

##### 🔹 3.2: Calculate Running Total using `ISONORAFTER`

Use the `ISONORAFTER` function to compare dates in descending order, useful for ordering and cumulative logic.

---

##### 🔹 3.3: Calculate Running Total for the Last 3 Months

Build a **rolling total** for the last three months from the current date using `DATESBETWEEN` and `EOMONTH`.

---

##### 🔹 3.4: Calculate Year-to-Date (YTD) Running Total using `MAX`

Limit your cumulative total to only include dates **within the same year**, using a `MAX`-based approach.

---

##### 🔹 3.5: Calculate Year-to-Date (YTD) using `TOTALYTD`

Use Power BI’s built-in `TOTALYTD` function to compute running totals from the start of the year to the current date.

---







[![linkedin](https://img.shields.io/badge/linkedin-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/ahammed-jaleel-33772b5b/)
[![YouTube](https://img.shields.io/badge/youtube-FF0000?style=for-the-badge&logo=youtube&logoColor=white)](https://www.youtube.com/@mobsanalytics)
[![Instagram](https://img.shields.io/badge/instagram-C13584?style=for-the-badge&logo=instagram&logoColor=white)](https://www.instagram.com/mobsanalytics/)



