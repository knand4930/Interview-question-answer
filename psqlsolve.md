-- CREATE TABLE author.employee(
-- 	emp_id serial,
-- 	salary int,
-- 	designation varchar(500)
-- );

-- INSERT INTO employee (salary, designation)
-- VALUES
--     (70000, 'react Developer'),
--     (40000, 'flutter Developer');

-- SELECT MAX(salary) AS second_salary
-- FROM employee
-- WHERE salary < (SELECT MAX(salary) FROM employee);

-- SELECT salary AS second_salary
-- FROM employee
-- WHERE salary < (SELECT MAX(salary) FROM employee)
--  order by second_salary desc;


-- SELECT max(salary) AS second_salary, designation as employee_designation
-- FROM employee
-- WHERE salary < (SELECT MAX(salary) FROM employee)
--  order by second_salary desc;


-- SELECT salary as second_salary, designation as employee_designation
-- FROM employee where salary = (SELECT MAX(salary) from employee where salary <(SELECT MAX(salary) from employee))

-- DROP TABLE employee;

-- SQl Question Solve

-- CREATE TABLE employee(
-- 	emp_id int unique not null,
-- 	name varchar(500) not null,
-- 	department varchar(500) not null,
-- 	salary int not null,
-- 	hire_date date not null,
-- 	manager_id int
-- )


-- INSERT INTO employee(emp_id, name, department, salary, hire_date, manager_id)
-- VALUES
-- (1, 'John Smith', 'IT', 75000, '2020-01-15', 5),
-- (2, 'Sarah Johnson', 'HR', 65000, '2019-03-20', 6),
-- (3, 'Mike Wilson', 'IT', 80000, '2018-07-10', 5),
-- (4, 'Emily Davis', 'Finance', 70000, '2021-02-28', 7),
-- (5, 'Robert Brown', 'IT', 95000, '2017-05-15', NULL),
-- (6, 'Lisa Garcia', 'HR', 85000, '2016-09-12', NULL),
-- (7, 'David Miller', 'Finance', 90000, '2019-11-08', NULL);


-- CREATE TABLE products(
-- 	product_id int,
-- 	name varchar(300),
-- 	category varchar(40),
-- 	price NUMERIC(6, 2),
-- 	stock int
-- );

-- ALTER TABLE products
-- ALTER COLUMN product_id TYPE INT,
-- ADD CONSTRAINT products_product_id_unique UNIQUE (product_id);


-- INSERT INTO products (product_id, name, category, price, stock)
-- VALUES
-- (1, 'Laptop', 'Electronics', 999.99, 50),
-- (2, 'Mouse', 'Electronics', 25.99, 200),
-- (3, 'Chair', 'Furniture', 149.99, 75),
-- (4, 'Desk', 'Furniture', 299.99, 30),
-- (5, 'Monitor', 'Electronics', 249.99, 100);


-- CREATE TABLE customers (
--     customer_id SERIAL PRIMARY KEY,
--     name VARCHAR(500) NOT NULL,
--     email VARCHAR(255) UNIQUE NOT NULL,
--     city VARCHAR(50),
--     country VARCHAR(50),
--     CONSTRAINT email_check CHECK (
--         email ~* '^[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Za-z]{2,}$'
--     )
-- )


-- insert into customers(customer_id,name,email,city,country)
-- VALUES
-- (1,	'Alice Brown',	'alice@email.com',	'New York',	'USA'),
-- (2,	'Bob Green',	'bob@email.com',	'London',	'UK'),
-- (3,	'Carol White','carol@email.com','Toronto',	'Canada'),
-- (4,	'David Black',	'david@email.com',	'Sydney',	'Australia'),
-- (5,	'Eve Gray',	'eve@email.com',	'Paris',	'France');

-- CREATE TABLE orders (
--     order_id INT UNIQUE,
--     customer_id INT,
--     product_id INT,
--     quantity INT,
--     order_date DATE,
--     total_amount NUMERIC(5,2),
--     FOREIGN KEY (customer_id) REFERENCES customers(customer_id),
--     FOREIGN KEY (product_id) REFERENCES products(product_id)
-- );


-- insert into orders(order_id,customer_id,product_id,quantity,order_date,total_amount)
-- VALUES
-- (1,	1,	1,	1,	'2024-01-15',	999.99),
-- (2,	2,	2,	2,	'2024-01-16',	51.98),
-- (3,	3,	3,	1,	'2024-01-17',	149.99),
-- (4,	1, 5,	2,	'2024-01-18',	499.98),
-- (5,	4,	4,	1,	'2024-01-19',	299.99);

-- Question 1 Tables: employees Task: Retrieve all employee names and their salaries. Expected Output:
-- SELECT name , salary as salaries from employee;

-- Question 2 Tables: products Task: Find all products in the 'Electronics' category. Expected Output:
-- select name , price from products where category='Electronics';

