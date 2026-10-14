# Employee Performance and Attrition Analysis (SQL and Power BI)

A Power BI dashboard that looks at a small HR dataset from four angles: how many people work in each department, who has left, how performance review scores compare, and how salaries have moved over time.

The dataset is synthetic and small (30 employees, 200 performance reviews, 90 salary records), so it works well as a learning project or a template for a larger HR report.

## What's in the dashboard

The report is a single page, built from the CSV files in this project. It includes:

- **KPI cards** for average performance score, total attrition count and total employees.
- **Headcount by department**, shown as a donut chart.
- **Attrition count by department**, shown as a bar chart.
- **Salary trend**, with minimum, average and maximum salary by year.
- **Annual attrition**, combining the number of employees who left with the yearly attrition rate.
- **Top performers**, showing the highest average review score in each department.
- **Slicers** for join year, exit year, salary year and department, so every visual can be filtered.

## What the data shows

These figures come straight from the CSV files:

| Department  | Employees | Exits | Share who left |
|-------------|-----------|-------|----------------|
| Engineering | 10        | 3     | 30%            |
| HR          | 9         | 5     | 56%            |
| Sales       | 6         | 5     | 83%            |
| Finance     | 5         | 3     | 60%            |
| **Total**   | **30**    | **16**| **53%**        |

- Engineering is the largest department and has the lowest share of leavers. Sales is the smallest after Finance and loses the highest share of its people.
- The average review score across all 200 reviews is about 7.3 on a scale where scores range from 4 to 10. By department, HR averages about 7.5, Finance 7.4, Engineering 7.1 and Sales 7.0.
- Exits fall between 2017 and 2024, with the most in 2019 (five). No one left in 2022.
- Average salary by year sits between roughly 57,700 and 71,400. The 2023 figure rests on a single record, so don't read much into it.

## Tech stack

- **Power BI Desktop** for the data model, measures and visuals
- **DAX** for the dashboard measures (Avg Performance Score, Total Attrition Count, Total Employees)
- **SQL** for preparing the summary tables (the SQL scripts are not included in this project)
- **CSV** files as the data source

## Project contents

```
README.md
Employee_Performance_and_Attrition_Analysis_Using_SQL_and_Power_BI.pbix   Power BI report and data model

employees.csv                  30 employees: department, join date, exit date, gender
departments.csv                4 departments (HR, Engineering, Sales, Finance)
salaries.csv                   90 salary records with effective dates (2015 to 2023)
performance_reviews.csv        200 reviews with date, score and reviewer (2018 to 2023)

Salary_Trend.csv               Average, max and min salary by year and department
Salary_Trends_Over_Time.csv    Average, max and min salary by year, all departments
Top_performers_per_dept.csv    Highest average review score in each department
Attrition_Rate_per_Year.csv    Employees who left per year, with a rate column
```

### How the tables relate

- `employees.DepartmentID` links to `departments.DepartmentID`
- `salaries.EmployeeID` links to `employees.EmployeeID`
- `performance_reviews.EmployeeID` links to `employees.EmployeeID`

The four summary files at the bottom of the list were prepared separately and feed specific visuals.

## Prerequisites

- **Power BI Desktop**, which is free from Microsoft and runs on Windows. The `.pbix` file can't be opened in a browser or on macOS without a Windows environment.

Nothing else needs to be installed to view the dashboard. The CSV files are plain text, so you can also open them in Excel, a text editor or any data tool.

## Getting started

1. Download or clone the project so all files sit in one folder.
2. Open the `.pbix` file in Power BI Desktop.
3. Use the slicers to filter by year or department.

If Power BI reports that it can't find a data source, go to **Home > Transform data > Data source settings**, choose **Change Source**, and point each entry to the matching CSV in your local folder. Then select **Refresh**.

## Working with the data

A few notes if you plan to reuse or extend the project:

- **Dates:** `JoinDate`, `ExitDate`, `EffectiveFrom` and `ReviewDate` are in `YYYY-MM-DD` format. An empty `ExitDate` means the employee is still with the company, which is how attrition is counted.
- **Salary history:** each employee has several salary rows. Yearly averages use every salary record effective in that year.
- **Review scores:** each employee has at least three reviews, so department and employee averages are based on a handful of data points.

## Known limitations

- **The annual attrition rate is always 100%.** In `Attrition_Rate_per_Year.csv`, `TotalEmployees` equals `EmployeesLeft` for every year, because only the people who left that year are counted in the denominator. The "Employees Left" counts are reliable, but the rate column is not meaningful as it stands. A more useful rate would divide exits by the headcount at the start of each year, which needs the join and exit dates in `employees.csv`.
- **Small sample.** With 30 employees, a single person leaving moves a department's percentage a lot, so treat the department comparisons as illustrative rather than conclusive.
- **Synthetic data.** The employee records are made up for the exercise, so the patterns don't describe any real organisation.

## Troubleshooting

| Problem | What to try |
|---|---|
| The file won't open | Make sure you're using a recent Power BI Desktop release; older versions may not read newer reports. |
| Visuals are empty after opening | Refresh the report, and check the data source paths as described above. |
| Numbers differ from the CSVs | Check for active slicers. A filtered year or department changes every KPI card. |
