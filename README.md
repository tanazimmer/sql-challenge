# SQL Homework - Employee Database: A Mystery in Two Parts

## Primary Coding Language and Skills: SQL, Python

It is a beautiful spring day, and it is two weeks since you have been hired as a new data engineer at Pewlett Hackard. Your first major task is a research project on employees of the corporation from the 1980s and 1990s. All that remain of the database of employees from that period are six CSV files.
###Challenges:

#### Data Modeling
Inspect the CSVs and sketch out an ERD of the tables.
![ERD](https://github.com/tanazimmer/sql-challenge/blob/master/QuickDBD-HW.png)

#### Data Engineering

* Use the information you have to create a table schema for each of the six CSV files. Remember to specify data types, primary keys, foreign keys, and other constraints.


#### Data Analysis

Once you have a complete database, do the following:

1. List the following details of each employee: employee number, last name, first name, sex, and salary.
```
SELECT e.emp_no, e.last_name, e.first_name, e.sex, s.salary
FROM employees as e
INNER JOIN salaries as s ON
e.emp_no = s.emp_no;
```
2. List first name, last name, and hire date for employees who were hired in 1986.
```
SELECT first_name, last_name, hire_date
FROM employees
WHERE DATE_PART('year',hire_date) = 1986;
```

3. List the manager of each department with the following information: department number, department name, the manager's employee number, last name, first name.
```
SELECT * FROM dept_manager;
SELECT * FROM departments;
SELECT * FROM employees;

SELECT dm.dept_no, d.dept_name, dm.emp_no, e.last_name, e.first_name 
FROM employees as e
INNER JOIN dept_manager as dm
on dm.emp_no = e.emp_no
INNER JOIN departments as d
on d.dept_no = dm.dept_no;

```

4. List the department of each employee with the following information: employee number, last name, first name, and department name.
```
SELECT * FROM titles;
SELECT * FROM dept_emp;

SELECT e.emp_no, e.last_name, e.first_name, d.dept_name
FROM employees as e
INNER JOIN dept_emp as de
on de.emp_no = e.emp_no
INNER JOIN departments as d
on d.dept_no = de.dept_no
```

5. List first name, last name, and sex for employees whose first name is "Hercules" and last names begin with "B."

```
SELECT first_name, last_name, sex
FROM employees
WHERE first_name = 'Hercules' AND last_name LIKE 'B%';
```

6. List all employees in the Sales department, including their employee number, last name, first name, and department name.

```
SELECT e.emp_no, e.last_name, e.first_name, d.dept_name
FROM employees as e
INNER JOIN dept_emp as de
ON de.emp_no = e.emp_no
INNER JOIN departments as d
ON d.dept_no = de.dept_no
WHERE dept_name = 'Sales';
```

7. List all employees in the Sales and Development departments, including their employee number, last name, first name, and department name.
```
SELECT e.emp_no, e.last_name, e.first_name, d.dept_name
FROM employees as e
INNER JOIN dept_emp as de
ON de.emp_no = e.emp_no
INNER JOIN departments as d
ON d.dept_no = de.dept_no
WHERE dept_name = 'Sales' OR dept_name = 'Development';
```

8. In descending order, list the frequency count of employee last names, i.e., how many employees share each last name.
```
SELECT last_name, count(last_name) AS "Last Name Count"
FROM employees
GROUP BY last_name
ORDER BY "Last Name Count" DESC;
```

### Bonus (Optional)

* Create a histogram to visualize the most common salary ranges for employees.
![salary range](https://github.com/tanazimmer/sql-challenge/blob/master/images/salray_range.PNG)

* Create a bar chart of average salary by title.
![salary range by title](https://github.com/tanazimmer/sql-challenge/blob/master/images/salaries_bytitle.PNG)

