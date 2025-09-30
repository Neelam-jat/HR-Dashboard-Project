# HR Dashboard Project

![HR Dashboard Screenshot](HR%20Summary.png)

## Repository Structure

This repository contains all files needed to reproduce and review the HR Dashboard project:

- **Dashboard_HR_.twbx** &mdash; Tableau packaged workbook.
- **HR Summary.png** &mdash; Screenshot of the HR dashboard (see above).
- **LICENSE** &mdash; Project license information.
- **README.md** &mdash; Project documentation (this file).

---

## Overview

This project presents an interactive Human Resources (HR) dashboard built in Tableau, designed to help organizations visualize, analyze, and make data-driven decisions about their workforce. The dashboard leverages cleaned and well-structured HR data processed using SQL and Python, and is published for public access on [Tableau Public](https://public.tableau.com/app/profile/neelam.s.jat/viz/Dashboard_HR_17573520292220/HRSummary).

## Purpose

The purpose of this dashboard is to provide HR leaders and analysts with actionable insights into key workforce metrics, such as employee demographics, department distribution, hiring and termination trends, performance ratings, and salary analytics. It supports data-informed decision making for talent management, diversity and inclusion, and compensation planning.

## Key Business Questions Answered

1. **How many employees are currently active, hired, or terminated over time?**
2. **Which departments have the largest workforce and highest turnover?**
3. **What is the gender distribution across the organization?**
4. **How do education level and age relate to employee performance?**
5. **Is there a relationship between education, gender, and salary?**
6. **How does average salary vary by age and job role?**
7. **What is the geographic distribution of employees between HQ and branch locations?**
8. **Which education levels are associated with higher performance ratings?**
9. **What are the salary trends for different job titles and age groups?**

## Dashboard Features

- **Overview KPIs:** Active employees, hires, terminations.
- **Department Analysis:** Headcount per department.
- **Demographics:** Gender breakdown, education vs. age, education vs. performance.
- **Income Analytics:** Salary by education and gender.
- **Location Map:** HQ vs. branch distribution.
- **Age vs. Salary Scatterplot:** Highlights job roles and salary averages.
- **Interactive Filters:** Slice by gender, status, location, hire date.

## Data Pipeline

1. **Data Sources:** Raw HR data exported from HRIS/ERP systems or Kaggle datasets.
2. **Data Cleaning:** 
   - SQL for initial structuring (deduplication, filtering, joins).
   - Python for further cleaning (handling missing values, standardizing formats).
3. **Tableau Preparation:** Cleaned CSV or database tables imported into Tableau for visualization.

## Sample SQL Script

```sql name=hr_data_cleaning.sql
-- Remove duplicates and select relevant columns
SELECT DISTINCT
    employee_id,
    first_name,
    last_name,
    gender,
    age,
    education_level,
    department,
    salary,
    performance_rating,
    hire_date,
    termination_date,
    location,
    job_title
FROM raw_hr_data
WHERE status IN ('Active', 'Terminated', 'Hired');
```

## Sample Python Script

```python name=hr_data_cleaning.py
import pandas as pd

# Load raw data
df = pd.read_csv('raw_hr_data.csv')

# Drop duplicates
df = df.drop_duplicates(subset=['employee_id'])

# Fill missing values
df['performance_rating'].fillna('Satisfactory', inplace=True)
df['salary'] = df['salary'].fillna(df['salary'].median())

# Standardize education levels
education_map = {
    'HS': 'High School',
    'Bachelors': 'Bachelor',
    'Masters': 'Master',
    'PhD': 'PhD'
}
df['education_level'] = df['education_level'].replace(education_map)

# Save cleaned data
df.to_csv('clean_hr_data.csv', index=False)
```

## Project Structure

```text
HR-Dashboard-Project/
├── README.md
├── hr_data_cleaning.sql
├── hr_data_cleaning.py
├── clean_hr_data.csv
├── Dashboard_HR_.twbx
├── HR Summary.png
└── LICENSE
```

## License

This project uses the [Creative Commons Attribution 4.0 International (CC BY 4.0) License](https://creativecommons.org/licenses/by/4.0/), allowing others to share and adapt the work with proper attribution to the original author.

```
Creative Commons Attribution 4.0 International (CC BY 4.0)
```

## How to Reproduce

1. **Download raw HR data (CSV or database dump).**
2. **Run SQL and Python scripts to clean and prepare the data.**
3. **Import cleaned data into Tableau and open the dashboard file (`Dashboard_HR_.twbx`).**
4. **Publish or share via Tableau Public.**

## Tableau Dashboard Link

[View the HR Dashboard on Tableau Public](https://public.tableau.com/app/profile/neelam.s.jat/viz/Dashboard_HR_17573520292220/HRSummary)

---

## Inferred Business Insights

### 1. How many employees are currently active, hired, or terminated over time?
- **Active Employees:** 7,984
- **Hired:** 8,950
- **Terminated:** 966
  - The dashboard shows trends over time for both hires and terminations, helping HR track workforce growth and attrition.

### 2. Which departments have the largest workforce and highest turnover?
- **Largest Departments:** 
  - Operations (highest headcount)
  - Sales
  - Customer Service
  - IT
- **Smaller Departments:** Marketing, Finance, HR
  - Operations and Sales are the primary workforce drivers.

### 3. What is the gender distribution across the organization?
- **Gender Ratio:**
  - Female: 46%
  - Male: 54%
  - The dashboard provides quick filtering by gender.

### 4. How do education level and age relate to employee performance?
- **Education & Age:** 
  - Most employees with a Master's degree are in the 35-44 age group.
- **Education & Performance:** 
  - Employees with higher education (Master/PhD) are more likely to have "Excellent" or "Good" performance ratings.
  - 50% of employees with a Bachelor’s degree have "Good" performance.

### 5. Is there a relationship between education, gender, and salary?
- **Income by Education & Gender:**
  - PhD holders earn the highest average salaries (up to 93K for males).
  - Salary increases with education level for both genders.
  - Females with Master’s degrees earn 80K; males earn 86K.
  - Gender gap is visible but not dramatic for higher education levels.

### 6. How does average salary vary by age and job role?
- **Age vs. Salary:**
  - Salary ranges from 60K to 120K.
  - IT Manager has the highest salary cluster (close to 120K).
  - HR Manager is marked near the average.
  - Older age groups (>40) generally have higher salaries.

### 7. What is the geographic distribution of employees between HQ and branch locations?
- **Location Distribution:**
  - HQ: 70% of employees
  - Branch: 30% of employees
  - Most employees are concentrated in HQ, with branches in states like New York, Pennsylvania, Michigan, Ohio, West Virginia.

### 8. Which education levels are associated with higher performance ratings?
- **Performance by Education:**
  - Master’s and PhD degrees correlate with higher “Excellent” and “Good” ratings.
  - Bachelor’s degree employees often have “Good” performance.

### 9. What are the salary trends for different job titles and age groups?
- **Salary Trends:**
  - IT Managers are top earners.
  - HR Managers are at or below average.
  - Salary generally increases with age and education.
  - Significant jump for PhD holders.

**These insights are derived from the HR Dashboard visualizations in the attached Tableau workbook and summary image. For further analysis or custom queries, refer to the SQL and Python scripts included in this repository.**

---

**Author:** [Neelam S Jat]
