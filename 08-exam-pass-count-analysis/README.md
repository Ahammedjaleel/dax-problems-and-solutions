
# 08 - exam-pass-count-analysis

Analyze the total number of subjects each student has **passed**, with dynamic behavior based on filters — such as whether a single subject or all subjects are selected — using DAX in Power BI.

---

## 📁 Dataset Table

This analysis uses a single table:

- `ExamResult`

### 📄 ExamResult Table Columns:
| Column        | Description                           |
|---------------|----------------------------------------|
| `StudentName` | Name of the student                    |
| `Subject`     | Name of the subject                    |
| `Result`      | Result of the exam (`Pass` or `Fail`)  |

<img width="337" height="473" alt="image" src="https://github.com/user-attachments/assets/01011d21-5faf-4f92-981c-f45260970639" />


---

## 🔗 Relationships

_No relationships are required for this specific analysis, as all data is within a single table._

---

## ❓ What Are We Solving?

This DAX challenge explores how to **count the number of passed subjects per student**, while intelligently handling situations where the data may or may not be filtered down to a single subject.

---

##  Output Screenshot

<img width="600" height="400" alt="image" src="https://github.com/user-attachments/assets/7a8e7ade-8c1c-4c2e-977d-d680af59476b" />


---

## 💡 Problem Statement

> Solve the following using DAX to improve your understanding of row context, filtering, and conditional logic.

---

### 🔹 Problem 21: Count of Subjects Passed by Each Student

**Objective:**  
Display the **total number of subjects that each student has passed**. The measure should adapt dynamically based on filters — for example, whether a single subject is selected or not.

This helps when building reports that display both subject-level and overall student performance, depending on slicers or visual context.

---

## ✅ Solution 21A: Using `HASONEVALUE`

```dax
Answer21_Count_hasonevalue = 
IF (
    HASONEVALUE ( ExamResult[Subject] ),
    SELECTEDVALUE ( ExamResult[Result] ),
    COUNTROWS (
        FILTER ( ExamResult, ExamResult[Result] = "Pass" )
    )
)
```
## ✅ Solution 21B: Using ISINSCOPE (Same Logic, Different Function)

```dax
Answer21_Explanation_Count_Isinscope = 
IF (
    ISINSCOPE ( ExamResult[Subject] ),  // Check if 'ExamResult[Subject]' is in the current filter context
    SELECTEDVALUE ( ExamResult[Result] ),  // Return the result for that subject
    COUNTROWS (
        FILTER ( ExamResult, ExamResult[Result] = "Pass" )  // Count how many subjects are passed
    )
)

```
## Explanation:

Both versions solve the same logic using different functions:

HASONEVALUE checks whether there’s exactly one value in the current context.

ISINSCOPE checks if a column is present in the current grouping/filter context — ideal for visuals like matrix or tables.

These are useful for building adaptive DAX measures that behave differently based on the filter or visual context.

---

#### Let's Connect
[![github](https://img.shields.io/badge/github-181717?style=for-the-badge&logo=github&logoColor=white)](https://github.com/ahammedjaleel)
[![linkedin](https://img.shields.io/badge/linkedin-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/ahammed-jaleel-33772b5b/)
---
