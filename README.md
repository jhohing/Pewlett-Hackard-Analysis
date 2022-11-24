# Pewlett-Hackard-Analysis

## Overview of Project

### Purpose
THis analysis is meant to determine the number of retiring employees per title and identify the employees who are eligible to participate in a mentorship program. It will be used by Bobby's manager to prepare for the "silver tsunami" as current employees reach retirement age.

## Results
- The retirement_titles table was create by joining the employees and titles tables. It shows each employees at every position they held at Pewlett-Hackward. Some employees have moved up the ranks during their tenure with the company. Below you can download the data to view the employees that have moved up the ranks since their hire date.

![retirement_titles_pic](https://github.com/jhohing/Pewlett-Hackard-Analysis/blob/main/retirement_titles.png)

To download: [retirement_titles] (https://github.com/jhohing/Pewlett-Hackard-Analysis/blob/main/Data/retirement_titles.csv)

- The unique_titles table was created by joining the employees and titles tables, Filtering them by date of birth and hired date, removing duplicates, and ordering by the date hired. There are a total of **72,458 employees retiring**.

To download the data: [unique_titles.csv](https://github.com/jhohing/Pewlett-Hackard-Analysis/blob/main/Data/unique_titles.csv)

- Out of those 72,458 employees retiring, 25,916 are Senior Engineers, 24,926 are Senior Staff, 9,285 are Engineers, 7,636, are Staff, 3603 are Technique Leaders, 1090 are Assistant Engineers, and 2 are Managers.

![retiring_titles_pic](https://github.com/jhohing/Pewlett-Hackard-Analysis/blob/main/retiring_titles.png)

To download the data: [retiring_titles.csv](https://github.com/jhohing/Pewlett-Hackard-Analysis/blob/main/Data/retiring_titles.csv)

- The mentorship_eligibility table was created joining the employees, department employees, and titles tables. The data is filters to including employees that were born in 1965 and that are current working for Pewlett Hackard. This will determine if thesse employees are eligible for the mentorship program. There are 1,549 eligible employees.

![mentorship_eligible_emps](https://github.com/jhohing/Pewlett-Hackard-Analysis/blob/main/mentorship_eligible_emps.png)

To download the data: [mentorship_eligibility.csv] (https://github.com/jhohing/Pewlett-Hackard-Analysis/blob/main/Data/mentorship_eligibility.csv)

## Summary
Based on the findings in my analysis, Pewlett Hackard could look at having 90,000 vacant positions company wide. Considering there are only 1,549 employees eligible for the mentorship program, Pewlett Hackard will not have enough qualified employees to mentor the the next generation.

This query shows the number of each eligible employee for the mentorship program per each title.

````
SELECT COUNT(me.emp_no) as emp_count, me.title
FROM mentorship_eligibility as me
GROUP BY me.title
ORDER BY emp_count DESC;

````

This query showsa the years each employee that is set to retire worked for Pewlett Hackard. Below is the queyr and a link to access the data.

````
SELECT ut.emp_no,
ut.first_name,
ut.last_name,
ut.title,
e.hire_date,
DATE_PART('year', CURRENT_DATE::date) - DATE_PART('year', e.hire_date::date) as years
INTO emp_tenure
FROM unique_titles as ut
INNER JOIN employees as e
ON e.emp_no = ut.emp_no
ORDER BY ut.emp_no

````
To download the data: [emp_tenure.csv] (https://github.com/jhohing/Pewlett-Hackard-Analysis/blob/main/Data/emp_tenure.csv)
