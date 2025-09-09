# SQL Practice Questions & Solutions

This repository contains a comprehensive collection of SQL practice questions with solutions, covering basic to advanced database operations.

## Table of Contents
- [Database Schema](#database-schema)
- [Basic Queries (Questions 1-10)](#basic-queries)
- [Aggregation Functions (Questions 11-20)](#aggregation-functions)
- [GROUP BY and HAVING (Questions 21-30)](#group-by-and-having)
- [JOIN Operations (Questions 31-40)](#join-operations)
- [UPDATE Operations (Questions 41-50)](#update-operations)
- [Advanced Queries (Questions 51-58)](#advanced-queries)

## Database Schema

### Tables Structure

#### Employees Table
```sql
CREATE TABLE employee(
    emp_id int unique not null,
    name varchar(500) not null,
    department varchar(500) not null,
    salary int not null,
    hire_date date not null,
    manager_id int
);
```

#### Products Table
```sql
CREATE TABLE products(
    product_id int,
    name varchar(300),
    category varchar(40),
    price NUMERIC(6, 2),
    stock int
);
```

#### Customers Table
```sql
CREATE TABLE customers (
    customer_id SERIAL PRIMARY KEY,
    name VARCHAR(500) NOT NULL,
    email VARCHAR(255) UNIQUE NOT NULL,
    city VARCHAR(50),
    country VARCHAR(50)
);
```

#### Orders Table
```sql
CREATE TABLE orders (
    order_id INT UNIQUE,
    customer_id INT,
    product_id INT,
    quantity INT,
    order_date DATE,
    total_amount NUMERIC(5,2),
    FOREIGN KEY (customer_id) REFERENCES customers(customer_id),
    FOREIGN KEY (product_id) REFERENCES products(product_id)
);
```

#### Departments Table
```sql
CREATE TABLE departments(
    dept_id int,
    dept_name varchar(200),
    budget int,
    location varchar(200)
);
```

#### Sales Table
```sql
CREATE TABLE sales (
    sale_id INT,
    employee_id INT,
    product_id INT,
    customer_id INT,
    sale_date TIMESTAMP,
    quantity INT,
    unit_price NUMERIC(10,2)
);
```

#### Inventory Movements Table
```sql
CREATE TABLE inventory_movements (
    movement_id INT PRIMARY KEY,
    product_id INT,
    movement_type VARCHAR(10),  -- IN or OUT
    quantity INT,
    movement_date DATE,
    reason VARCHAR(255)
);
```

## Basic Queries

### Question 1: Retrieve Employee Names and Salaries
**Task:** Get all employee names and their salaries
```sql
SELECT name, salary as salaries FROM employee;
```

### Question 2: Find Electronics Products
**Task:** Find all products in the 'Electronics' category
```sql
SELECT name, price FROM products WHERE category='Electronics';
```

### Question 3: Employees Hired After 2019
**Task:** Get all employees hired after 2019-01-01
```sql
SELECT name, hire_date, department
FROM employee
WHERE hire_date > '2019-01-01'
ORDER BY hire_date DESC;
```

### Question 4: Customers from USA and Canada
**Task:** List all customers from the USA and Canada
```sql
SELECT name, city, country
FROM customers
WHERE country IN ('USA', 'Canada');
```

### Question 5: Products with Low Stock
**Task:** Find products with stock less than 100
```sql
SELECT name, stock FROM products WHERE stock < 100;
```

### Question 6: Employees with Salary Range
**Task:** Get employees with salary between 70000 and 85000
```sql
SELECT name, salary FROM employee
WHERE salary BETWEEN 70000 AND 85000;
```

### Question 7: January 2024 Orders
**Task:** Find all orders placed in January 2024
```sql
SELECT order_id, customer_id, order_date, total_amount
FROM orders
WHERE EXTRACT(YEAR FROM order_date) = 2024
  AND EXTRACT(MONTH FROM order_date) = 1;
```

### Question 8: Products Ordered by Price
**Task:** List products ordered by price in descending order
```sql
SELECT name, price FROM products ORDER BY price DESC;
```

### Question 9: Top 3 Highest Paid Employees
**Task:** Find the top 3 highest paid employees
```sql
SELECT name, salary
FROM employee
ORDER BY salary DESC
LIMIT 3;
```

### Question 10: Unique Countries
**Task:** Get unique countries from the customers table
```sql
SELECT DISTINCT(country) FROM customers;
```

## Aggregation Functions

### Question 11: Count Total Employees
```sql
SELECT COUNT(*) FROM employee;
```

### Question 12: Average Product Price
```sql
SELECT ROUND(AVG(price), 2) AS avg_price FROM products;
```

### Question 13: Maximum and Minimum Salary
```sql
SELECT MAX(salary) as max_salary, MIN(salary) as min_salary FROM employee;
```

### Question 14: Total Sales Amount
```sql
SELECT SUM(total_amount) as total_sales FROM orders;
```

### Question 15: Products Count by Category
```sql
SELECT category, COUNT(*) as product_count 
FROM products 
GROUP BY category 
ORDER BY product_count DESC;
```

### Question 16: Average Salary by Department
```sql
SELECT department, ROUND(AVG(salary), 2) as salary_avg 
FROM employee
GROUP BY department
ORDER BY salary_avg DESC;
```

### Question 17: Orders Count per Customer
```sql
SELECT customer_id, COUNT(*) as order_count 
FROM orders 
GROUP BY customer_id 
ORDER BY customer_id;
```

### Question 18: Total Inventory Value
```sql
SELECT ROUND(SUM(price * stock), 2) as total_inventory_value FROM products;
```

### Question 19: Earliest and Latest Hire Dates
```sql
SELECT MIN(hire_date) as earliest_hire, MAX(hire_date) as latest_hire FROM employee;
```

### Question 20: Average Order Amount
```sql
SELECT ROUND(AVG(total_amount), 2) FROM orders;
```

## GROUP BY and HAVING

### Question 21: Departments with More Than 1 Employee
```sql
SELECT department, COUNT(*) as employee_count 
FROM employee 
GROUP BY department 
HAVING COUNT(*) > 1 
ORDER BY employee_count;
```

### Question 22: Categories with Average Price Above 200
```sql
SELECT category, ROUND(AVG(price), 2) as avg_price 
FROM products 
GROUP BY category 
HAVING AVG(price) > 200 
ORDER BY avg_price;
```

### Question 23: Customers Who Spent More Than 500
```sql
SELECT customer_id, SUM(total_amount) 
FROM orders 
GROUP BY customer_id 
HAVING SUM(total_amount) > 500;
```

### Question 24: Departments with Average Salary Above 80000
```sql
SELECT department, ROUND(AVG(salary), 2) as avg_salary 
FROM employee 
GROUP BY department 
HAVING AVG(salary) > 80000;
```

### Question 25: Categories with Total Stock Less Than 200
```sql
SELECT category, SUM(stock) as total_stock 
FROM products 
GROUP BY category 
HAVING SUM(stock) < 200;
```

### Question 26: Month with Highest Sales in 2024
```sql
SELECT 
    EXTRACT(MONTH FROM order_date) as month,
    SUM(total_amount) as total_sales
FROM orders
WHERE EXTRACT(YEAR FROM order_date) = 2024
GROUP BY EXTRACT(MONTH FROM order_date)
HAVING SUM(total_amount) = (
    SELECT MAX(month_total) FROM (
        SELECT SUM(total_amount) as month_total FROM orders
        WHERE EXTRACT(YEAR FROM order_date) = 2024
        GROUP BY EXTRACT(MONTH FROM order_date)
    ) as sub
);
```

### Question 27: Departments with Employees Hired in Different Years
```sql
SELECT department, COUNT(DISTINCT EXTRACT(YEAR FROM hire_date)) AS hire_years 
FROM employee 
GROUP BY department;
```

### Question 28: Category with Highest Maximum Price
```sql
SELECT category, MAX(price) as max_price 
FROM products 
GROUP BY category 
HAVING MAX(price) = (SELECT MAX(price) FROM products);
```

### Question 29: Customers with More Than 1 Order
```sql
SELECT customer_id, COUNT(*) 
FROM orders 
GROUP BY customer_id 
HAVING COUNT(customer_id) > 1;
```

### Question 30: Departments Where All Employees Earn More Than 60000
```sql
SELECT department, MIN(salary) as min_salary 
FROM employee 
GROUP BY department 
HAVING MIN(salary) > 60000;
```

## JOIN Operations

### Question 31: Order Details with Customer Names
```sql
SELECT o.order_id, c.name as customer_name, o.order_date, o.total_amount
FROM orders o
JOIN customers c ON c.customer_id = o.customer_id;
```

### Question 32: Orders with Product Names and Prices
```sql
SELECT o.order_id, p.name as product_name, o.quantity, p.price, o.quantity * p.price as total_amount
FROM orders o
JOIN products p ON p.product_id = o.product_id;
```

### Question 33: Employees with Manager Names
```sql
SELECT e.name as employee_name, m.name as manager_name
FROM employee e
LEFT JOIN manager m ON m.manager_id = e.manager_id;
```

### Question 34: Complete Order Information
```sql
SELECT
    o.order_id as "Order Id",
    c.name as "Customer Name",
    p.name as "Product Name",
    o.quantity as "Quantity",
    p.price as "Unit Price"
FROM orders o
JOIN customers c ON o.customer_id = c.customer_id
JOIN products p ON o.product_id = p.product_id;
```

### Question 35: All Customers and Their Order Count
```sql
SELECT
    c.customer_id as customer_id,
    c.name as customer_name,
    COUNT(o.order_id) AS order_count
FROM customers c
LEFT JOIN orders o ON c.customer_id = o.customer_id
GROUP BY c.customer_id
ORDER BY c.customer_id;
```

### Question 36: Products and Total Sales Quantity
```sql
SELECT
    p.product_id,
    p.name as product_name,
    COALESCE(SUM(o.quantity), 0) as total_quantity
FROM products p
LEFT JOIN orders o ON o.product_id = p.product_id
GROUP BY p.product_id, p.name
ORDER BY total_quantity;
```

### Question 37: Employees Earning More Than Department Average
```sql
SELECT
    e.name,
    e.salary,
    ROUND((SELECT AVG(salary) FROM employee WHERE department = e.department), 2) as dept_avg_salary
FROM employee e
WHERE e.salary > (SELECT AVG(salary) FROM employee WHERE department = e.department)
ORDER BY dept_avg_salary DESC;
```

### Question 38: USA Customers Who Placed Orders
```sql
SELECT
    c.name,
    c.country,
    COUNT(o.quantity) as total_orders
FROM customers c
JOIN orders o ON c.customer_id = o.customer_id
WHERE c.country = 'USA'
GROUP BY c.customer_id, c.name, c.country;
```

### Question 39: Products Never Ordered
```sql
SELECT
    p.name as product_name,
    p.category as product_category
FROM products p
LEFT JOIN orders o ON o.product_id = p.product_id
WHERE o.product_id IS NULL;
```

### Question 40: Salary Difference from Department Maximum
```sql
SELECT 
    e.name,
    e.department,
    e.salary,
    (SELECT MAX(salary) FROM employee WHERE department = e.department) as max_salary,
    ((SELECT MAX(salary) FROM employee WHERE department = e.department) - e.salary) as diff_salary
FROM employee e;
```

## UPDATE Operations

### Question 41: Increase IT Department Salaries by 5%
```sql
UPDATE employee 
SET salary = salary * 1.05 
WHERE department = 'IT';
```

### Question 42: Reduce Laptop Stock by 10 Units
```sql
UPDATE products 
SET stock = stock - 10 
WHERE name = 'Laptop';
```

### Question 43: Update Sarah Johnson's Department
```sql
UPDATE employee
SET department = 'Operations'
WHERE name = 'Sarah Johnson';
```

### Question 44: Apply 10% Discount to Furniture
```sql
UPDATE products
SET price = price * 0.9
WHERE category = 'Furniture';
```

### Question 45: Convert Customer Emails to Lowercase
```sql
UPDATE customers
SET email = LOWER(email);
```

### Question 46: Set Manager for IT Employees Without Manager
```sql
UPDATE employee
SET manager_id = 5
WHERE department = 'IT' AND manager_id IS NULL;
```

### Question 47: Increase Prices for Low Stock Items
```sql
UPDATE products
SET price = price * 1.15
WHERE stock < 50;
```

### Question 48: Add Tax to Orders Over $200
```sql
UPDATE orders
SET total_amount = ROUND(total_amount * 1.10, 2)
WHERE total_amount > 200;
```

### Question 49: Update Hire Date for Employees Without Manager
```sql
UPDATE employee
SET hire_date = CURRENT_DATE
WHERE manager_id IS NULL;
```

### Question 50: Update City for Non-USA Customers
```sql
UPDATE customers
SET city = 'Unknown'
WHERE country != 'USA';
```

## Advanced Queries

### Question 51: Total Sales Amount by Department
```sql
SELECT d.dept_name, SUM(s.quantity * s.unit_price) as total_sales 
FROM sales s
JOIN employee e ON e.emp_id = s.employee_id
JOIN departments d ON d.dept_id = e.department_id
GROUP BY d.dept_name
ORDER BY d.dept_name;
```

### Question 52: Electronics Customers and Their Spending
```sql
SELECT c.name, c.email, SUM(o.quantity * p.price) as total_amount 
FROM orders o
JOIN customers c ON c.customer_id = o.customer_id
JOIN products p ON p.product_id = o.product_id
WHERE p.category = 'Electronics'
GROUP BY c.email, c.name;
```

### Question 53: Employee Sales Value (Including Zero Sales)
```sql
SELECT e.emp_id, e.name, COALESCE(SUM(s.quantity * p.price), 0) as total_sales 
FROM employee e
LEFT JOIN sales s ON s.employee_id = e.emp_id
LEFT JOIN products p ON p.product_id = s.product_id
GROUP BY e.emp_id, e.name
ORDER BY total_sales DESC;
```

### Question 54: Current Stock from Inventory Movements
```sql
SELECT p.name, COALESCE(SUM(
    CASE
        WHEN im.movement_type = 'IN' THEN im.quantity
        WHEN im.movement_type = 'OUT' THEN -im.quantity
        ELSE 0
    END
), 0) as calculated_stock 
FROM products p
LEFT JOIN inventory_movements im ON im.product_id = p.product_id
GROUP BY p.name
ORDER BY calculated_stock DESC;
```

### Question 55: Most Popular Product by Country
```sql
SELECT c.country, p.name as product_name, SUM(o.quantity) as total_quantity
FROM orders o
JOIN products p ON p.product_id = o.product_id
JOIN customers c ON c.customer_id = o.customer_id
GROUP BY c.country, p.name
HAVING SUM(o.quantity) = (
    SELECT MAX(sub.total_quantity)
    FROM (
        SELECT SUM(o2.quantity) as total_quantity
        FROM orders o2
        JOIN customers c2 ON c2.customer_id = o2.customer_id
        WHERE c2.country = c.country 
        GROUP BY o2.product_id
    ) sub
)
ORDER BY c.country;
```

### Question 56: Department Statistics
```sql
SELECT department, COUNT(*) as employee_count, ROUND(AVG(salary), 2) as avg_salary 
FROM employee
GROUP BY department
ORDER BY employee_count;
```

### Question 57: Top Salesperson by Total Sales
```sql
SELECT e.name, COUNT(s.sale_id) as sales_count, SUM(s.quantity * s.unit_price) AS total_sales  
FROM sales s
JOIN employee e ON e.emp_id = s.employee_id
GROUP BY s.employee_id, e.name
ORDER BY total_sales DESC
LIMIT 1;
```

### Question 58: Products Ordered by Multiple Countries
```sql
SELECT p.name as product_name, COUNT(DISTINCT c.country) as country_count
FROM orders o
JOIN products p ON p.product_id = o.product_id
JOIN customers c ON c.customer_id = o.customer_id
GROUP BY p.product_id, p.name
HAVING COUNT(DISTINCT c.country) > 1
ORDER BY country_count DESC;
```

## Key SQL Concepts Covered

- **Basic Queries**: SELECT, WHERE, ORDER BY, LIMIT
- **Aggregation**: COUNT, SUM, AVG, MAX, MIN
- **Grouping**: GROUP BY, HAVING
- **Joins**: INNER JOIN, LEFT JOIN, RIGHT JOIN, FULL OUTER JOIN
- **Subqueries**: Correlated and non-correlated subqueries
- **Window Functions**: Advanced analytical queries
- **Data Manipulation**: UPDATE, INSERT, DELETE
- **Data Types**: Handling dates, numeric data, strings
- **Constraints**: Foreign keys, unique constraints, check constraints

## Practice Tips

1. **Start with Basic Queries**: Master SELECT statements before moving to complex joins
2. **Understand Data Relationships**: Study the table schemas and relationships
3. **Practice Aggregations**: Learn when to use GROUP BY vs simple aggregation
4. **Master Joins**: Understand different join types and when to use each
5. **Use Subqueries Wisely**: Know when a subquery is more efficient than a join
6. **Optimize Queries**: Consider indexing and query performance
7. **Test Edge Cases**: Consider NULL values and empty result sets

---

*This collection covers fundamental to advanced SQL concepts. Practice each question multiple times with different datasets to master SQL querying skills.*