-- Question 3 Tables: employees Task: Get all employees hired after 2019-01-01. Expected Output:
-- SELECT name, hire_date, department
-- FROM employee
-- WHERE hire_date > '2019-01-01'
-- ORDER BY hire_date DESC;

-- Question 4 Tables: customers Task: List all customers from the USA and Canada. Expected Output:
-- SELECT name, city, country from customers
-- where country = 'USA' or country ='Canada';

-- SELECT name, city, country
-- FROM customers
-- WHERE country IN ('USA', 'Canada');


-- Question 5 Tables: products Task: Find products with stock less than 100. Expected Output:
-- select name, stock from products where stock<100;

-- Question 6 Tables: employees Task: Get employees with salary between 70000 and 85000. Expected Output:
-- select name, salary from employee
-- where
-- salary between 70000 and 85000
-- ;


-- Question 7 Tables: orders Task: Find all orders placed in January 2024. Expected Output:
-- select order_id, customer_id, order_date, total_amount from orders
-- where
-- order_date
-- between '01-01-2024' and '31-01-2024'
-- SELECT order_id, customer_id, order_date, total_amount
-- FROM orders
-- WHERE order_date >= '2024-01-01'
--   AND order_date < '2024-02-01';
-- SELECT order_id, customer_id, order_date, total_amount
-- FROM orders
-- WHERE EXTRACT(YEAR FROM order_date) = 2024
--   AND EXTRACT(MONTH FROM order_date) = 1;


-- Question 8 Tables: products Task: List products ordered by price in descending order. Expected Output:
-- select name , price from products order by price desc;


-- Question 9 Tables: employees Task: Find the top 3 highest paid employees. Expected Output:
-- select name, salary from employee where salary<(select max(salary) from employee) order by salary desc limit 3;
-- SELECT name, salary
-- FROM employee
-- ORDER BY salary DESC
-- LIMIT 3;

-- SELECT name, salary
-- FROM employee
-- ORDER BY salary DESC
-- OFFSET 4 LIMIT 3;

-- -- Question 10 Tables: customers Task: Get unique countries from the customers table. Expected Output:
-- select distinct(country) from customers;


-- Question 11 Tables: employees Task: Count the total number of employees. Expected Output:
-- select count(*) from employee;

-- Question 12 Tables: products Task: Find the average price of all products. Expected Output:
-- SELECT ROUND(AVG(price), 2) AS avg_price
-- FROM products;


-- Question 13 Tables: employees Task: Get the maximum and minimum salary. Expected Output:
-- select max(salary) as max_salary ,min(salary) as min_salary from employee;

-- Question 14 Tables: orders Task: Calculate the total sales amount. Expected Output:
-- select sum(total_amount) as total_sales from orders;

-- Question 15 Tables: products Task: Count products; by category. Expected Output:
-- select category, count(*) as product_count from products group by category order by product_count desc


-- Question 16 Tables: employees Task: Find the average salary by department. Expected Output:
-- select department , ROUND(avg(salary), 2) as salary_avg from employee
-- group by department
-- ORDER BY salary_avg desc;

-- Question 17 Tables: orders Task: Count the number of orders per customer. Expected Output:
-- select customer_id , count(*) as order_count from orders group by customer_id order by customer_id;

-- Question 18 Tables: products Task: Find the total inventory value (price * stock). Expected Output:
-- select ROUND(sum(price * stock ), 2) as total_inventory_value from (select price , stock from products order by product_id limit 3)t;
-- select round(sum(price*stock) , 2) as total_inventory_value from products;

-- Question 19 Tables: employees Task: Get the earliest and latest hire dates. Expected Output:
-- select min(hire_date) as earliest_hire, max(hire_date) as latest_hire from employee;

-- Question 20 Tables: orders Task: Find the average order amount. Expected Output:
-- select round(avg(total_amount), 2) from orders;

-- Question 21 Tables: employees Task: List departments with more than 1 employee. Expected Output:
-- select department, count(*) as employee_count from employee group by department having count(*) >1 order by employee_count;

-- Question 22 Tables: products Task: Show categories with average price above 200. Expected Output:
-- select category, round(avg(stock * price) ,2)as avg_price from products group by category having avg(stock * price) >200;
-- select category, round(avg(price) ,2)as avg_price from products group by category having avg(price) >200 order by avg_price;

-- Question 23 Tables: orders Task: Find customers who have spent more than 500 in total. Expected Output:
-- select customer_id, sum(total_amount) from orders group by customer_id having sum(total_amount) > 500;

-- Question 24 Tables: employees Task: Show departments where the average salary is above 80000. Expected Output:
-- select department, round(avg(salary),2) as avg_salary from employee group by department having avg(salary)>80000;

-- Question 25 Tables: products Task: List categories with total stock less than 200. Expected Output:
-- select category, sum(stock) as avg_stack from products group by category having sum(stock)<200;

-- Question 26 Tables: orders Task: Find the month with the highest total sales in 2024. Expected Output:
-- select extract(month from order_date), sum(total_amount) as max_sales from orders where extract(year from order_date)=2024 group by extract(month from order_date);

