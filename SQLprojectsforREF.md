# SQL
Projects
BY SHERIFF ADEYEYE

CREATE DATABASE ORDERS;
USE ORDERS;
--
CREATE TABLE orders(
REF_NO CHAR(14) NOT NULL,
ORD_DTE DATE NOT NULL DEFAULT '1990-01-01',
CUST_NAME VARCHAR(50) NOT NULL,
CATEGORY VARCHAR(20) NOT NULL,
PRODUCT VARCHAR(20) NOT NULL,
SALES DECIMAL(18, 5),
PROFIT DECIMAL(18, 5)
);

INSERT INTO orders VALUES ('CA-2012-124891', '2012-07-31', 'Rick Hansen', 'Technology', 'Accessories', 2309.65, 762.1845),
('CA-2014-135909', '2014-10-14', 'Jane Waco', 'Office Supplies', 'Binders', 5083.96, 1906.485),  ('CA-2012-116638', '2012-01-28', 'Joseph Holt', 'Furniture', 'Tables', 4297.644, -1862.3124),  ('CA-2014-143567', '2014-03-11', 'Thomas Boland', 'Technology', 'Accessories', 2249.91, 517.4793),  ('CA-2011-154627', '2011-10-29', 'Sue Ann Reed', 'Technology', 'Phones', 2735.952, 341.994),  ('CA-2013-159016', '2013-03-11', 'Karen Ferguson', 'Technology', 'Phones', 4158.912, 363.9048),  ('CA-2012-139731', '2012-10-15', 'Joel Eaton', 'Furniture', 'Chairs', 2453.43, -350.49),  ('CA-2011-168494', '2011-12-12', 'Nora Preis', 'Furniture', 'Tables', 3610.848, 135.4068),  ('CA-2011-160766', '2011-09-14', 'Darrin Martin', 'Technology', 'Machines', 2799.96, 1371.9804),  ('US-2014-168116', '2014-11-05', 'Grant Thornton', 'Technology', 'Machines', 7999.98, -3839.9904),  ('CA-2011-116904', '2011-09-23', 'Sanjit Chand', 'Office Supplies', 'Binders', 9449.95, 4630.4755),  ('US-2012-163825', '2012-06-16', 'Lena Creighton', 'Office Supplies', 'Binders', 3050.376, 1143.891),  ('US-2014-135013', '2014-07-25', 'Harold Ryan', 'Technology', 'Copiers', 2399.96, 839.986),  ('CA-2012-111829', '2012-03-19', 'Fred Hopkins', 'Technology', 'Copiers', 3149.93, 1480.4671),  ('CA-2014-129021', '2014-08-24', 'Patrick Brill', 'Technology', 'Phones', 4367.896, 327.5922),  ('CA-2012-114811', '2012-11-08', 'Keith Dawkins', 'Technology', 'Machines', 4643.8, 2229.024),  ('CA-2013-143805', '2013-12-02', 'Jonathan Doherty', 'Office Supplies', 'Appliances', 2104.55, 694.5015),  ('CA-2012-145352', '2012-03-16', 'Christopher Martinez', 'Office Supplies', 'Binders', 6354.95, 3177.475),  ('CA-2014-138289', '2014-01-17', 'Andy Reiter', 'Office Supplies', 'Binders', 5443.96, 2504.2216),  ('CA-2014-118892', '2014-08-18', 'Tom Prescott', 'Furniture', 'Chairs', 4416.174, -630.882),  ('US-2012-163825', '2012-06-16', 'Lena Creighton', 'Office Supplies', 'Binders', 3050.376, 1143.891),  ('CA-2012-114811', '2012-11-08', 'Keith Dawkins', 'Technology', 'Machines', 4643.8, 2229.024);


-- Q1: List all orders in ascending or descending order of SALES

SELECT * FROM orders
order by sales desc;

-- Q2: List all customers in ascending order of CATEGORY and descending order by SALES

SELECT * FROM orders
order by category, sales desc;

-- Q3: Display only unique records from the order table

SELECT distinct * FROM orders

-- Q4: Display unique combination of CATEGORY and PRODUCT arranged in ASC order.

ORDER by category, product;

SELECT category, product, profit
FROM orders
WHERE profit > 0;

-- Q5: Which orders are giving loss to the company ( where )

SELECT category, product, profit
FROM orders
WHERE profit < 0;


-- Q6: Which are the orders that belong to Technology category? ( where )


SELECT * FROM orders
WHERE category = 'technology';


SELECT category, sum(sales) AS total_sales, AVG(sales) AS average_sales
FROM orders
WHERE profit > 0
GROUP BY category
HAVING AVG(sales) > 3500
ORDER by total_sales DESC;



USE enterprise;

CREATE TABLE departments (
department_id INTEGER Primary Key,
department_name VARCHAR (50),
location VARCHAR (50)
);

