# SQL-challenge: 

## Background
It’s been two weeks since you were hired as a new data engineer at Pewlett Hackard (a fictional company). Your first major task is to do a research project about people whom the company employed during the 1980s and 1990s. All that remains of the employee database from that period are six CSV files.

For this project, you’ll design the tables to hold the data from the CSV files, import the CSV files into a SQL database, and then answer questions about the data. That is, you’ll perform data modeling, data engineering, and data analysis, respectively.

This Challenge is divided into three parts: 
- Data Modeling
- Data Engineering
- Data Analysis

## Data Modeling

Entity Relationship Diagram

![EDR](https://github.com/user-attachments/assets/39eb9cf9-1cae-4c50-90dd-a6656becdd37)


## Data Engineering 
See the table-schema.sql file
-- Data Engineering --
-- Drop Tables if Existing
DROP TABLE IF EXISTS departments;
DROP TABLE IF EXISTS dept_emp;
DROP TABLE IF EXISTS dept_manager;
DROP TABLE IF EXISTS employees;
DROP TABLE IF EXISTS salaries;
DROP TABLE IF EXISTS titles;

-- Exported from QuickDBD: Specifying Data Types, Primary Keys & Foreign Keys 

CREATE TABLE "dept_emp" (
    "emp_no" INT   NOT NULL,
    "dept_no" VARCHAR(10)   NOT NULL
);

CREATE TABLE "employees" (
    "emp_no" INT   NOT NULL,
    "emp_title_id" VARCHAR(10)   NOT NULL,
    "birth_date" VARCHAR(8)   NOT NULL,
    "first_name" VARCHAR(20)   NOT NULL,
    "last_name" VARCHAR(20)   NOT NULL,
    "sex" VARCHAR(1)   NOT NULL,
    "hire_date" VARCHAR(8)   NOT NULL,
    CONSTRAINT "pk_employees" PRIMARY KEY (
        "emp_no"
     )
);

CREATE TABLE "departments" (
    "dept_no" VARCHAR(10)   NOT NULL,
    "dept_name" VARCHAR(30)   NOT NULL,
    CONSTRAINT "pk_departments" PRIMARY KEY (
        "dept_no"
     )
);

CREATE TABLE "dept_manager" (
    "dept_no" VARCHAR(10)   NOT NULL,
    "emp_no" INT   NOT NULL
);

CREATE TABLE "salaries" (
    "emp_no" INT   NOT NULL,
    "salary" INT   NOT NULL
);

CREATE TABLE "titles" (
    "title_id" VARCHAR(5)   NOT NULL,
    "title" VARCHAR(30)   NOT NULL,
    CONSTRAINT "pk_titles" PRIMARY KEY (
        "title_id"
     )
);

ALTER TABLE "dept_emp" ADD CONSTRAINT "fk_dept_emp_emp_no" FOREIGN KEY("emp_no")
REFERENCES "employees" ("emp_no");

ALTER TABLE "dept_emp" ADD CONSTRAINT "fk_dept_emp_dept_no" FOREIGN KEY("dept_no")
REFERENCES "departments" ("dept_no");

ALTER TABLE "employees" ADD CONSTRAINT "fk_employees_emp_no" FOREIGN KEY("emp_no")
REFERENCES "dept_manager" ("emp_no");

ALTER TABLE "employees" ADD CONSTRAINT "fk_employees_emp_title_id" FOREIGN KEY("emp_title_id")
REFERENCES "titles" ("title_id");

ALTER TABLE "departments" ADD CONSTRAINT "fk_departments_dept_no" FOREIGN KEY("dept_no")
REFERENCES "dept_manager" ("dept_no");

ALTER TABLE "salaries" ADD CONSTRAINT "fk_salaries_emp_no" FOREIGN KEY("emp_no")
REFERENCES "employees" ("emp_no");

-- Query * FROM Each Table Confirming Data
SELECT * FROM departments;
SELECT * FROM titles;
SELECT * FROM employees;
SELECT * FROM dept_emp;
SELECT * FROM dept_manager;
SELECT * FROM salaries;

## Data Analysis 

Data analysis performed in files:
analysis_queries.sql

1. List the employee number, last name, first name, sex, and salary of each employee.
   Example:
![image](https://github.com/user-attachments/assets/d0ebd7a4-7333-4201-8d38-4fcac3dc815a)

2. List the first name, last name, and hire date for the employees who were hired in 1986.
   Example:
![image](https://github.com/user-attachments/assets/388d8ebf-eb59-4bfe-9f6a-54740fc5441c)

3. List the manager of each department along with their department number, department name, employee number, last name, and first name.
   Example:
   ![image](https://github.com/user-attachments/assets/868b3eaa-c4bc-4c1d-8fd0-89627ad108bf)

4. List the department number for each employee along with that employee’s employee number, last name, first name, and department name.
   Example:
   ![image](https://github.com/user-attachments/assets/931e4f66-7841-4c09-8abf-6b7d28dd7743)

5. List first name, last name, and sex of each employee whose first name is Hercules and whose last name begins with the letter B.
   Example:
   ![image](https://github.com/user-attachments/assets/313a2a89-b497-4e59-9e58-08ed94ff929f)

6. List each employee in the Sales department, including their employee number, last name, and first name.
   Example:
   ![image](https://github.com/user-attachments/assets/fb9cc401-e825-428f-af93-d768ac8a7fed)

7. List each employee in the Sales and Development departments, including their employee number, last name, first name, and department name.
   Example:
   ![image](https://github.com/user-attachments/assets/17d32089-bdb8-449c-a804-0e5e1c711343)

8. List the frequency counts, in descending order, of all the employee last names (that is, how many employees share each last name).
   Example:
   ![image](https://github.com/user-attachments/assets/cc888114-a251-4c85-9abd-a4a7f585fd9d)



