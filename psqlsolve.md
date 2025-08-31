# SQL Queries and Examples

This document provides a series of SQL queries and examples based on the provided database schema and questions. Each section includes the query, its purpose, and the expected output. The database includes tables for `employee`, `products`, `customers`, `orders`, and a hypothetical `manager` table.

## Table of Contents
1. [Database Schema](#database-schema)
2. [Queries](#queries)
    - [Question 1: Retrieve all employee names and their salaries](#question-1-retrieve-all-employee-names-and-their-salaries)
    - [Question 2: Find all products in the 'Electronics' category](#question-2-find-all-products-in-the-electronics-category)
    - [Question 3: Get all employees hired after 2019-01-01](#question-3-get-all-employees-hired-after-2019-01-01)
    - [Question 4: List all customers from the USA and Canada](#question-4-list-all-customers-from-the-usa-and-canada)
    - [Question 5: Find products with stock less than 100](#question-5-find-products-with-stock-less-than-100)
    - [Question 6: Get employees with salary between 70000 and 85000](#question-6-get-employees-with-salary-between-70000-and-85000)
    - [Question 7: Find all orders placed in January 2024](#question-7-find-all-orders-placed-in-january-2024)
    - [Question 8: List products ordered by price in descending order](#question-8-list-products-ordered-by-price-in-descending-order)
    - [Question 9: Find the top 3 highest paid employees](#question-9-find-the-top-3-highest-paid-employees)
    - [Question 10: Get unique countries from the customers table](#question-10-get-unique-countries-from-the-customers-table)
    - [Question 11: Count the total number of employees](#question-11-count-the-total-number-of-employees)
    - [Question 12: Find the average price of all products](#question-12-find-the-average-price-of-all-products)
    - [Question 13: Get the maximum and minimum salary](#question-13-get-the-maximum-and-minimum-salary)
    - [Question 14: Calculate the total sales amount](#question-14-calculate-the-total-sales-amount)
    - [Question 15: Count products by category](#question-15-count-products-by-category)
    - [Question 16: Find the average salary by department](#question-16-find-the-average-salary-by-department)
    - [Question 17: Count the number of orders per customer](#question-17-count-the-number-of-orders-per-customer)
    - [Question 18: Find the total inventory value](#question-18-find-the-total-inventory-value)
    - [Question 19: Get the earliest and latest hire dates](#question-19-get-the-earliest-and-latest-hire-dates)
    - [Question 20: Find the average order amount](#question-20-find-the-average-order-amount)
    - [Question 21: List departments with more than 1 employee](#question-21-list-departments-with-more-than-1-employee)
    - [Question 22: Show categories with average price above 200](#question-22-show-categories-with-average-price-above-200)
    - [Question 23: Find customers who have spent more than 500 in total](#question-23-find-customers-who-have-spent-more-than-500-in-total)
    - [Question 24: Show departments where the average salary is above 80000](#question-24-show-departments-where-the-average-salary-is-above-80000)
    - [Question 25: List categories with total stock less than 200](#question-25-list-categories-with-total-stock-less-than-200)
    - [Question 26: Find the month with the highest total sales in 2024](#question-26-find-the-month-with-the-highest-total-sales-in-2024)
    - [Question 27: Show departments with employees hired in different years](#question-27-show-departments-with-employees-hired-in-different-years)
    - [Question 28: Find the category with the highest maximum price](#question-28-find-the-category-with-the-highest-maximum-price)
    - [Question 29: List customers with more than 1 order](#question-29-list-customers-with-more-than-1-order)
    - [Question 30: Find departments where all employees earn more than 60000](#question-30-find-departments-where-all-employees-earn-more-than-60000)
    - [Question 31: Show order details with customer names](#question-31-show-order-details-with-customer-names)
    - [Question 32: Display orders with product names and prices](#question-32-display-orders-with-product-names-and-prices)
    - [Question 33: List employees with their manager names](#question-33-list-employees-with-their-manager-names)
    - [Question 34: Show complete order information with customer and product details](#question-34-show-complete-order-information-with-customer-and-product-details)
    - [Question 35: List all customers and their order count](#question-35-list-all-customers-and-their-order-count)
    - [Question 36: Show products and their total sales quantity](#question-36-show-products-and-their-total-sales-quantity)
    - [Question 37: Find employees who earn more than their department's average salary](#question-37-find-employees-who-earn-more-than-their-departments-average-salary)
    - [Question 38: List customers from USA who have placed orders](#question-38-list-customers-from-usa-who-have-placed-orders)
    - [Question 39: Find products that have never been ordered](#question-39-find-products-that-have-never-been-ordered)
    - [Question 40: Show the salary difference between each employee and the highest paid employee in their department](#question-40-show-the-salary-difference-between-each-employee-and-the-highest-paid-employee-in-their-department)

---

## Database Schema

### Employee Table
```sql
CREATE TABLE employee (
    emp_id INT UNIQUE NOT NULL,
    name VARCHAR(500) NOT NULL,
    department VARCHAR(500) NOT NULL,
    salary INT NOT NULL,
    hire_date DATE NOT NULL,
    manager_id INT
);

INSERT INTO employee (emp_id, name, department, salary, hire_date, manager_id)
VALUES
    (1, 'John Smith', 'IT', 75000, '2020-01-15', 5),
    (2, 'Sarah Johnson', 'HR', 65000, '2019-03-20', 6),
    (3, 'Mike Wilson', 'IT', 80000, '2018-07-10', 5),
    (4, 'Emily Davis', 'Finance', 70000, '2021-02-28', 7),
    (5, 'Robert Brown', 'IT', 95000, '2017-05-15', NULL),
    (6, 'Lisa Garcia', 'HR', 85000, '2016-09-12', NULL),
    (7, 'David Miller', 'Finance', 90000, '2019-11-08', NULL);
```

### Products Table
```sql
CREATE TABLE products (
    product_id INT,
    name VARCHAR(300),
    category VARCHAR(40),
    price NUMERIC(6, 2),
    stock INT
);

ALTER TABLE products
ALTER COLUMN product_id TYPE INT,
ADD CONSTRAINT products_product_id_unique UNIQUE (product_id);

INSERT INTO products (product_id, name, category, price, stock)
VALUES
    (1, 'Laptop', 'Electronics', 999.99, 50),
    (2, 'Mouse', 'Electronics', 25.99, 200),
    (3, 'Chair', 'Furniture', 149.99, 75),
    (4, 'Desk', 'Furniture', 299.99, 30),
    (5, 'Monitor', 'Electronics', 249.99, 100);
```

### Customers Table
```sql
CREATE TABLE customers (
    customer_id SERIAL PRIMARY KEY,
    name VARCHAR(500) NOT NULL,
    email VARCHAR(255) UNIQUE NOT NULL,
    city VARCHAR(50),
    country VARCHAR(50),
    CONSTRAINT email_check CHECK (
        email ~* '^[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Za-z]{2,}$'
    )
);

INSERT INTO customers (customer_id, name, email, city, country)
VALUES
    (1, 'Alice Brown', 'alice@email.com', 'New York', 'USA'),
    (2, 'Bob Green', 'bob@email.com', 'London', 'UK'),
    (3, 'Carol White', 'carol@email.com', 'Toronto', 'Canada'),
    (4, 'David Black', 'david@email.com', 'Sydney', 'Australia'),
    (5, 'Eve Gray', 'eve@email.com', 'Paris', 'France');
```

### Orders Table
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

INSERT INTO orders (order_id, customer_id, product_id, quantity, order_date, total_amount)
VALUES
    (1, 1, 1, 1, '2024-01-15', 999.99),
    (2, 2, 2, 2, '2024-01-16', 51.98),
    (3, 3, 3, 1, '2024-01-17', 149.99),
    (4, 1, 5, 2, '2024-01-18', 499.98),
    (5, 4, 4, 1, '2024-01-19', 299.99);
```

### Manager Table (Hypothetical for Question 33)
```sql
CREATE TABLE manager (
    manager_id INT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    department VARCHAR(50),
    email VARCHAR(100),
    phone VARCHAR(20)
);

ALTER TABLE employee
ADD CONSTRAINT fk_manager
FOREIGN KEY (manager_id)
REFERENCES manager(manager_id);
```

---

## Queries

### Question 1: Retrieve all employee names and their salaries
**Task**: Retrieve all employee names and their salaries from the `employee` table.  
**Expected Output**: List of employee names and their salaries.

```sql
SELECT name, salary AS salaries
FROM employee;
```

### Question 2: Find all products in the 'Electronics' category
**Task**: Find all products in the 'Electronics' category from the `products` table.  
**Expected Output**: List of product names and their prices in the 'Electronics' category.

```sql
SELECT name, price
FROM products
WHERE category = 'Electronics';
```

### Question 3: Get all employees hired after 2019-01-01
**Task**: Retrieve employees hired after January 1, 2019.  
**Expected Output**: List of employee names, hire dates, and departments, ordered by hire date descending.

```sql
SELECT name, hire_date, department
FROM employee
WHERE hire_date > '2019-01-01'
ORDER BY hire_date DESC;
```

### Question 4: List all customers from the USA and Canada
**Task**: List all customers from the USA and Canada.  
**Expected Output**: List of customer names, cities, and countries.

```sql
SELECT name, city, country
FROM customers
WHERE country IN ('USA', 'Canada');
```

### Question 5: Find products with stock less than 100
**Task**: Find products with stock less than 100.  
**Expected Output**: List of product names and their stock quantities.

```sql
SELECT name, stock
FROM products
WHERE stock < 100;
```

### Question 6: Get employees with salary between 70000 and 85000
**Task**: Retrieve employees with salaries between 70,000 and 85,000.  
**Expected Output**: List of employee names and their salaries.

```sql
SELECT name, salary
FROM employee
WHERE salary BETWEEN 70000 AND 85000;
```

### Question 7: Find all orders placed in January 2024
**Task**: Find all orders placed in January 2024.  
**Expected Output**: List of order IDs, customer IDs, order dates, and total amounts.

```sql
SELECT order_id, customer_id, order_date, total_amount
FROM orders
WHERE order_date BETWEEN '2024-01-01' AND '2024-01-31';
```

### Question 8: List products ordered by price in descending order
**Task**: List all products ordered by price in descending order.  
**Expected Output**: List of product names and their prices.

```sql
SELECT name, price
FROM products
ORDER BY price DESC;
```

### Question 9: Find the top 3 highest paid employees
**Task**: Retrieve the top 3 highest paid employees.  
**Expected Output**: List of employee names and their salaries.

```sql
SELECT name, salary
FROM employee
ORDER BY salary DESC
LIMIT 3;
```

### Question 10: Get unique countries from the customers table
**Task**: Retrieve unique countries from the `customers` table.  
**Expected Output**: List of unique countries.

```sql
SELECT DISTINCT country
FROM customers;
```

### Question 11: Count the total number of employees
**Task**: Count the total number of employees in the `employee` table.  
**Expected Output**: Total count of employees.

```sql
SELECT COUNT(*) AS employee_count
FROM employee;
```

### Question 12: Find the average price of all products
**Task**: Calculate the average price of all products.  
**Expected Output**: Average price rounded to 2 decimal places.

```sql
SELECT ROUND(AVG(price), 2) AS avg_price
FROM products;
```

### Question 13: Get the maximum and minimum salary
**Task**: Retrieve the maximum and minimum salaries from the `employee` table.  
**Expected Output**: Maximum and minimum salary values.

```sql
SELECT MAX(salary) AS max_salary, MIN(salary) AS min_salary
FROM employee;
```

### Question 14: Calculate the total sales amount
**Task**: Calculate the total sales amount from the `orders` table.  
**Expected Output**: Sum of total_amount.

```sql
SELECT SUM(total_amount) AS total_sales
FROM orders;
```

### Question 15: Count products by category
**Task**: Count the number of products per category.  
**Expected Output**: List of categories and their product counts, ordered by count descending.

```sql
SELECT category, COUNT(*) AS product_count
FROM products
GROUP BY category
ORDER BY product_count DESC;
```

### Question 16: Find the average salary by department
**Task**: Calculate the average salary by department.  
**Expected Output**: List of departments and their average salaries, rounded to 2 decimal places.

```sql
SELECT department, ROUND(AVG(salary), 2) AS salary_avg
FROM employee
GROUP BY department
ORDER BY salary_avg DESC;
```

### Question 17: Count the number of orders per customer
**Task**: Count the number of orders per customer.  
**Expected Output**: List of customer IDs and their order counts.

```sql
SELECT customer_id, COUNT(*) AS order_count
FROM orders
GROUP BY customer_id
ORDER BY customer_id;
```

### Question 18: Find the total inventory value
**Task**: Calculate the total inventory value (price * stock).  
**Expected Output**: Total inventory value rounded to 2 decimal places.

```sql
SELECT ROUND(SUM(price * stock), 2) AS total_inventory_value
FROM products;
```

### Question 19: Get the earliest and latest hire dates
**Task**: Retrieve the earliest and latest hire dates from the `employee` table.  
**Expected Output**: Earliest and latest hire dates.

```sql
SELECT MIN(hire_date) AS earliest_hire, MAX(hire_date) AS latest_hire
FROM employee;
```

### Question 20: Find the average order amount
**Task**: Calculate the average order amount from the `orders` table.  
**Expected Output**: Average total_amount rounded to 2 decimal places.

```sql
SELECT ROUND(AVG(total_amount), 2) AS avg_order_amount
FROM orders;
```

### Question 21: List departments with more than 1 employee
**Task**: List departments with more than one employee.  
**Expected Output**: List of departments and their employee counts.

```sql
SELECT department, COUNT(*) AS employee_count
FROM employee
GROUP BY department
HAVING COUNT(*) > 1
ORDER BY employee_count;
```

### Question 22: Show categories with average price above 200
**Task**: Show product categories with an average price above 200.  
**Expected Output**: List of categories and their average prices.

```sql
SELECT category, ROUND(AVG(price), 2) AS avg_price
FROM products
GROUP BY category
HAVING AVG(price) > 200
ORDER BY avg_price;
```

### Question 23: Find customers who have spent more than 500 in total
**Task**: Find customers with total spending greater than 500.  
**Expected Output**: List of customer IDs and their total spending.

```sql
SELECT customer_id, SUM(total_amount) AS total_spent
FROM orders
GROUP BY customer_id
HAVING SUM(total_amount) > 500;
```

### Question 24: Show departments where the average salary is above 80000
**Task**: Show departments with an average salary above 80,000.  
**Expected Output**: List of departments and their average salaries.

```sql
SELECT department, ROUND(AVG(salary), 2) AS avg_salary
FROM employee
GROUP BY department
HAVING AVG(salary) > 80000;
```

### Question 25: List categories with total stock less than 200
**Task**: List product categories with total stock less than 200.  
**Expected Output**: List of categories and their total stock.

```sql
SELECT category, SUM(stock) AS total_stock
FROM products
GROUP BY category
HAVING SUM(stock) < 200;
```

### Question 26: Find the month with the highest total sales in 2024
**Task**: Find the month in 2024 with the highest total sales.  
**Expected Output**: Month and total sales amount.

```sql
SELECT EXTRACT(MONTH FROM order_date) AS month, SUM(total_amount) AS total_sales
FROM orders
WHERE EXTRACT(YEAR FROM order_date) = 2024
GROUP BY EXTRACT(MONTH FROM order_date)
HAVING SUM(total_amount) = (
    SELECT MAX(month_total)
    FROM (
        SELECT SUM(total_amount) AS month_total
        FROM orders
        WHERE EXTRACT(YEAR FROM order_date) = 2024
        GROUP BY EXTRACT(MONTH FROM order_date)
    ) AS sub
);
```

### Question 27: Show departments with employees hired in different years
**Task**: Show departments with employees hired in different years.  
**Expected Output**: List of departments and the count of distinct hire years.

```sql
SELECT department, COUNT(DISTINCT EXTRACT(YEAR FROM hire_date)) AS hire_years
FROM employee
GROUP BY department;
```

### Question 28: Find the category with the highest maximum price
**Task**: Find the product category with the highest maximum price.  
**Expected Output**: Category and maximum price.

```sql
SELECT category, MAX(price) AS max_price
FROM products
GROUP BY category
HAVING MAX(price) = (SELECT MAX(price) FROM products);
```

### Question 29: List customers with more than 1 order
**Task**: List customers who have placed more than one order.  
**Expected Output**: List of customer IDs and their order counts.

```sql
SELECT customer_id, COUNT(*) AS order_count
FROM orders
GROUP BY customer_id
HAVING COUNT(*) > 1;
```

### Question 30: Find departments where all employees earn more than 60000
**Task**: Find departments where all employees have a salary greater than 60,000.  
**Expected Output**: List of departments and their minimum salaries.

```sql
SELECT department, MIN(salary) AS min_salary
FROM employee
GROUP BY department
HAVING MIN(salary) > 60000;
```

### Question 31: Show order details with customer names
**Task**: Show order details including customer names.  
**Expected Output**: Order ID, customer name, order date, and total amount.

```sql
SELECT o.order_id, c.name AS customer_name, o.order_date, o.total_amount
FROM orders o
JOIN customers c ON c.customer_id = o.customer_id;
```

### Question 32: Display orders with product names and prices
**Task**: Display orders with product names and prices.  
**Expected Output**: Order ID, product name, quantity, price, and total amount.  
**Note**: The original query had an error (joining on `o.product_id` instead of `o.order_id`). The corrected query is provided.

```sql
SELECT o.order_id, p.name AS product_name, o.quantity, p.price, o.quantity * p.price AS total_amount
FROM orders o
JOIN products p ON p.product_id = o.product_id;
```

### Question 33: List employees with their manager names
**Task**: List employees with their manager names (assumes `manager` table exists).  
**Expected Output**: Employee name and manager name.

```sql
SELECT e.name AS employee_name, m.name AS manager_name
FROM employee e
LEFT JOIN manager m ON m.manager_id = e.manager_id;
```

### Question 34: Show complete order information with customer and product details
**Task**: Show complete order information including customer and product details.  
**Expected Output**: Order ID, customer name, product name, quantity。那么

```sql
SELECT o.order_id AS "Order Id", c.name AS "Customer Name", p.name AS "Product Name", o.quantity AS "Quantity", p.price AS "Unit Price"
FROM orders o
JOIN customers c ON o.customer_id = c.customer_id
JOIN products p ON o.product_id = p.product_id;
```

### Question 35: List all customers and their order count
**Task**: List all customers and their order count, including those with no orders.  
**Expected Output**: Customer ID, customer name, and order count.

```sql
SELECT c.customer_id, c.name AS customer_name, COUNT(o.order_id) AS order_count
FROM customers c
LEFT JOIN orders o ON c.customer_id = o.customer_id
GROUP BY c.customer_id, c.name
ORDER BY c.customer_id;
```

### Question 36: Show products and their total sales quantity
**Task**: Show products and their total sales quantity.  
**Expected Output**: Product ID, product name, and total quantity sold.  
**Note**: Modified to include aggregation for total quantity.

```sql
SELECT p.product_id, p.name AS product_name, SUM(o.quantity) AS total_quantity
FROM products p
LEFT JOIN orders o ON o.product_id = p.product_id
GROUP BY p.product_id, p.name
ORDER BY p.product_id;
```

### Question 37: Find employees who earn more than their department's average salary
**Task**: Find employees who earn more than their department's average salary.  
**Expected Output**: Employee name, salary, and department average salary.

```sql
SELECT e.name, e.salary, ROUND((SELECT AVG(salary) FROM employee WHERE department = e.department), 2) AS dept_avg_salary
FROM employee e
WHERE e.salary > (SELECT AVG(salary) FROM employee WHERE department = e.department)
ORDER BY dept_avg_salary DESC;
```

### Question 38: List customers from USA who have placed orders
**Task**: List customers from the USA who have placed orders.  
**Expected Output**: Customer name, country, and total quantity ordered.

```sql
SELECT c.name, c.country, COUNT(o.quantity) AS total_quantity
FROM customers c
JOIN orders o ON c.customer_id = o.customer_id
WHERE c.country = 'USA'
GROUP BY c.customer_id, c.name, c.country;
```

### Question 39: Find products that have never been ordered
**Task**: Find products that have never been ordered.  
**Expected Output**: Product name and category.  
**Note**: The original query had an error (incorrect join condition). The corrected query uses a LEFT JOIN.

```sql
SELECT p.name AS product_name, p.category AS product_category
FROM products p
LEFT JOIN orders o ON o.product_id = p.product_id
WHERE o.product_id IS NULL;
```

### Question 40: Show the salary difference between each employee and the highest paid employee in their department
**Task**: Show the salary difference between each employee and the highest paid employee in their department.  
**Expected Output**: Employee name, salary, department, and salary difference from the highest paid employee.

```sql
SELECT e.name, e.salary, e.department, (SELECT MAX(salary) FROM employee WHERE department = e.department) - e.salary AS salary_difference
FROM employee e
ORDER BY e.department, salary_difference;
```
