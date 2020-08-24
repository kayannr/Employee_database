# Employee Database: A Mystery in Two Parts (SQL)

## Background 
This project involves conducting a research project on employees of the corporation from the 1980s and 1990s. All that remain of the database of employees from that period are six CSV files. The tables are designed to hold data in the CSVs which is then imported into a SQL database. In other words, the following are performed:
>   * Data Modeling
>   * Data Engineering
>   * Data Analysis

## Objectives 
### Data Modeling 
![data](EmployeeSQL/ERD/employees_erd1.png)

### Data Engineering 
* The information are used to create a table schema for each of the six CSV files. Data types, primary keys, foreign keys, and other constraints are specified.
* Each CSV file are imported into the corresponding SQL table.

```
- Data Engineering --
-- Drop Tables if Existing
--DROP TABLE IF EXISTS departments;
--DROP TABLE IF EXISTS dept_employees;
--DROP TABLE IF EXISTS dept_managers;
--DROP TABLE IF EXISTS employees;
--DROP TABLE IF EXISTS salaries;
--DROP TABLE IF EXISTS titles;

-- Exported from QuickDBD: https://www.quickdatabasediagrams.com/
-- Link to schema: https://app.quickdatabasediagrams.com/#/d/0JOpLb
-- NOTE! If you have used non-SQL datatypes in your design, you will have to change these here.


CREATE TABLE "departments" (
    "dept_no" VARCHAR(4)   NOT NULL,
    "dept_name" VARCHAR(20)   NOT NULL,
    CONSTRAINT "pk_departments" PRIMARY KEY (
        "dept_no"
     )
);

CREATE TABLE "dept_employees" (
    "emp_no" INTEGER   NOT NULL,
    "dept_no" VARCHAR(4)   NOT NULL
);

CREATE TABLE "dept_managers" (
    "dept_no" VARCHAR(4)   NOT NULL,
    "emp_no" INTEGER   NOT NULL
);

CREATE TABLE "employees" (
    "emp_no" INTEGER   NOT NULL,
    "emp_title_id" VARCHAR(5)   NOT NULL,
    "birth_date" DATE   NOT NULL,
    "first_name" VARCHAR(20)   NOT NULL,
    "last_name" VARCHAR(20)   NOT NULL,
    "sex" VARCHAR(1)   NOT NULL,
    "hire_date" DATE   NOT NULL,
    CONSTRAINT "pk_employees" PRIMARY KEY (
        "emp_no"
     )
);

CREATE TABLE "salaries" (
    "emp_no" INTEGER   NOT NULL,
    "salary" INTEGER   NOT NULL
);

CREATE TABLE "titles" (
    "title_id" VARCHAR(5)   NOT NULL,
    "title" VARCHAR(20)   NOT NULL,
    CONSTRAINT "pk_titles" PRIMARY KEY (
        "title_id"
     )
);

ALTER TABLE "dept_employees" ADD CONSTRAINT "fk_dept_employees_emp_no" FOREIGN KEY("emp_no")
REFERENCES "employees" ("emp_no");

ALTER TABLE "dept_employees" ADD CONSTRAINT "fk_dept_employees_dept_no" FOREIGN KEY("dept_no")
REFERENCES "departments" ("dept_no");

ALTER TABLE "dept_managers" ADD CONSTRAINT "fk_dept_managers_dept_no" FOREIGN KEY("dept_no")
REFERENCES "departments" ("dept_no");

ALTER TABLE "dept_managers" ADD CONSTRAINT "fk_dept_managers_emp_no" FOREIGN KEY("emp_no")
REFERENCES "employees" ("emp_no");

ALTER TABLE "employees" ADD CONSTRAINT "fk_employees_emp_title_id" FOREIGN KEY("emp_title_id")
REFERENCES "titles" ("title_id");

ALTER TABLE "salaries" ADD CONSTRAINT "fk_salaries_emp_no" FOREIGN KEY("emp_no")
REFERENCES "employees" ("emp_no");


-- Query * FROM Each Table To Confirm Data Is Correct
SELECT * FROM "titles"; 
SELECT * FROM "employees"; 
SELECT * FROM "salaries"; 
SELECT * FROM "departments"; 
SELECT * FROM "dept_employees"; 
SELECT * FROM "dept_managers"; 
```