INSERT INTO departments (department_id, department_name, location)
VALUES
(1, 'Sales', 'New York'),
(2, 'HR', 'London'),
(3, 'Engineering', 'San Fransisco'),
(4, 'Marketing', 'Chicago'),
(5, 'IT', 'Austin');

SELECT * FROM departments;


CREATE TABLE employees (
employee_id INTEGER Primary KEY AUTO_INCREMENT,
employee_name VARCHAR (50) NOT NULL,
department_id INTEGER NOT NULL,
Foreign Key (department_id)
REFERENCES departments (department_id),
salary INTEGER NOT NULL
);
-- Set starting value for auto incre
ALTER TABLE employees AUTO_INCREMENT = 101;

INSERT INTO employees (employee_name, department_id, salary)
VALUES
('Alice Johnson', 1, 80000),
('Bob Smith', 2, 65000),
('Charlie Brown', 3, 95000),
('David Wilson', 4, 70000),
('Emily Davis', 3, 73000),
('Frank Lee', 2, 85000),
('Grace White', 5, 62000),
('Hannah Green', 4, 75000);

SELECT * FROM employees;


CREATE TABLE projects (
project_id INTEGER Primary KEY AUTO_INCREMENT,
project_name VARCHAR (50) NOT NULL,
department_id INTEGER NOT NULL,
Foreign Key (department_id)
REFERENCES departments (department_id),
budget INTEGER NOT NULL
);

-- Set starting value for auto incre
ALTER TABLE projects AUTO_INCREMENT = 201;

INSERT INTO projects (project_name, department_id, budget)
VALUES
('Project Alpha', 1, 45000),
('Project Beta', 2, 30000),
('Project Gamma', 3, 80000),
('Project Delta', 4, 60000),
('Project Epsilon', 3, 120000),
('FProject Zeta', 1, 70000),
('Project Eta', 4, 50000),
('Project Theta', 5, 95000);


-- Find Employees in the Engineering Department (ID = 3) with Salary Greater than 70,000.

SELECT employees.employee_id, employees.employee_name, employees.salary, departments.department_name
FROM employees
JOIN departments ON employees.department_id = departments.department_id
WHERE departments.department_name = 'engineering' AND employees.salary > 70000;

-- List Projects in Departments 1 or 4 with a Budget Less Than 50,000

SELECT * FROM projects
WHERE department_id IN (1, 4)
AND budget < 50000;

SELECT projects.project_id, projects.project_name, projects.budget, departments.department_name
FROM projects
JOIN departments ON projects.department_id = departments.department_id
WHERE projects.department_id IN (1, 4) AND projects.budget < 50000;


-- Find Employees Not in Department 2

SELECT * FROM employees
WHERE department_id != 2;

-- Find Employees with Salary Between 50,000 and 80,000

SELECT * FROM employees
WHERE salary BETWEEN 50000 AND 80000;

-- List All Projects with Budget Greater Than or Equal to 75,000

SELECT * FROM projects
WHERE budget >= 75000;

-- Find Employees with Salary Not Equal to 90,000

SELECT * FROM employees
WHERE salary != 90000;

-- Retrieve Employees with Names Starting with 'A' and Salary Above 60,000

SELECT * FROM employees
WHERE employee_name LIKE 'A%'
AND salary > 60000;

-- Find Departments with an ID Less Than 3

SELECT * FROM departments
WHERE department_id < 3;

-- List Employees in Either Department 2 or 3 with Salary Greater Than 75,000

SELECT * FROM employees
WHERE department_id = 2 OR department_id = 3
AND salary > 75000;

-- Retrieve Projects with Budget Between 50,000 and 100,000, Not in Department 4

SELECT * FROM projects
WHERE budget BETWEEN 50000 AND 100000
HAVING department_id <> 4;

-- Find Employees in Department 1 Whose Name Does Not Contain 'John'

SELECT * FROM employees
WHERE department_id = 1
AND (employee_name) NOT LIKE '%John%';

-- Retrieve Projects Belonging to Departments 1, 3, or 4 with Budget Greater Than 70,000

SELECT projects.project_name, departments.department_id FROM projects
JOIN departments ON projects.department_id = departments.department_id
WHERE projects.budget > 70000
AND departments.department_id IN (1, 3, 4);


-- Find the Total Salary of Employees in Department 2 and Department 3

SELECT department_id, SUM(salary) AS total_salary
FROM employees
WHERE department_id IN (2, 3)
GROUP BY department_id;

-- Calculate Average Salary of Employees Not in Department 4

SELECT department_id, employee_id, AVG(salary) AS total_salary
FROM employees
WHERE department_id != 4
GROUP BY employee_id;

-- Count Projects with Budgets Either Less Than 30,000 or Greater Than 90,000

SELECT * FROM projects
WHERE budget < 30000 OR budget > 90000;