-- select
-- extract(month from order_date) as month,
-- sum(total_amount) as total_sales
-- from orders
-- where extract(year from order_date)=2024
-- group by extract(month from order_date)
-- having sum(total_amount)=
-- (
-- select max(month_total) from (
-- 	select sum(total_amount) as month_total from orders
-- where
-- extract(year from order_date)=2024
-- group by extract(month from order_date)
-- ) as sub
-- );

-- Question 27 Tables: employees Task: Show departments with employees hired in different years. Expected Output:
-- select department, count(*) as hire_years from employee group by department;
-- select department, COUNT(DISTINCT EXTRACT(YEAR FROM hire_date)) AS hire_years from employee group by department;
-- select department , count(distinct extract(year from hire_date)) as hire_years from employee group by department having count(distinct extract(year from hire_date)) =1;


-- Question 28 Tables: products Task: Find the category with the highest maximum price. Expected Output:
-- select category, max(price) as max_price from products group by category having max(price)=(
-- select max(price) from products
-- );

-- Question 29 Tables: orders Task: List customers with more than 1 order. Expected Output:
-- select customer_id , count(*) from orders group by customer_id having count(customer_id) > 1;

-- Question 30 Tables: employees Task: Find departments where all employees earn more than 60000. Expected Output:
-- select department , min(salary) as min_salary from employee group by department having min(salary) > 60000;


-- Question 31 Tables: orders, customers Task: Show order details with customer names. Expected Output:
-- select o.order_id, c.name as customer_name, o.order_date, o.total_amount
-- from orders o
-- join customers c
-- on c.customer_id=o.customer_id

-- Question 32 Tables: orders, products Task: Display orders with product names and prices. Expected Output:
-- select o.order_id, p.name as product_name, o.quantity , p.price , o.quantity*p.price as total_amount
-- from orders o
-- join products p
-- on p.product_id=o.order_id;

-- Question 33 Tables: employees, departments (assume manager_id references emp_id) Task: List employees with their manager names. Expected Output:
-- CREATE TABLE manager (
--     manager_id INT PRIMARY KEY,  -- will match employee emp_id
--     name VARCHAR(100) NOT NULL,
--     department VARCHAR(50),
--     email VARCHAR(100),
--     phone VARCHAR(20)
-- );

-- ALTER TABLE employee
-- ADD CONSTRAINT fk_manager
-- FOREIGN KEY (manager_id)
-- REFERENCES manager(manager_id);

-- select e.name as employee_name, m.name as manager_name
-- from employee e
-- left join manager m
-- on m.manager_id=e.manager_id;

-- select e.name as employee_name, m.name as manager_name
-- from manager m
-- right join employee e
-- on m.manager_id=e.manager_id;

-- Question 34 Tables: orders, customers, products Task: Show complete order information with customer and product details. Expected Output:
-- select
-- o.order_id as "Order Id",
-- c.name as "Customer Name",
-- p.name as "Product Name",
-- o.quantity as "Quantity",
-- p.price as "Unit Price"
-- from orders o
-- join customers c on o.customer_id=c.customer_id
-- join products p on o.product_id = p.product_id;


-- Question 35 Tables: customers, orders Task: List all customers and their order count (including customers with no orders). Expected Output:
-- select
-- c.customer_id as customer_id,
-- c.name as customer_name,
-- COUNT(o.order_id) AS order_count

-- from customers c
-- left join orders o on c.customer_id=o.customer_id
-- group by c.customer_id
-- order by c.customer_id;

-- Question 36 Tables: products, orders Task: Show products and their total sales quantity. Expected Output:
-- select
-- p.product_id,
-- p.name as product_name,
-- o.quantity
-- from products p
-- FULL OUTER join orders o on o.product_id=p.product_id
-- order by o.quantity;


-- Question 37 Tables: employees Task: Find employees who earn more than their department's average salary. Expected Output:
-- SELECT
-- 	e.name,
-- 	e.salary,
-- 	round((select AVG(salary) from employee where department =e.department),2) as dept_avg_salary
-- FROM employee e
-- where e.salary >(select avg(salary) from employee where department=e.department)
-- order by dept_avg_salary desc;

-- Question 38 Tables: customers, orders Task: List customers from USA who have placed orders. Expected Output:
-- select
-- c.name,
-- c.country,
-- count(o.quantity) as total_quantity
-- from
-- customers c
-- join orders o on c.customer_id=o.customer_id
-- where c.country='USA'
-- GROUP BY c.customer_id, c.name, c.country;

-- Question 39 Tables: products, orders Task: Find products that have never been ordered. Expected Output:
-- select
-- p.name as product_name,
-- p.category as product_category
-- from products p
-- join orders o on o.product_id=p.product_id
-- where o.product_id is null
-- ;

-- Question 40 Tables: employees Task: Show the salary difference between each employee and the highest paid employee in their department. Expected Output:
--select * from employee;





