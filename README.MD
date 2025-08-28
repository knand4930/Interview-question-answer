# 100+ PostgreSQL Interview Questions with SQL Queries (5+ Years Experience)

## 1. Advanced SELECT Queries

### Q1: Find the second highest salary from employees table
```sql
SELECT MAX(salary) as second_highest_salary
FROM employees 
WHERE salary < (SELECT MAX(salary) FROM employees);

-- Alternative using LIMIT and OFFSET
SELECT DISTINCT salary 
FROM employees 
ORDER BY salary DESC 
LIMIT 1 OFFSET 1;
```

### Q2: Find employees with salary higher than their department average
```sql
SELECT e.name, e.salary, e.department_id
FROM employees e
WHERE e.salary > (
    SELECT AVG(salary) 
    FROM employees e2 
    WHERE e2.department_id = e.department_id
);
```

### Q3: Find departments with more than 5 employees
```sql
SELECT d.department_name, COUNT(e.employee_id) as employee_count
FROM departments d
JOIN employees e ON d.department_id = e.department_id
GROUP BY d.department_id, d.department_name
HAVING COUNT(e.employee_id) > 5;
```

### Q4: Find employees who joined in the last 3 months
```sql
SELECT name, hire_date
FROM employees
WHERE hire_date >= CURRENT_DATE - INTERVAL '3 months';
```

### Q5: Find duplicate email addresses
```sql
SELECT email, COUNT(*) as count
FROM employees
GROUP BY email
HAVING COUNT(*) > 1;
```

## 2. Window Functions

### Q6: Rank employees by salary within each department
```sql
SELECT 
    name, 
    department_id, 
    salary,
    RANK() OVER (PARTITION BY department_id ORDER BY salary DESC) as rank
FROM employees;
```

### Q7: Calculate running total of sales
```sql
SELECT 
    sale_date,
    amount,
    SUM(amount) OVER (ORDER BY sale_date) as running_total
FROM sales
ORDER BY sale_date;
```

### Q8: Find the difference between current and previous salary
```sql
SELECT 
    employee_id,
    salary_date,
    salary,
    LAG(salary) OVER (PARTITION BY employee_id ORDER BY salary_date) as previous_salary,
    salary - LAG(salary) OVER (PARTITION BY employee_id ORDER BY salary_date) as salary_increase
FROM salary_history;
```

### Q9: Calculate moving average of last 3 orders
```sql
SELECT 
    order_date,
    amount,
    AVG(amount) OVER (ORDER BY order_date ROWS 2 PRECEDING) as moving_avg
FROM orders;
```

### Q10: Find top 3 highest paid employees per department
```sql
SELECT *
FROM (
    SELECT 
        name, 
        department_id, 
        salary,
        ROW_NUMBER() OVER (PARTITION BY department_id ORDER BY salary DESC) as rn
    FROM employees
) ranked
WHERE rn <= 3;
```

## 3. Common Table Expressions (CTEs)

### Q11: Recursive CTE to find employee hierarchy
```sql
WITH RECURSIVE employee_hierarchy AS (
    -- Base case: managers (employees with no boss)
    SELECT employee_id, name, manager_id, 1 as level
    FROM employees
    WHERE manager_id IS NULL
    
    UNION ALL
    
    -- Recursive case: employees reporting to someone
    SELECT e.employee_id, e.name, e.manager_id, eh.level + 1
    FROM employees e
    JOIN employee_hierarchy eh ON e.manager_id = eh.employee_id
)
SELECT * FROM employee_hierarchy ORDER BY level, name;
```

### Q12: Find all subordinates of a specific manager
```sql
WITH RECURSIVE subordinates AS (
    SELECT employee_id, name, manager_id
    FROM employees
    WHERE employee_id = 100  -- specific manager ID
    
    UNION ALL
    
    SELECT e.employee_id, e.name, e.manager_id
    FROM employees e
    JOIN subordinates s ON e.manager_id = s.employee_id
)
SELECT * FROM subordinates WHERE employee_id != 100;
```

### Q13: Calculate cumulative sales by month
```sql
WITH monthly_sales AS (
    SELECT 
        DATE_TRUNC('month', order_date) as month,
        SUM(amount) as monthly_total
    FROM orders
    GROUP BY DATE_TRUNC('month', order_date)
)
SELECT 
    month,
    monthly_total,
    SUM(monthly_total) OVER (ORDER BY month) as cumulative_total
FROM monthly_sales;
```

## 4. Advanced JOINs

### Q14: Find employees who never made a sale
```sql
SELECT e.name
FROM employees e
LEFT JOIN sales s ON e.employee_id = s.employee_id
WHERE s.employee_id IS NULL;
```

### Q15: Self-join to find employees with same salary
```sql
SELECT DISTINCT e1.name, e2.name, e1.salary
FROM employees e1
JOIN employees e2 ON e1.salary = e2.salary 
    AND e1.employee_id < e2.employee_id;
```

### Q16: Multiple table join with aggregation
```sql
SELECT 
    d.department_name,
    COUNT(DISTINCT e.employee_id) as employee_count,
    COUNT(DISTINCT p.project_id) as project_count,
    AVG(e.salary) as avg_salary
FROM departments d
LEFT JOIN employees e ON d.department_id = e.department_id
LEFT JOIN employee_projects ep ON e.employee_id = ep.employee_id
LEFT JOIN projects p ON ep.project_id = p.project_id
GROUP BY d.department_id, d.department_name;
```

## 5. Subqueries and Correlated Subqueries

### Q17: Find employees earning more than average in their department
```sql
SELECT name, salary, department_id
FROM employees e1
WHERE salary > (
    SELECT AVG(salary)
    FROM employees e2
    WHERE e2.department_id = e1.department_id
);
```

### Q18: Find customers with orders above their average order value
```sql
SELECT DISTINCT c.customer_name
FROM customers c
JOIN orders o ON c.customer_id = o.customer_id
WHERE o.amount > (
    SELECT AVG(amount)
    FROM orders o2
    WHERE o2.customer_id = c.customer_id
);
```

### Q19: Find products that were never ordered
```sql
SELECT product_name
FROM products p
WHERE NOT EXISTS (
    SELECT 1
    FROM order_items oi
    WHERE oi.product_id = p.product_id
);
```

## 6. Date and Time Functions

### Q20: Calculate age in years
```sql
SELECT 
    name,
    birth_date,
    EXTRACT(YEAR FROM AGE(CURRENT_DATE, birth_date)) as age
FROM employees;
```

### Q21: Find orders placed on weekends
```sql
SELECT *
FROM orders
WHERE EXTRACT(DOW FROM order_date) IN (0, 6);  -- 0=Sunday, 6=Saturday
```

### Q22: Group sales by quarter
```sql
SELECT 
    EXTRACT(YEAR FROM sale_date) as year,
    EXTRACT(QUARTER FROM sale_date) as quarter,
    SUM(amount) as total_sales
FROM sales
GROUP BY EXTRACT(YEAR FROM sale_date), EXTRACT(QUARTER FROM sale_date)
ORDER BY year, quarter;
```

### Q23: Find business days between two dates
```sql
SELECT 
    order_id,
    order_date,
    delivery_date,
    (EXTRACT(DOW FROM generate_series(order_date, delivery_date, '1 day'::interval))
     NOT IN (0, 6))::int as business_days
FROM orders;

-- Alternative approach
SELECT 
    order_id,
    (delivery_date - order_date) - 
    (EXTRACT(week FROM delivery_date) - EXTRACT(week FROM order_date)) * 2 as business_days
FROM orders;
```

## 7. String Functions and Pattern Matching

### Q24: Find employees with names starting with vowels
```sql
SELECT name
FROM employees
WHERE name ~ '^[AEIOUaeiou]';
```

### Q25: Extract domain from email addresses
```sql
SELECT 
    email,
    SUBSTRING(email FROM '@(.*)$') as domain
FROM employees;

-- Alternative
SELECT 
    email,
    SPLIT_PART(email, '@', 2) as domain
FROM employees;
```

### Q26: Format phone numbers
```sql
SELECT 
    phone,
    CASE 
        WHEN LENGTH(REGEXP_REPLACE(phone, '[^0-9]', '', 'g')) = 10 THEN
            SUBSTRING(phone, 1, 3) || '-' || SUBSTRING(phone, 4, 3) || '-' || SUBSTRING(phone, 7, 4)
        ELSE phone
    END as formatted_phone
FROM employees;
```

## 8. JSON Operations

### Q27: Query JSON data
```sql
-- Assuming a table with JSON column
SELECT 
    id,
    data->>'name' as name,
    data->>'age' as age,
    data->'address'->>'city' as city
FROM user_profiles
WHERE (data->>'age')::int > 25;
```

### Q28: Aggregate JSON array elements
```sql
SELECT 
    id,
    JSON_ARRAY_LENGTH(skills) as skill_count,
    JSON_ARRAY_ELEMENTS_TEXT(skills) as individual_skills
FROM employee_skills;
```

### Q29: Update JSON data
```sql
UPDATE user_profiles 
SET data = data || '{"last_login": "2024-01-15"}'::jsonb
WHERE id = 1;
```

## 9. Array Operations

### Q30: Work with PostgreSQL arrays
```sql
-- Create and query arrays
SELECT 
    name,
    skills,
    ARRAY_LENGTH(skills, 1) as skill_count,
    'PostgreSQL' = ANY(skills) as knows_postgresql
FROM employees
WHERE skills && ARRAY['SQL', 'Python'];  -- Overlap operator
```

### Q31: Unnest arrays
```sql
SELECT 
    name,
    UNNEST(skills) as individual_skill
FROM employees;
```

## 10. Performance and Indexing

### Q32: Analyze query performance
```sql
EXPLAIN (ANALYZE, BUFFERS, FORMAT JSON)
SELECT *
FROM employees e
JOIN departments d ON e.department_id = d.department_id
WHERE e.salary > 50000;
```

### Q33: Create partial index
```sql
CREATE INDEX idx_employees_high_salary 
ON employees(salary) 
WHERE salary > 100000;
```

### Q34: Create composite index
```sql
CREATE INDEX idx_employees_dept_salary 
ON employees(department_id, salary DESC);
```

## 11. Advanced Aggregations

### Q35: Calculate median salary
```sql
SELECT 
    department_id,
    PERCENTILE_CONT(0.5) WITHIN GROUP (ORDER BY salary) as median_salary
FROM employees
GROUP BY department_id;
```

### Q36: Calculate mode (most frequent value)
```sql
SELECT 
    department_id,
    MODE() WITHIN GROUP (ORDER BY job_title) as most_common_job
FROM employees
GROUP BY department_id;
```

### Q37: String aggregation
```sql
SELECT 
    department_id,
    STRING_AGG(name, ', ' ORDER BY name) as employee_list
FROM employees
GROUP BY department_id;
```

### Q38: Conditional aggregation
```sql
SELECT 
    department_id,
    COUNT(*) as total_employees,
    COUNT(*) FILTER (WHERE salary > 50000) as high_earners,
    AVG(salary) FILTER (WHERE hire_date > '2020-01-01') as avg_salary_new_hires
FROM employees
GROUP BY department_id;
```

## 12. Data Modification

### Q39: Update with JOIN
```sql
UPDATE employees
SET salary = salary * 1.1
FROM departments d
WHERE employees.department_id = d.department_id
    AND d.department_name = 'Engineering';
```

### Q40: Insert with conflict resolution (UPSERT)
```sql
INSERT INTO employee_stats (employee_id, login_count, last_login)
VALUES (1, 1, CURRENT_TIMESTAMP)
ON CONFLICT (employee_id)
DO UPDATE SET 
    login_count = employee_stats.login_count + 1,
    last_login = CURRENT_TIMESTAMP;
```

### Q41: Delete with EXISTS
```sql
DELETE FROM customers c
WHERE NOT EXISTS (
    SELECT 1 FROM orders o 
    WHERE o.customer_id = c.customer_id
);
```

### Q42: Bulk insert with COPY
```sql
COPY employees(name, email, department_id, salary)
FROM '/path/to/employees.csv'
WITH (FORMAT CSV, HEADER true);
```

## 13. Data Types and Constraints

### Q43: Working with ENUM types
```sql
-- Create ENUM type
CREATE TYPE status_type AS ENUM ('active', 'inactive', 'pending');

-- Use in table
CREATE TABLE orders (
    id SERIAL PRIMARY KEY,
    status status_type DEFAULT 'pending'
);

-- Query with ENUM
SELECT * FROM orders WHERE status = 'active';
```

### Q44: Working with ranges
```sql
-- Using date ranges
SELECT *
FROM bookings
WHERE booking_period && '[2024-01-01, 2024-01-31)'::daterange;
```

### Q45: Custom constraints
```sql
ALTER TABLE employees
ADD CONSTRAINT check_salary_positive 
CHECK (salary > 0);

ALTER TABLE employees
ADD CONSTRAINT check_email_format
CHECK (email ~* '^[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Za-z]{2,}$');
```

## 14. Advanced Functions and Procedures

### Q46: Create a custom function
```sql
CREATE OR REPLACE FUNCTION calculate_bonus(emp_id INTEGER)
RETURNS DECIMAL AS $$
DECLARE
    emp_salary DECIMAL;
    years_service INTEGER;
    bonus_amount DECIMAL;
BEGIN
    SELECT salary, EXTRACT(YEAR FROM AGE(CURRENT_DATE, hire_date))
    INTO emp_salary, years_service
    FROM employees
    WHERE employee_id = emp_id;
    
    bonus_amount := emp_salary * 0.1 * years_service;
    
    RETURN bonus_amount;
END;
$$ LANGUAGE plpgsql;

-- Use the function
SELECT name, calculate_bonus(employee_id) as bonus
FROM employees;
```

### Q47: Create a stored procedure
```sql
CREATE OR REPLACE PROCEDURE promote_employee(
    emp_id INTEGER,
    new_title VARCHAR,
    salary_increase DECIMAL
)
LANGUAGE plpgsql AS $$
BEGIN
    UPDATE employees
    SET job_title = new_title,
        salary = salary + salary_increase,
        last_promotion_date = CURRENT_DATE
    WHERE employee_id = emp_id;
    
    INSERT INTO promotion_history (employee_id, old_title, new_title, promotion_date)
    SELECT employee_id, job_title, new_title, CURRENT_DATE
    FROM employees
    WHERE employee_id = emp_id;
    
    COMMIT;
END;
$$;
```

## 15. Triggers

### Q48: Create an audit trigger
```sql
-- Audit table
CREATE TABLE employee_audit (
    audit_id SERIAL PRIMARY KEY,
    employee_id INTEGER,
    operation CHAR(1),
    old_values JSONB,
    new_values JSONB,
    changed_by VARCHAR(100),
    changed_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Trigger function
CREATE OR REPLACE FUNCTION employee_audit_trigger()
RETURNS TRIGGER AS $$
BEGIN
    IF TG_OP = 'DELETE' THEN
        INSERT INTO employee_audit(employee_id, operation, old_values, changed_by)
        VALUES (OLD.employee_id, 'D', row_to_json(OLD), user);
        RETURN OLD;
    ELSIF TG_OP = 'UPDATE' THEN
        INSERT INTO employee_audit(employee_id, operation, old_values, new_values, changed_by)
        VALUES (NEW.employee_id, 'U', row_to_json(OLD), row_to_json(NEW), user);
        RETURN NEW;
    ELSIF TG_OP = 'INSERT' THEN
        INSERT INTO employee_audit(employee_id, operation, new_values, changed_by)
        VALUES (NEW.employee_id, 'I', row_to_json(NEW), user);
        RETURN NEW;
    END IF;
END;
$$ LANGUAGE plpgsql;

-- Create trigger
CREATE TRIGGER employee_audit_trigger
    AFTER INSERT OR UPDATE OR DELETE ON employees
    FOR EACH ROW EXECUTE FUNCTION employee_audit_trigger();
```

## 16. Partitioning

### Q49: Create partitioned table
```sql
-- Parent table
CREATE TABLE sales_data (
    id SERIAL,
    sale_date DATE,
    amount DECIMAL,
    customer_id INTEGER
) PARTITION BY RANGE (sale_date);

-- Partitions
CREATE TABLE sales_2023 PARTITION OF sales_data
    FOR VALUES FROM ('2023-01-01') TO ('2024-01-01');

CREATE TABLE sales_2024 PARTITION OF sales_data
    FOR VALUES FROM ('2024-01-01') TO ('2025-01-01');

-- Query will automatically use appropriate partition
SELECT * FROM sales_data WHERE sale_date BETWEEN '2024-01-01' AND '2024-12-31';
```

## 17. Full Text Search

### Q50: Implement full-text search
```sql
-- Add tsvector column
ALTER TABLE articles ADD COLUMN search_vector tsvector;

-- Update search vector
UPDATE articles 
SET search_vector = to_tsvector('english', title || ' ' || content);

-- Create index
CREATE INDEX idx_articles_search ON articles USING GIN(search_vector);

-- Search query
SELECT title, ts_rank(search_vector, query) as rank
FROM articles, to_tsquery('english', 'postgresql & performance') query
WHERE search_vector @@ query
ORDER BY rank DESC;
```

## 18. Advanced Analytics

### Q51: Calculate customer lifetime value
```sql
WITH customer_metrics AS (
    SELECT 
        customer_id,
        MIN(order_date) as first_order,
        MAX(order_date) as last_order,
        COUNT(*) as order_count,
        SUM(amount) as total_spent,
        AVG(amount) as avg_order_value
    FROM orders
    GROUP BY customer_id
),
customer_lifespan AS (
    SELECT 
        *,
        EXTRACT(DAYS FROM (last_order - first_order)) + 1 as days_active,
        total_spent / NULLIF(EXTRACT(DAYS FROM (last_order - first_order)) + 1, 0) as daily_value
    FROM customer_metrics
)
SELECT 
    customer_id,
    total_spent as lifetime_value,
    daily_value * 365 as projected_annual_value,
    CASE 
        WHEN days_active >= 365 THEN 'Loyal'
        WHEN total_spent > 1000 THEN 'High Value'
        ELSE 'Regular'
    END as customer_segment
FROM customer_lifespan;
```

### Q52: Cohort analysis
```sql
WITH cohort_data AS (
    SELECT 
        customer_id,
        DATE_TRUNC('month', MIN(order_date)) as cohort_month,
        DATE_TRUNC('month', order_date) as order_month
    FROM orders
    GROUP BY customer_id, DATE_TRUNC('month', order_date)
),
cohort_table AS (
    SELECT 
        cohort_month,
        EXTRACT(EPOCH FROM (order_month - cohort_month))/2592000 as period_number,
        COUNT(DISTINCT customer_id) as customers
    FROM cohort_data
    GROUP BY cohort_month, order_month
)
SELECT 
    cohort_month,
    period_number,
    customers,
    FIRST_VALUE(customers) OVER (PARTITION BY cohort_month ORDER BY period_number) as cohort_size,
    ROUND(100.0 * customers / FIRST_VALUE(customers) OVER (PARTITION BY cohort_month ORDER BY period_number), 2) as retention_rate
FROM cohort_table
ORDER BY cohort_month, period_number;
```

## 19. Data Quality and Validation

### Q53: Find orphaned records
```sql
-- Find employees without departments
SELECT e.name
FROM employees e
LEFT JOIN departments d ON e.department_id = d.department_id
WHERE d.department_id IS NULL;

-- Find orders without customers
SELECT o.order_id
FROM orders o
LEFT JOIN customers c ON o.customer_id = c.customer_id
WHERE c.customer_id IS NULL;
```

### Q54: Data profiling query
```sql
SELECT 
    'employees' as table_name,
    COUNT(*) as total_rows,
    COUNT(DISTINCT employee_id) as unique_ids,
    COUNT(*) - COUNT(name) as null_names,
    COUNT(*) - COUNT(email) as null_emails,
    COUNT(DISTINCT email) as unique_emails,
    MIN(salary) as min_salary,
    MAX(salary) as max_salary,
    AVG(salary) as avg_salary,
    STDDEV(salary) as salary_stddev
FROM employees;
```

### Q55: Detect potential duplicates
```sql
SELECT 
    name,
    email,
    COUNT(*) as duplicate_count,
    STRING_AGG(employee_id::text, ', ') as employee_ids
FROM employees
GROUP BY LOWER(TRIM(name)), LOWER(TRIM(email))
HAVING COUNT(*) > 1;
```

## 20. Complex Business Logic

### Q56: Calculate employee utilization rates
```sql
WITH project_hours AS (
    SELECT 
        employee_id,
        DATE_TRUNC('month', work_date) as month,
        SUM(hours_worked) as total_hours
    FROM timesheet
    GROUP BY employee_id, DATE_TRUNC('month', work_date)
),
working_days AS (
    SELECT 
        DATE_TRUNC('month', CURRENT_DATE) as month,
        COUNT(*) as business_days
    FROM generate_series(
        DATE_TRUNC('month', CURRENT_DATE),
        DATE_TRUNC('month', CURRENT_DATE) + INTERVAL '1 month' - INTERVAL '1 day',
        '1 day'::interval
    ) as day_series
    WHERE EXTRACT(DOW FROM day_series) BETWEEN 1 AND 5
)
SELECT 
    e.name,
    ph.month,
    ph.total_hours,
    wd.business_days * 8 as expected_hours,
    ROUND(100.0 * ph.total_hours / (wd.business_days * 8), 2) as utilization_rate
FROM employees e
JOIN project_hours ph ON e.employee_id = ph.employee_id
CROSS JOIN working_days wd
ORDER BY utilization_rate DESC;
```

### Q57: Inventory management with reorder points
```sql
SELECT 
    p.product_name,
    i.current_stock,
    i.reorder_point,
    i.reorder_quantity,
    COALESCE(pending.pending_orders, 0) as pending_orders,
    CASE 
        WHEN i.current_stock + COALESCE(pending.pending_orders, 0) <= i.reorder_point 
        THEN 'REORDER NEEDED'
        WHEN i.current_stock <= i.safety_stock 
        THEN 'LOW STOCK'
        ELSE 'OK'
    END as stock_status,
    CASE 
        WHEN i.current_stock + COALESCE(pending.pending_orders, 0) <= i.reorder_point
        THEN i.reorder_quantity - COALESCE(pending.pending_orders, 0)
        ELSE 0
    END as suggested_order_quantity
FROM products p
JOIN inventory i ON p.product_id = i.product_id
LEFT JOIN (
    SELECT 
        product_id,
        SUM(quantity) as pending_orders
    FROM purchase_orders po
    JOIN purchase_order_items poi ON po.order_id = poi.order_id
    WHERE po.status = 'PENDING'
    GROUP BY product_id
) pending ON p.product_id = pending.product_id
ORDER BY 
    CASE stock_status 
        WHEN 'REORDER NEEDED' THEN 1
        WHEN 'LOW STOCK' THEN 2
        ELSE 3
    END;
```

## 21. Geographic and Spatial Queries (PostGIS)

### Q58: Find nearby locations (assuming PostGIS extension)
```sql
-- Enable PostGIS extension
CREATE EXTENSION IF NOT EXISTS postgis;

-- Find stores within 10km of a point
SELECT 
    store_name,
    ST_Distance(location, ST_MakePoint(-122.4194, 37.7749)) as distance_meters
FROM stores
WHERE ST_DWithin(location, ST_MakePoint(-122.4194, 37.7749), 10000)
ORDER BY distance_meters;
```

## 22. Advanced Security

### Q59: Row Level Security (RLS)
```sql
-- Enable RLS on table
ALTER TABLE employee_data ENABLE ROW LEVEL SECURITY;

-- Create policy
CREATE POLICY employee_data_policy ON employee_data
    FOR ALL TO application_role
    USING (department_id = get_current_user_department());

-- Create function to get user's department
CREATE OR REPLACE FUNCTION get_current_user_department()
RETURNS INTEGER AS $$
    SELECT department_id FROM user_departments 
    WHERE username = current_user;
$$ LANGUAGE SQL STABLE;
```

## 23. Database Administration

### Q60: Monitor database performance
```sql
-- Find slow queries
SELECT 
    query,
    calls,
    total_time,
    mean_time,
    min_time,
    max_time,
    stddev_time
FROM pg_stat_statements
ORDER BY mean_time DESC
LIMIT 10;
```

### Q61: Find blocking queries
```sql
SELECT 
    blocked_locks.pid AS blocked_pid,
    blocked_activity.usename AS blocked_user,
    blocking_locks.pid AS blocking_pid,
    blocking_activity.usename AS blocking_user,
    blocked_activity.query AS blocked_statement,
    blocking_activity.query AS blocking_statement
FROM pg_catalog.pg_locks blocked_locks
JOIN pg_catalog.pg_stat_activity blocked_activity 
    ON blocked_activity.pid = blocked_locks.pid
JOIN pg_catalog.pg_locks blocking_locks 
    ON blocking_locks.locktype = blocked_locks.locktype
    AND blocking_locks.DATABASE IS NOT DISTINCT FROM blocked_locks.DATABASE
    AND blocking_locks.relation IS NOT DISTINCT FROM blocked_locks.relation
    AND blocking_locks.page IS NOT DISTINCT FROM blocked_locks.page
    AND blocking_locks.tuple IS NOT DISTINCT FROM blocked_locks.tuple
    AND blocking_locks.virtualxid IS NOT DISTINCT FROM blocked_locks.virtualxid
    AND blocking_locks.transactionid IS NOT DISTINCT FROM blocked_locks.transactionid
    AND blocking_locks.classid IS NOT DISTINCT FROM blocked_locks.classid
    AND blocking_locks.objid IS NOT DISTINCT FROM blocked_locks.objid
    AND blocking_locks.objsubid IS NOT DISTINCT FROM blocked_locks.objsubid
    AND blocking_locks.pid != blocked_locks.pid
JOIN pg_catalog.pg_stat_activity blocking_activity 
    ON blocking_activity.pid = blocking_locks.pid
WHERE NOT blocked_locks.GRANTED;
```

### Q62: Table and index sizes
```sql
SELECT 
    schemaname,
    tablename,
    pg_size_pretty(pg_total_relation_size(schemaname||'.'||tablename)) as total_size,
    pg_size_pretty(pg_relation_size(schemaname||'.'||tablename)) as table_size,
    pg_size_pretty(pg_total_relation_size(schemaname||'.'||tablename) - 
                   pg_relation_size(schemaname||'.'||tablename)) as index_size
FROM pg_tables
WHERE schemaname NOT IN ('information_schema', 'pg_catalog')
ORDER BY pg_total_relation_size(schemaname||'.'||tablename) DESC;
```

## 24. Data Migration and ETL

### Q63: Pivot data
```sql
-- Transform rows to columns
SELECT 
    employee_id,
    SUM(CASE WHEN skill_name = 'PostgreSQL' THEN 1 ELSE 0 END) as postgresql,
    SUM(CASE WHEN skill_name = 'Python' THEN 1 ELSE 0 END) as python,
    SUM(CASE WHEN skill_name = 'Java' THEN 1 ELSE 0 END) as java
FROM employee_skills
GROUP BY employee_id;
```

### Q64: Unpivot data
```sql
-- Transform columns to rows
SELECT employee_id, 'Q1' as quarter, q1_sales as sales FROM quarterly_sales
UNION ALL
SELECT employee_id, 'Q2' as quarter, q2_sales as sales FROM quarterly_sales
UNION ALL
SELECT employee_id, 'Q3' as quarter, q3_sales as sales FROM quarterly_sales
UNION ALL
SELECT employee_id, 'Q4' as quarter, q4_sales as sales FROM quarterly_sales;
```

### Q65: Data cleansing
```sql
UPDATE customers
SET 
    email = LOWER(TRIM(email)),
    phone = REGEXP_REPLACE(phone, '[^0-9]', '', 'g'),
    name = TRIM(REGEXP_REPLACE(name, '\s+', ' ', 'g'))
WHERE 
    email IS NOT NULL OR 
    phone IS NOT NULL OR 
    name IS NOT NULL;
```

## 25. Advanced Optimization

### Q66: Query optimization with materialized view
```sql
-- Create materialized view for expensive aggregation
CREATE MATERIALIZED VIEW monthly_sales_summary AS
SELECT 
    DATE_TRUNC('month', order_date) as month,
    customer_id,
    COUNT(*) as order_count,
    SUM(amount) as total_amount,
    AVG(amount) as avg_amount
FROM orders
GROUP BY DATE_TRUNC('month', order_date), customer_id;

-- Create index on materialized view
CREATE INDEX idx_monthly_sales_month_customer 
ON monthly_sales_summary(month, customer_id);

-- Refresh materialized view
REFRESH MATERIALIZED VIEW monthly_sales_summary;
```

### Q67: Parallel query example
```sql
SET max_parallel_workers_per_gather = 4;
SET parallel_tuple_cost = 0.1;

SELECT /*+ Parallel(orders 4) */
    customer_id,
    COUNT(*) as order_count,
    SUM(amount) as total_spent
FROM orders
WHERE order_date >= '2024-01-01'
GROUP BY customer_id
HAVING COUNT(*) > 10;
```

## 26. Error Handling and Debugging

### Q68: Exception handling in functions
```sql
CREATE OR REPLACE FUNCTION safe_divide(a NUMERIC, b NUMERIC)
RETURNS NUMERIC AS $$
BEGIN
    IF b = 0 THEN
        RAISE EXCEPTION 'Division by zero is not allowed';
    END IF;
    
    RETURN a / b;
EXCEPTION
    WHEN division_by_zero THEN
        RAISE NOTICE 'Division by zero attempted, returning NULL';
        RETURN NULL;
    WHEN OTHERS THEN
        RAISE NOTICE 'Unexpected error: %', SQLERRM;
        RETURN NULL;
END;
$ LANGUAGE plpgsql;
```

### Q69: Transaction with rollback
```sql
BEGIN;

SAVEPOINT before_update;

UPDATE accounts SET balance = balance - 1000 WHERE account_id = 1;
UPDATE accounts SET balance = balance + 1000 WHERE account_id = 2;

-- Check if first account has sufficient balance
IF (SELECT balance FROM accounts WHERE account_id = 1) < 0 THEN
    ROLLBACK TO SAVEPOINT before_update;
    RAISE EXCEPTION 'Insufficient funds';
END IF;

COMMIT;
```

## 27. Advanced Data Types

### Q70: Working with UUID
```sql
-- Enable UUID extension
CREATE EXTENSION IF NOT EXISTS "uuid-ossp";

-- Create table with UUID
CREATE TABLE sessions (
    session_id UUID PRIMARY KEY DEFAULT uuid_generate_v4(),
    user_id INTEGER,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Query with UUID
SELECT * FROM sessions WHERE session_id = '550e8400-e29b-41d4-a716-446655440000';
```

### Q71: Working with XML data
```sql
-- Query XML data
SELECT 
    id,
    XPATH('//name/text()', xml_data)[1]::TEXT as name,
    XPATH('//age/text()', xml_data)[1]::TEXT::INTEGER as age
FROM user_profiles
WHERE XPATH('//city/text()', xml_data)[1]::TEXT = 'New York';
```

### Q72: Working with network addresses (inet/cidr)
```sql
CREATE TABLE network_logs (
    id SERIAL PRIMARY KEY,
    client_ip INET,
    network CIDR,
    access_time TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Find all IPs in a specific network
SELECT client_ip
FROM network_logs
WHERE client_ip << '192.168.1.0/24';

-- Find network containing specific IP
SELECT network
FROM network_logs
WHERE '192.168.1.100'::INET << network;
```

## 28. Advanced Transactions

### Q73: Isolation levels demonstration
```sql
-- Session 1: Read Committed (default)
BEGIN ISOLATION LEVEL READ COMMITTED;
SELECT balance FROM accounts WHERE account_id = 1;
-- Result: 1000

-- Session 2: Update in different transaction
BEGIN;
UPDATE accounts SET balance = 1500 WHERE account_id = 1;
COMMIT;

-- Session 1: Read again
SELECT balance FROM accounts WHERE account_id = 1;
-- Result: 1500 (sees committed changes)
COMMIT;

-- Repeatable Read example
BEGIN ISOLATION LEVEL REPEATABLE READ;
SELECT balance FROM accounts WHERE account_id = 1;
-- Will see consistent snapshot throughout transaction
```

### Q74: Advisory locks
```sql
-- Try to acquire advisory lock
SELECT pg_try_advisory_lock(12345);

-- Process critical section
UPDATE inventory SET quantity = quantity - 1 
WHERE product_id = 100 AND quantity > 0;

-- Release lock
SELECT pg_advisory_unlock(12345);
```

## 29. Performance Monitoring

### Q75: Index usage statistics
```sql
SELECT 
    schemaname,
    tablename,
    indexname,
    idx_tup_read,
    idx_tup_fetch,
    idx_scan,
    CASE WHEN idx_scan > 0 
         THEN round((idx_tup_fetch::numeric / idx_scan)::numeric, 2)
         ELSE 0 
    END AS avg_tuples_per_scan
FROM pg_stat_user_indexes
ORDER BY idx_scan DESC;
```

### Q76: Buffer cache hit ratio
```sql
SELECT 
    schemaname,
    tablename,
    heap_blks_read,
    heap_blks_hit,
    ROUND(
        100.0 * heap_blks_hit / NULLIF(heap_blks_hit + heap_blks_read, 0), 
        2
    ) AS cache_hit_ratio
FROM pg_statio_user_tables
WHERE heap_blks_read > 0
ORDER BY cache_hit_ratio;
```

### Q77: Find missing indexes
```sql
SELECT 
    schemaname,
    tablename,
    attname,
    n_distinct,
    correlation,
    seq_scan,
    seq_tup_read,
    CASE WHEN seq_scan > 0 
         THEN seq_tup_read / seq_scan 
         ELSE 0 
    END as avg_seq_read
FROM pg_stats
JOIN pg_stat_user_tables ON pg_stats.tablename = pg_stat_user_tables.relname
WHERE seq_scan > 100 AND n_distinct > 100
ORDER BY seq_scan DESC;
```

## 30. Backup and Recovery

### Q78: Point-in-time recovery simulation
```sql
-- Create a restore point
SELECT pg_create_restore_point('before_data_modification');

-- Show current WAL position
SELECT pg_current_wal_lsn();

-- Backup command (would be run from command line)
-- pg_basebackup -D /backup/location -Ft -z -P

-- Recovery configuration (in postgresql.conf or recovery.signal)
-- restore_command = 'cp /archive/%f %p'
-- recovery_target_name = 'before_data_modification'
```

### Q79: Logical replication setup
```sql
-- On publisher
CREATE PUBLICATION my_publication FOR TABLE employees, departments;

-- On subscriber
CREATE SUBSCRIPTION my_subscription 
CONNECTION 'host=publisher_host port=5432 user=replication_user dbname=mydb'
PUBLICATION my_publication;

-- Monitor replication status
SELECT * FROM pg_stat_subscription;
SELECT * FROM pg_stat_replication;
```

## 31. Advanced Analytics Functions

### Q80: Time series analysis
```sql
WITH daily_sales AS (
    SELECT 
        DATE(order_date) as sale_date,
        SUM(amount) as daily_total
    FROM orders
    WHERE order_date >= CURRENT_DATE - INTERVAL '30 days'
    GROUP BY DATE(order_date)
),
sales_with_lag AS (
    SELECT 
        sale_date,
        daily_total,
        LAG(daily_total, 1) OVER (ORDER BY sale_date) as prev_day,
        LAG(daily_total, 7) OVER (ORDER BY sale_date) as prev_week
    FROM daily_sales
)
SELECT 
    sale_date,
    daily_total,
    prev_day,
    daily_total - prev_day as day_over_day_change,
    ROUND(100.0 * (daily_total - prev_day) / NULLIF(prev_day, 0), 2) as day_over_day_pct,
    daily_total - prev_week as week_over_week_change,
    ROUND(100.0 * (daily_total - prev_week) / NULLIF(prev_week, 0), 2) as week_over_week_pct
FROM sales_with_lag
ORDER BY sale_date;
```

### Q81: Advanced statistical functions
```sql
SELECT 
    department_id,
    COUNT(*) as employee_count,
    AVG(salary) as mean_salary,
    STDDEV_POP(salary) as population_stddev,
    STDDEV_SAMP(salary) as sample_stddev,
    VAR_POP(salary) as population_variance,
    VAR_SAMP(salary) as sample_variance,
    PERCENTILE_CONT(0.25) WITHIN GROUP (ORDER BY salary) as q1,
    PERCENTILE_CONT(0.5) WITHIN GROUP (ORDER BY salary) as median,
    PERCENTILE_CONT(0.75) WITHIN GROUP (ORDER BY salary) as q3,
    PERCENTILE_CONT(0.75) WITHIN GROUP (ORDER BY salary) - 
    PERCENTILE_CONT(0.25) WITHIN GROUP (ORDER BY salary) as iqr
FROM employees
GROUP BY department_id;
```

### Q82: Correlation analysis
```sql
SELECT 
    CORR(years_experience, salary) as experience_salary_correlation,
    CORR(age, salary) as age_salary_correlation,
    REGR_SLOPE(salary, years_experience) as salary_per_year_experience,
    REGR_INTERCEPT(salary, years_experience) as base_salary,
    REGR_R2(salary, years_experience) as r_squared
FROM employees
WHERE years_experience IS NOT NULL AND salary IS NOT NULL;
```

## 32. Complex Queries for Business Intelligence

### Q83: Customer segmentation (RFM Analysis)
```sql
WITH customer_metrics AS (
    SELECT 
        customer_id,
        MAX(order_date) as last_order_date,
        COUNT(*) as frequency,
        SUM(amount) as monetary_value,
        CURRENT_DATE - MAX(order_date) as recency_days
    FROM orders
    GROUP BY customer_id
),
rfm_scores AS (
    SELECT 
        customer_id,
        recency_days,
        frequency,
        monetary_value,
        NTILE(5) OVER (ORDER BY recency_days ASC) as recency_score,
        NTILE(5) OVER (ORDER BY frequency DESC) as frequency_score,
        NTILE(5) OVER (ORDER BY monetary_value DESC) as monetary_score
    FROM customer_metrics
)
SELECT 
    customer_id,
    recency_score,
    frequency_score,
    monetary_score,
    CASE 
        WHEN recency_score >= 4 AND frequency_score >= 4 AND monetary_score >= 4 THEN 'Champions'
        WHEN recency_score >= 3 AND frequency_score >= 3 AND monetary_score >= 3 THEN 'Loyal Customers'
        WHEN recency_score >= 3 AND frequency_score <= 2 THEN 'Potential Loyalists'
        WHEN recency_score >= 4 AND frequency_score <= 2 AND monetary_score <= 2 THEN 'New Customers'
        WHEN recency_score <= 2 AND frequency_score >= 3 AND monetary_score >= 3 THEN 'At Risk'
        WHEN recency_score <= 2 AND frequency_score <= 2 AND monetary_score >= 3 THEN 'Cannot Lose Them'
        WHEN recency_score <= 2 AND frequency_score <= 2 AND monetary_score <= 2 THEN 'Hibernating'
        ELSE 'Others'
    END as customer_segment
FROM rfm_scores;
```

### Q84: Sales funnel analysis
```sql
WITH funnel_steps AS (
    SELECT 
        DATE_TRUNC('month', created_date) as month,
        COUNT(*) as leads
    FROM leads
    GROUP BY DATE_TRUNC('month', created_date)
),
opportunities AS (
    SELECT 
        DATE_TRUNC('month', created_date) as month,
        COUNT(*) as opportunities
    FROM opportunities
    GROUP BY DATE_TRUNC('month', created_date)
),
closed_deals AS (
    SELECT 
        DATE_TRUNC('month', closed_date) as month,
        COUNT(*) as deals,
        SUM(amount) as revenue
    FROM opportunities
    WHERE status = 'Closed Won'
    GROUP BY DATE_TRUNC('month', closed_date)
)
SELECT 
    f.month,
    f.leads,
    o.opportunities,
    cd.deals,
    cd.revenue,
    ROUND(100.0 * o.opportunities / NULLIF(f.leads, 0), 2) as lead_to_opp_rate,
    ROUND(100.0 * cd.deals / NULLIF(o.opportunities, 0), 2) as opp_to_close_rate,
    ROUND(100.0 * cd.deals / NULLIF(f.leads, 0), 2) as overall_conversion_rate,
    ROUND(cd.revenue / NULLIF(cd.deals, 0), 2) as avg_deal_size
FROM funnel_steps f
LEFT JOIN opportunities o ON f.month = o.month
LEFT JOIN closed_deals cd ON f.month = cd.month
ORDER BY f.month;
```

### Q85: Seasonal analysis
```sql
SELECT 
    EXTRACT(QUARTER FROM order_date) as quarter,
    EXTRACT(MONTH FROM order_date) as month,
    COUNT(*) as order_count,
    SUM(amount) as total_revenue,
    AVG(amount) as avg_order_value,
    LAG(SUM(amount)) OVER (
        PARTITION BY EXTRACT(QUARTER FROM order_date) 
        ORDER BY EXTRACT(YEAR FROM order_date)
    ) as prev_year_same_quarter,
    ROUND(
        100.0 * (
            SUM(amount) - LAG(SUM(amount)) OVER (
                PARTITION BY EXTRACT(QUARTER FROM order_date) 
                ORDER BY EXTRACT(YEAR FROM order_date)
            )
        ) / NULLIF(
            LAG(SUM(amount)) OVER (
                PARTITION BY EXTRACT(QUARTER FROM order_date) 
                ORDER BY EXTRACT(YEAR FROM order_date)
            ), 0
        ), 2
    ) as yoy_growth_rate
FROM orders
GROUP BY EXTRACT(YEAR FROM order_date), EXTRACT(QUARTER FROM order_date), EXTRACT(MONTH FROM order_date)
ORDER BY EXTRACT(YEAR FROM order_date), quarter, month;
```

## 33. Advanced Data Modeling

### Q86: Slowly Changing Dimensions (Type 2)
```sql
CREATE TABLE customer_dim (
    customer_key SERIAL PRIMARY KEY,
    customer_id INTEGER,
    customer_name VARCHAR(100),
    address VARCHAR(200),
    phone VARCHAR(20),
    effective_date DATE,
    expiration_date DATE,
    is_current BOOLEAN DEFAULT TRUE
);

-- Function to handle SCD Type 2 updates
CREATE OR REPLACE FUNCTION update_customer_scd(
    p_customer_id INTEGER,
    p_customer_name VARCHAR(100),
    p_address VARCHAR(200),
    p_phone VARCHAR(20)
)
RETURNS VOID AS $
BEGIN
    -- Expire current record
    UPDATE customer_dim
    SET expiration_date = CURRENT_DATE - 1,
        is_current = FALSE
    WHERE customer_id = p_customer_id AND is_current = TRUE;
    
    -- Insert new record
    INSERT INTO customer_dim (
        customer_id, customer_name, address, phone, 
        effective_date, expiration_date, is_current
    )
    VALUES (
        p_customer_id, p_customer_name, p_address, p_phone,
        CURRENT_DATE, '9999-12-31', TRUE
    );
END;
$ LANGUAGE plpgsql;
```

### Q87: Hierarchical data with path enumeration
```sql
WITH RECURSIVE org_hierarchy AS (
    -- Root level
    SELECT 
        employee_id,
        name,
        manager_id,
        1 as level,
        ARRAY[employee_id] as path,
        name::TEXT as path_names
    FROM employees
    WHERE manager_id IS NULL
    
    UNION ALL
    
    -- Recursive part
    SELECT 
        e.employee_id,
        e.name,
        e.manager_id,
        oh.level + 1,
        oh.path || e.employee_id,
        oh.path_names || ' > ' || e.name
    FROM employees e
    JOIN org_hierarchy oh ON e.manager_id = oh.employee_id
)
SELECT 
    employee_id,
    name,
    level,
    REPEAT('  ', level - 1) || name as indented_name,
    path_names,
    ARRAY_LENGTH(path, 1) as depth
FROM org_hierarchy
ORDER BY path;
```

## 34. Data Warehouse Queries

### Q88: Star schema query with multiple fact tables
```sql
SELECT 
    d.date,
    p.product_name,
    c.customer_name,
    r.region_name,
    SUM(fs.quantity) as total_quantity,
    SUM(fs.revenue) as total_revenue,
    AVG(fr.rating) as avg_rating,
    COUNT(fr.review_id) as review_count
FROM fact_sales fs
JOIN dim_date d ON fs.date_key = d.date_key
JOIN dim_product p ON fs.product_key = p.product_key
JOIN dim_customer c ON fs.customer_key = c.customer_key
JOIN dim_region r ON c.region_key = r.region_key
LEFT JOIN fact_reviews fr ON fs.product_key = fr.product_key 
    AND fs.customer_key = fr.customer_key
WHERE d.fiscal_year = 2024
    AND r.region_name = 'North America'
GROUP BY d.date, p.product_name, c.customer_name, r.region_name
HAVING SUM(fs.revenue) > 10000
ORDER BY total_revenue DESC;
```

### Q89: Advanced cube operations
```sql
SELECT 
    COALESCE(region_name, 'ALL REGIONS') as region,
    COALESCE(product_category, 'ALL CATEGORIES') as category,
    COALESCE(TO_CHAR(sale_date, 'YYYY-MM'), 'ALL MONTHS') as month,
    SUM(amount) as total_sales,
    COUNT(*) as transaction_count,
    GROUPING(region_name, product_category, TO_CHAR(sale_date, 'YYYY-MM')) as grouping_level
FROM sales s
JOIN products p ON s.product_id = p.product_id
JOIN regions r ON s.region_id = r.region_id
WHERE sale_date >= '2024-01-01'
GROUP BY CUBE(region_name, product_category, TO_CHAR(sale_date, 'YYYY-MM'))
ORDER BY grouping_level, region, category, month;
```

## 35. Security and Compliance

### Q90: Data masking for sensitive information
```sql
CREATE OR REPLACE FUNCTION mask_credit_card(cc_number TEXT)
RETURNS TEXT AS $
BEGIN
    IF LENGTH(cc_number) >= 4 THEN
        RETURN REPEAT('*', LENGTH(cc_number) - 4) || RIGHT(cc_number, 4);
    ELSE
        RETURN REPEAT('*', LENGTH(cc_number));
    END IF;
END;
$ LANGUAGE plpgsql SECURITY DEFINER;

-- Usage
SELECT 
    customer_name,
    mask_credit_card(credit_card_number) as masked_cc,
    CASE 
        WHEN current_user = 'admin' THEN email
        ELSE REGEXP_REPLACE(email, '^(.{2}).*(@.*)
    , '\1***\2')
    END as email
FROM customer_payments;
```

### Q91: Audit trail with encryption
```sql
-- Install pgcrypto extension
CREATE EXTENSION IF NOT EXISTS pgcrypto;

CREATE TABLE audit_log (
    id SERIAL PRIMARY KEY,
    table_name VARCHAR(50),
    operation CHAR(1),
    old_values TEXT,
    new_values TEXT,
    user_name VARCHAR(50),
    timestamp TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    encrypted_data TEXT
);

-- Audit trigger with encryption
CREATE OR REPLACE FUNCTION audit_trigger_with_encryption()
RETURNS TRIGGER AS $
DECLARE
    old_data TEXT;
    new_data TEXT;
    encryption_key TEXT := 'my_secret_key_2024';
BEGIN
    IF TG_OP = 'DELETE' THEN
        old_data := row_to_json(OLD)::TEXT;
        INSERT INTO audit_log (
            table_name, operation, old_values, user_name, encrypted_data
        ) VALUES (
            TG_TABLE_NAME, 'D', old_data, user,
            pgp_sym_encrypt(old_data, encryption_key)
        );
        RETURN OLD;
    ELSIF TG_OP = 'UPDATE' THEN
        old_data := row_to_json(OLD)::TEXT;
        new_data := row_to_json(NEW)::TEXT;
        INSERT INTO audit_log (
            table_name, operation, old_values, new_values, user_name, encrypted_data
        ) VALUES (
            TG_TABLE_NAME, 'U', old_data, new_data, user,
            pgp_sym_encrypt(new_data, encryption_key)
        );
        RETURN NEW;
    ELSIF TG_OP = 'INSERT' THEN
        new_data := row_to_json(NEW)::TEXT;
        INSERT INTO audit_log (
            table_name, operation, new_values, user_name, encrypted_data
        ) VALUES (
            TG_TABLE_NAME, 'I', new_data, user,
            pgp_sym_encrypt(new_data, encryption_key)
        );
        RETURN NEW;
    END IF;
END;
$ LANGUAGE plpgsql;
```

## 36. Advanced Testing and Quality Assurance

### Q92: Data validation and constraint testing
```sql
-- Create a comprehensive data validation function
CREATE OR REPLACE FUNCTION validate_employee_data()
RETURNS TABLE (
    validation_rule VARCHAR(100),
    failed_records INTEGER,
    sample_ids INTEGER[]
) AS $
BEGIN
    -- Check for missing required fields
    RETURN QUERY
    SELECT 
        'Missing employee name'::VARCHAR(100),
        COUNT(*)::INTEGER,
        ARRAY_AGG(employee_id ORDER BY employee_id LIMIT 5)
    FROM employees 
    WHERE name IS NULL OR TRIM(name) = '';
    
    -- Check for invalid email formats
    RETURN QUERY
    SELECT 
        'Invalid email format'::VARCHAR(100),
        COUNT(*)::INTEGER,
        ARRAY_AGG(employee_id ORDER BY employee_id LIMIT 5)
    FROM employees 
    WHERE email IS NOT NULL 
        AND email !~ '^[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Za-z]{2,}
    ;
    
    -- Check for duplicate emails
    RETURN QUERY
    SELECT 
        'Duplicate email addresses'::VARCHAR(100),
        COUNT(*)::INTEGER,
        ARRAY_AGG(employee_id ORDER BY employee_id LIMIT 5)
    FROM employees e1
    WHERE EXISTS (
        SELECT 1 FROM employees e2 
        WHERE e1.email = e2.email AND e1.employee_id != e2.employee_id
    );
    
    -- Check for unrealistic salaries
    RETURN QUERY
    SELECT 
        'Unrealistic salary values'::VARCHAR(100),
        COUNT(*)::INTEGER,
        ARRAY_AGG(employee_id ORDER BY employee_id LIMIT 5)
    FROM employees 
    WHERE salary < 0 OR salary > 1000000;
    
    -- Check for future hire dates
    RETURN QUERY
    SELECT 
        'Future hire dates'::VARCHAR(100),
        COUNT(*)::INTEGER,
        ARRAY_AGG(employee_id ORDER BY employee_id LIMIT 5)
    FROM employees 
    WHERE hire_date > CURRENT_DATE;
END;
$ LANGUAGE plpgsql;

-- Run validation
SELECT * FROM validate_employee_data();
```

### Q93: Performance testing query
```sql
-- Create a performance test for different query patterns
CREATE OR REPLACE FUNCTION performance_test_queries()
RETURNS TABLE (
    query_name VARCHAR(100),
    execution_time_ms NUMERIC,
    rows_returned BIGINT
) AS $
DECLARE
    start_time TIMESTAMP;
    end_time TIMESTAMP;
    row_count BIGINT;
BEGIN
    -- Test 1: Simple aggregation
    start_time := clock_timestamp();
    SELECT COUNT(*) INTO row_count FROM employees;
    end_time := clock_timestamp();
    
    RETURN QUERY SELECT 
        'Simple COUNT(*)'::VARCHAR(100),
        EXTRACT(EPOCH FROM (end_time - start_time)) * 1000,
        row_count;
    
    -- Test 2: Complex JOIN with aggregation
    start_time := clock_timestamp();
    SELECT COUNT(*) INTO row_count
    FROM employees e
    JOIN departments d ON e.department_id = d.department_id
    JOIN employee_projects ep ON e.employee_id = ep.employee_id
    WHERE e.salary > 50000;
    end_time := clock_timestamp();
    
    RETURN QUERY SELECT 
        'Complex JOIN with WHERE'::VARCHAR(100),
        EXTRACT(EPOCH FROM (end_time - start_time)) * 1000,
        row_count;
    
    -- Test 3: Window function
    start_time := clock_timestamp();
    SELECT COUNT(*) INTO row_count FROM (
        SELECT employee_id, 
               ROW_NUMBER() OVER (PARTITION BY department_id ORDER BY salary DESC)
        FROM employees
    ) ranked WHERE row_number <= 5;
    end_time := clock_timestamp();
    
    RETURN QUERY SELECT 
        'Window function with ranking'::VARCHAR(100),
        EXTRACT(EPOCH FROM (end_time - start_time)) * 1000,
        row_count;
END;
$ LANGUAGE plpgsql;

-- Run performance test
SELECT * FROM performance_test_queries();
```

## 37. Machine Learning and Analytics

### Q94: Simple linear regression in SQL
```sql
WITH regression_data AS (
    SELECT 
        years_experience as x,
        salary as y,
        COUNT(*) OVER() as n,
        AVG(years_experience) OVER() as x_mean,
        AVG(salary) OVER() as y_mean
    FROM employees
    WHERE years_experience IS NOT NULL AND salary IS NOT NULL
),
regression_calc AS (
    SELECT 
        SUM((x - x_mean) * (y - y_mean)) as numerator,
        SUM(POWER(x - x_mean, 2)) as denominator,
        y_mean,
        x_mean
    FROM regression_data
    GROUP BY y_mean, x_mean
)
SELECT 
    numerator / NULLIF(denominator, 0) as slope,
    y_mean - (numerator / NULLIF(denominator, 0)) * x_mean as intercept,
    CASE 
        WHEN denominator > 0 THEN
            'Salary = ' || ROUND(y_mean - (numerator / denominator) * x_mean, 2) ||
            ' + ' || ROUND(numerator / denominator, 2) || ' * years_experience'
        ELSE 'Cannot calculate regression'
    END as equation
FROM regression_calc;
```

### Q95: Anomaly detection using statistical methods
```sql
WITH stats AS (
    SELECT 
        AVG(amount) as mean_amount,
        STDDEV(amount) as stddev_amount
    FROM transactions
    WHERE transaction_date >= CURRENT_DATE - INTERVAL '30 days'
),
anomalies AS (
    SELECT 
        transaction_id,
        customer_id,
        amount,
        transaction_date,
        ABS(amount - stats.mean_amount) / NULLIF(stats.stddev_amount, 0) as z_score
    FROM transactions
    CROSS JOIN stats
    WHERE transaction_date >= CURRENT_DATE - INTERVAL '30 days'
)
SELECT 
    transaction_id,
    customer_id,
    amount,
    transaction_date,
    z_score,
    CASE 
        WHEN z_score > 3 THEN 'High Anomaly'
        WHEN z_score > 2 THEN 'Medium Anomaly'
        WHEN z_score > 1.5 THEN 'Low Anomaly'
        ELSE 'Normal'
    END as anomaly_level
FROM anomalies
WHERE z_score > 1.5
ORDER BY z_score DESC;
```

## 38. Real-time Analytics

### Q96: Streaming aggregation simulation
```sql
-- Create a function to simulate real-time metrics
CREATE OR REPLACE FUNCTION real_time_metrics(lookback_minutes INTEGER DEFAULT 5)
RETURNS TABLE (
    metric_name VARCHAR(50),
    current_value NUMERIC,
    previous_value NUMERIC,
    change_pct NUMERIC,
    trend VARCHAR(20)
) AS $
BEGIN
    -- Orders per minute
    RETURN QUERY
    WITH current_window AS (
        SELECT COUNT(*) as cnt
        FROM orders
        WHERE order_date >= NOW() - (lookback_minutes || ' minutes')::INTERVAL
    ),
    previous_window AS (
        SELECT COUNT(*) as cnt
        FROM orders
        WHERE order_date >= NOW() - (lookback_minutes * 2 || ' minutes')::INTERVAL
            AND order_date < NOW() - (lookback_minutes || ' minutes')::INTERVAL
    )
    SELECT 
        'Orders per minute'::VARCHAR(50),
        (c.cnt::NUMERIC / lookback_minutes),
        (p.cnt::NUMERIC / lookback_minutes),
        CASE WHEN p.cnt > 0 
             THEN ROUND(100.0 * (c.cnt - p.cnt) / p.cnt, 2)
             ELSE NULL 
        END,
        CASE 
            WHEN p.cnt > 0 AND c.cnt > p.cnt THEN 'UP'
            WHEN p.cnt > 0 AND c.cnt < p.cnt THEN 'DOWN'
            ELSE 'STABLE'
        END::VARCHAR(20)
    FROM current_window c, previous_window p;
    
    -- Average order value
    RETURN QUERY
    WITH current_window AS (
        SELECT AVG(amount) as avg_amt
        FROM orders
        WHERE order_date >= NOW() - (lookback_minutes || ' minutes')::INTERVAL
    ),
    previous_window AS (
        SELECT AVG(amount) as avg_amt
        FROM orders
        WHERE order_date >= NOW() - (lookback_minutes * 2 || ' minutes')::INTERVAL
            AND order_date < NOW() - (lookback_minutes || ' minutes')::INTERVAL
    )
    SELECT 
        'Average order value'::VARCHAR(50),
        c.avg_amt,
        p.avg_amt,
        CASE WHEN p.avg_amt > 0 
             THEN ROUND(100.0 * (c.avg_amt - p.avg_amt) / p.avg_amt, 2)
             ELSE NULL 
        END,
        CASE 
            WHEN p.avg_amt > 0 AND c.avg_amt > p.avg_amt THEN 'UP'
            WHEN p.avg_amt > 0 AND c.avg_amt < p.avg_amt THEN 'DOWN'
            ELSE 'STABLE'
        END::VARCHAR(20)
    FROM current_window c, previous_window p;
END;
$ LANGUAGE plpgsql;

-- Usage
SELECT * FROM real_time_metrics(10);
```

## 39. Database Architecture and Design

### Q97: Database health check query
```sql
WITH db_stats AS (
    SELECT 
        pg_size_pretty(pg_database_size(current_database())) as db_size,
        (SELECT COUNT(*) FROM pg_stat_activity WHERE state = 'active') as active_connections,
        (SELECT COUNT(*) FROM pg_stat_activity WHERE state = 'idle') as idle_connections,
        (SELECT setting FROM pg_settings WHERE name = 'max_connections') as max_connections
),
table_stats AS (
    SELECT 
        COUNT(*) as total_tables,
        SUM(n_tup_ins) as total_inserts,
        SUM(n_tup_upd) as total_updates,
        SUM(n_tup_del) as total_deletes,
        SUM(seq_scan) as total_seq_scans,
        SUM(idx_scan) as total_idx_scans
    FROM pg_stat_user_tables
),
index_stats AS (
    SELECT 
        COUNT(*) as total_indexes,
        COUNT(*) FILTER (WHERE idx_scan = 0) as unused_indexes
    FROM pg_stat_user_indexes
)
SELECT 
    'Database Size' as metric,
    db_stats.db_size as value
FROM db_stats
UNION ALL
SELECT 
    'Active Connections',
    db_stats.active_connections::TEXT || '/' || db_stats.max_connections::TEXT
FROM db_stats
UNION ALL
SELECT 
    'Total Tables',
    table_stats.total_tables::TEXT
FROM table_stats
UNION ALL
SELECT 
    'Total Indexes',
    index_stats.total_indexes::TEXT
FROM index_stats
UNION ALL
SELECT 
    'Unused Indexes',
    index_stats.unused_indexes::TEXT
FROM index_stats
UNION ALL
SELECT 
    'Index Usage Ratio',
    ROUND(100.0 * table_stats.total_idx_scans / 
          NULLIF(table_stats.total_idx_scans + table_stats.total_seq_scans, 0), 2)::TEXT || '%'
FROM table_stats;
```

### Q98: Connection pooling analysis
```sql
SELECT 
    state,
    COUNT(*) as connection_count,
    ROUND(AVG(EXTRACT(EPOCH FROM (now() - state_change))), 2) as avg_duration_seconds,
    MAX(EXTRACT(EPOCH FROM (now() - state_change))) as max_duration_seconds,
    STRING_AGG(DISTINCT application_name, ', ') as applications
FROM pg_stat_activity
WHERE pid != pg_backend_pid()
GROUP BY state
ORDER BY connection_count DESC;
```

## 40. Advanced Query Optimization

### Q99: Query plan analysis function
```sql
CREATE OR REPLACE FUNCTION analyze_query_performance(query_text TEXT)
RETURNS TABLE (
    node_type TEXT,
    total_cost NUMERIC,
    startup_cost NUMERIC,
    rows_estimate BIGINT,
    width_estimate INTEGER,
    actual_time_ms NUMERIC,
    actual_rows BIGINT,
    loops INTEGER,
    optimization_suggestions TEXT
) AS $
BEGIN
    -- This is a simplified example - in practice, you'd parse EXPLAIN output
    -- For demonstration purposes, returning analysis suggestions
    
    RETURN QUERY
    SELECT 
        'Analysis'::TEXT,
        0::NUMERIC,
        0::NUMERIC,
        0::BIGINT,
        0::INTEGER,
        0::NUMERIC,
        0::BIGINT,
        0::INTEGER,
        CASE 
            WHEN query_text ILIKE '%SELECT *%' THEN 'Avoid SELECT *, specify needed columns'
            WHEN query_text ILIKE '%WHERE%NOT EXISTS%' THEN 'Consider using LEFT JOIN with IS NULL instead'
            WHEN query_text ILIKE '%ORDER BY%LIMIT%' THEN 'Ensure proper indexes for ORDER BY columns'
            WHEN query_text ILIKE '%GROUP BY%HAVING%' THEN 'Consider filtering before grouping with WHERE'
            ELSE 'Query appears optimized'
        END;
END;
$ LANGUAGE plpgsql;

-- Usage example
SELECT * FROM analyze_query_performance('SELECT * FROM employees WHERE salary > 50000 ORDER BY hire_date LIMIT 10');
```

### Q100: Index recommendation system
```sql
CREATE OR REPLACE FUNCTION recommend_indexes()
RETURNS TABLE (
    table_name TEXT,
    recommended_index TEXT,
    reason TEXT,
    priority INTEGER
) AS $
BEGIN
    -- Find tables with high sequential scan ratios
    RETURN QUERY
    SELECT 
        schemaname || '.' || relname,
        'CREATE INDEX idx_' || relname || '_' || 'composite ON ' || 
        schemaname || '.' || relname || '(column_name);',
        'High sequential scan ratio: ' || 
        ROUND(100.0 * seq_scan / NULLIF(seq_scan + coalesce(idx_scan, 0), 0), 2)::TEXT || '%',
        1
    FROM pg_stat_user_tables
    WHERE seq_scan > 1000 
        AND (seq_scan::FLOAT / NULLIF(seq_scan + coalesce(idx_scan, 0), 0)) > 0.8;
    
    -- Find large tables without primary key
    RETURN QUERY
    SELECT 
        schemaname || '.' || tablename,
        'ALTER TABLE ' || schemaname || '.' || tablename || ' ADD PRIMARY KEY (id);',
        'Large table without primary key, rows: ' || n_tup_ins::TEXT,
        2
    FROM pg_stat_user_tables
    LEFT JOIN pg_constraint ON conrelid = (schemaname || '.' || tablename)::regclass
        AND contype = 'p'
    WHERE conname IS NULL
        AND n_tup_ins > 10000;
        
    -- Find foreign keys without indexes
    RETURN QUERY
    SELECT 
        n.nspname || '.' || t.relname,
        'CREATE INDEX idx_' || t.relname || '_' || a.attname || 
        ' ON ' || n.nspname || '.' || t.relname || '(' || a.attname || ');',
        'Foreign key without supporting index: ' || a.attname,
        3
    FROM pg_constraint c
    JOIN pg_class t ON t.oid = c.conrelid
    JOIN pg_namespace n ON n.oid = t.relnamespace
    JOIN pg_attribute a ON a.attrelid = c.conrelid AND a.attnum = ANY(c.conkey)
    LEFT JOIN pg_index i ON i.indrelid = c.conrelid 
        AND a.attnum = ANY(i.indkey)
    WHERE c.contype = 'f'
        AND i.indexrelid IS NULL;
END;
$ LANGUAGE plpgsql;

-- Usage
SELECT * FROM recommend_indexes() ORDER BY priority;
```

## 41. Advanced Business Logic

### Q101: Dynamic pricing algorithm
```sql
CREATE OR REPLACE FUNCTION calculate_dynamic_price(
    base_price DECIMAL,
    product_id INTEGER,
    customer_segment VARCHAR(20),
    season VARCHAR(20) DEFAULT 'regular'
)
RETURNS DECIMAL AS $
DECLARE
    final_price DECIMAL;
    demand_multiplier DECIMAL := 1.0;
    inventory_multiplier DECIMAL := 1.0;
    customer_multiplier DECIMAL := 1.0;
    seasonal_multiplier DECIMAL := 1.0;
    current_inventory INTEGER;
    avg_daily_sales INTEGER;
BEGIN
    -- Get current inventory and sales velocity
    SELECT stock_quantity INTO current_inventory
    FROM inventory WHERE product_id = calculate_dynamic_price.product_id;
    
    SELECT AVG(daily_sales)::INTEGER INTO avg_daily_sales
    FROM (
        SELECT COUNT(*) as daily_sales
        FROM order_items oi
        JOIN orders o ON oi.order_id = o.order_id
        WHERE oi.product_id = calculate_dynamic_price.product_id
            AND o.order_date >= CURRENT_DATE - INTERVAL '30 days'
        GROUP BY DATE(o.order_date)
    ) daily_stats;
    
    -- Calculate demand multiplier based on recent sales
    IF avg_daily_sales > 10 THEN
        demand_multiplier := 1.2;
    ELSIF avg_daily_sales > 5 THEN
        demand_multiplier := 1.1;
    ELSIF avg_daily_sales < 1 THEN
        demand_multiplier := 0.9;
    END IF;
    
    -- Calculate inventory multiplier
    IF current_inventory < avg_daily_sales * 7 THEN
        inventory_multiplier := 1.15; -- Low stock premium
    ELSIF current_inventory > avg_daily_sales * 30 THEN
        inventory_multiplier := 0.95; -- Excess stock discount
    END IF;
    
    -- Customer segment multiplier
    customer_multiplier := CASE customer_segment
        WHEN 'premium' THEN 1.1
        WHEN 'vip' THEN 1.05
        WHEN 'budget' THEN 0.95
        ELSE 1.0
    END;
    
    -- Seasonal multiplier
    seasonal_multiplier := CASE season
        WHEN 'peak' THEN 1.25
        WHEN 'holiday' THEN 1.3
        WHEN 'off_season' THEN 0.85
        ELSE 1.0
    END;
    
    -- Calculate final price
    final_price := base_price * demand_multiplier * inventory_multiplier * 
                   customer_multiplier * seasonal_multiplier;
    
    -- Ensure price doesn't go below cost or above maximum markup
    SELECT 
        GREATEST(
            cost_price * 1.1, -- Minimum 10% markup
            LEAST(final_price, base_price * 2.0) -- Maximum 100% markup
        ) INTO final_price
    FROM products 
    WHERE product_id = calculate_dynamic_price.product_id;
    
    RETURN ROUND(final_price, 2);
END;
$ LANGUAGE plpgsql;

-- Usage example
SELECT 
    product_name,
    base_price,
    calculate_dynamic_price(base_price, product_id, 'premium', 'peak') as dynamic_price
FROM products
LIMIT 5;
```

### Q102: Advanced inventory management
```sql
CREATE OR REPLACE FUNCTION optimize_inventory_levels()
RETURNS TABLE (
    product_id INTEGER,
    product_name VARCHAR(100),
    current_stock INTEGER,
    optimal_stock_level INTEGER,
    reorder_point INTEGER,
    economic_order_quantity INTEGER,
    action_needed VARCHAR(50),
    priority_score INTEGER
) AS $
BEGIN
    RETURN QUERY
    WITH sales_analysis AS (
        SELECT 
            p.product_id,
            p.product_name,
            COALESCE(AVG(daily_sales.sales), 0) as avg_daily_sales,
            COALESCE(STDDEV(daily_sales.sales), 0) as sales_stddev,
            p.cost_price,
            p.carrying_cost_pct,
            p.order_cost
        FROM products p
        LEFT JOIN (
            SELECT 
                oi.product_id,
                DATE(o.order_date) as sale_date,
                SUM(oi.quantity) as sales
            FROM order_items oi
            JOIN orders o ON oi.order_id = o.order_id
            WHERE o.order_date >= CURRENT_DATE - INTERVAL '90 days'
            GROUP BY oi.product_id, DATE(o.order_date)
        ) daily_sales ON p.product_id = daily_sales.product_id
        GROUP BY p.product_id, p.product_name, p.cost_price, p.carrying_cost_pct, p.order_cost
    ),
    inventory_optimization AS (
        SELECT 
            sa.*,
            i.stock_quantity as current_stock,
            -- Safety stock (2 standard deviations)
            CEILING(sa.sales_stddev * 2) as safety_stock,
            -- Reorder point (lead time demand + safety stock)
            CEILING(sa.avg_daily_sales * 7 + sa.sales_stddev * 2) as reorder_point,
            -- Economic Order Quantity (EOQ)
            CASE 
                WHEN sa.carrying_cost_pct > 0 AND sa.avg_daily_sales > 0 THEN
                    CEILING(SQRT(2 * sa.avg_daily_sales * 365 * sa.order_cost / 
                                (sa.cost_price * sa.carrying_cost_pct / 100)))
                ELSE 30 -- Default minimum order quantity
            END as eoq,
            -- Optimal stock level (EOQ + Safety stock)
            CASE 
                WHEN sa.carrying_cost_pct > 0 AND sa.avg_daily_sales > 0 THEN
                    CEILING(SQRT(2 * sa.avg_daily_sales * 365 * sa.order_cost / 
                                (sa.cost_price * sa.carrying_cost_pct / 100))) +
                    CEILING(sa.sales_stddev * 2)
                ELSE 50 -- Default stock level
            END as optimal_stock
        FROM sales_analysis sa
        JOIN inventory i ON sa.product_id = i.product_id
    )
    SELECT 
        io.product_id,
        io.product_name,
        io.current_stock,
        io.optimal_stock,
        io.reorder_point,
        io.eoq,
        CASE 
            WHEN io.current_stock <= io.reorder_point THEN 'REORDER NOW'
            WHEN io.current_stock > io.optimal_stock * 1.5 THEN 'EXCESS STOCK'
            WHEN io.current_stock < io.optimal_stock * 0.8 THEN 'LOW STOCK'
            ELSE 'OPTIMAL'
        END,
        CASE 
            WHEN io.current_stock <= io.reorder_point THEN 1
            WHEN io.current_stock < io.optimal_stock * 0.8 THEN 2
            WHEN io.current_stock > io.optimal_stock * 1.5 THEN 3
            ELSE 4
        END
    FROM inventory_optimization io
    ORDER BY 
        CASE 
            WHEN io.current_stock <= io.reorder_point THEN 1
            WHEN io.current_stock < io.optimal_stock * 0.8 THEN 2
            WHEN io.current_stock > io.optimal_stock * 1.5 THEN 3
            ELSE 4
        END,
        io.avg_daily_sales DESC;
END;
$ LANGUAGE plpgsql;

-- Usage
SELECT * FROM optimize_inventory_levels()
WHERE action_needed != 'OPTIMAL'
LIMIT 20;
```

## 42. Final Advanced Concepts

### Q103: Multi-dimensional data analysis
```sql
-- Advanced OLAP-style query with multiple dimensions
WITH sales_cube AS (
    SELECT 
        EXTRACT(YEAR FROM o.order_date) as year,
        EXTRACT(QUARTER FROM o.order_date) as quarter,
        r.region_name,
        p.category,
        c.customer_segment,
        SUM(oi.quantity * oi.unit_price) as revenue,
        SUM(oi.quantity) as units_sold,
        COUNT(DISTINCT o.order_id) as order_count,
        COUNT(DISTINCT o.customer_id) as unique_customers
    FROM orders o
    JOIN order_items oi ON o.order_id = oi.order_id
    JOIN products p ON oi.product_id = p.product_id
    JOIN customers c ON o.customer_id = c.customer_id
    JOIN regions r ON c.region_id = r.region_id
    WHERE o.order_date >= '2023-01-01'
    GROUP BY CUBE(
        EXTRACT(YEAR FROM o.order_date),
        EXTRACT(QUARTER FROM o.order_date),
        r.region_name,
        p.category,
        c.customer_segment
    )
)
SELECT 
    COALESCE(year::TEXT, 'ALL YEARS') as year,
    COALESCE(quarter::TEXT, 'ALL QUARTERS') as quarter,
    COALESCE(region_name, 'ALL REGIONS') as region,
    COALESCE(category, 'ALL CATEGORIES') as category,
    COALESCE(customer_segment, 'ALL SEGMENTS') as segment,
    revenue,
    units_sold,
    order_count,
    unique_customers,
    ROUND(revenue / NULLIF(units_sold, 0), 2) as avg_unit_price,
    ROUND(revenue / NULLIF(order_count, 0), 2) as avg_order_value,
    ROUND(revenue / NULLIF(unique_customers, 0), 2) as revenue_per_customer,
    -- Ranking within each dimension
    ROW_NUMBER() OVER (PARTITION BY year, quarter ORDER BY revenue DESC) as revenue_rank
FROM sales_cube
WHERE revenue IS NOT NULL
ORDER BY year NULLS LAST, quarter NULLS LAST, revenue DESC;
```

### Q104: Advanced data science query
```sql
-- Customer Lifetime Value prediction using cohort analysis and linear regression
WITH monthly_cohorts AS (
    SELECT 
        customer_id,
        DATE_TRUNC('month', MIN(order_date)) as cohort_month,
        MIN(order_date) as first_purchase_date
    FROM orders
    GROUP BY customer_id
),
customer_monthly_activity AS (
    SELECT 
        mc.customer_id,
        mc.cohort_month,
        DATE_TRUNC('month', o.order_date) as activity_month,
        EXTRACT(EPOCH FROM (DATE_TRUNC('month', o.order_date) - mc.cohort_month))/2592000 as period_number,
        SUM(o.amount) as monthly_revenue,
        COUNT(o.order_id) as monthly_orders
    FROM monthly_cohorts mc
    JOIN orders o ON mc.customer_id = o.customer_id
    GROUP BY mc.customer_id, mc.cohort_month, DATE_TRUNC('month', o.order_date)
),
customer_metrics AS (
    SELECT 
        customer_id,
        cohort_month,
        MAX(period_number) as customer_age_months,
        SUM(monthly_revenue) as total_revenue,
        SUM(monthly_orders) as total_orders,
        AVG(monthly_revenue) as avg_monthly_revenue,
        COUNT(DISTINCT activity_month) as active_months
    FROM customer_monthly_activity
    GROUP BY customer_id, cohort_month
),
clv_calculation AS (
    SELECT 
        cm.*,
        -- Calculate predicted CLV using simplified formula
        CASE 
            WHEN cm.customer_age_months > 0 THEN
                cm.avg_monthly_revenue * 
                (cm.active_months::FLOAT / cm.customer_age_months) * 
                24 -- Predict 24 months forward
            ELSE cm.total_revenue
        END as predicted_clv,
        -- Customer health score
        CASE 
            WHEN cm.customer_age_months >= 12 AND cm.active_months >= 6 THEN 'Healthy'
            WHEN cm.customer_age_months >= 6 AND cm.active_months >= 3 THEN 'Moderate'
            WHEN cm.customer_age_months >= 3 AND cm.active_months >= 2 THEN 'New'
            ELSE 'At Risk'
        END as health_status
    FROM customer_metrics cm
)
SELECT 
    cohort_month,
    health_status,
    COUNT(*) as customer_count,
    ROUND(AVG(total_revenue), 2) as avg_historical_clv,
    ROUND(AVG(predicted_clv), 2) as avg_predicted_clv,
    ROUND(AVG(customer_age_months), 1) as avg_customer_age_months,
    ROUND(AVG(active_months::FLOAT / NULLIF(customer_age_months, 0)) * 100, 1) as avg_activity_rate_pct,
    ROUND(SUM(predicted_clv), 2) as total_predicted_value
FROM clv_calculation
GROUP BY cohort_month, health_status
ORDER BY cohort_month DESC, 
    CASE health_status 
        WHEN 'Healthy' THEN 1 
        WHEN 'Moderate' THEN 2 
        WHEN 'New' THEN 3 
        ELSE 4 
    END;
```

### Q105: Final comprehensive system monitoring query
```sql
-- Comprehensive database health and performance monitoring
CREATE OR REPLACE FUNCTION system_health_report()
RETURNS TABLE (
    category VARCHAR(50),
    metric VARCHAR(100),
    current_value TEXT,
    status VARCHAR(20),
    recommendation TEXT
) AS $
BEGIN
    -- Connection metrics
    RETURN QUERY
    SELECT 
        'Connections'::VARCHAR(50),
        'Active Connections'::VARCHAR(100),
        COUNT(*)::TEXT,
        CASE WHEN COUNT(*) > 80 THEN 'WARNING' ELSE 'OK' END,
        CASE WHEN COUNT(*) > 80 THEN 'Consider connection pooling' ELSE 'Connection count is healthy' END
    FROM pg_stat_activity 
    WHERE state = 'active';
    
    -- Database size metrics
    RETURN QUERY
    SELECT 
        'Storage'::VARCHAR(50),
        'Database Size'::VARCHAR(100),
        pg_size_pretty(pg_database_size(current_database())),
        'INFO'::VARCHAR(20),
        'Monitor growth trends'::TEXT;
    
    -- Lock metrics
    RETURN QUERY
    SELECT 
        'Locks'::VARCHAR(50),
        'Blocked Queries'::VARCHAR(100),
        COUNT(*)::TEXT,
        CASE WHEN COUNT(*) > 0 THEN 'WARNING' ELSE 'OK' END,
        CASE WHEN COUNT(*) > 0 THEN 'Investigate blocking queries' ELSE 'No blocked queries' END
    FROM pg_locks l1
    JOIN pg_locks l2 ON l1.transactionid = l2.transactionid
    WHERE l1.granted = FALSE AND l2.granted = TRUE;
    
    -- Index usage
    RETURN QUERY
    WITH index_stats AS (
        SELECT 
            COUNT(*) as total_indexes,
            COUNT(*) FILTER (WHERE idx_scan = 0) as unused_indexes
        FROM pg_stat_user_indexes
    )
    SELECT 
        'Performance'::VARCHAR(50),
        'Unused Indexes'::VARCHAR(100),
        unused_indexes || '/' || total_indexes,
        CASE WHEN unused_indexes::FLOAT/total_indexes > 0.2 THEN 'WARNING' ELSE 'OK' END,
        CASE WHEN unused_indexes::FLOAT/total_indexes > 0.2 
             THEN 'Consider dropping unused indexes' 
             ELSE 'Index usage is good' END
    FROM index_stats;
    
    -- Long running queries
    RETURN QUERY
    SELECT 
        'Performance'::VARCHAR(50),
        'Long Running Queries'::VARCHAR(100),
        COUNT(*)::TEXT,
        CASE WHEN COUNT(*) > 5 THEN 'WARNING' ELSE 'OK' END,
        CASE WHEN COUNT(*) > 5 THEN 'Investigate slow queries' ELSE 'Query performance is good' END
    FROM pg_stat_activity
    WHERE state = 'active' 
        AND query_start < NOW() - INTERVAL '5 minutes'
        AND query NOT ILIKE '%pg_stat_activity%';
        
    -- Cache hit ratio
    RETURN QUERY
    WITH cache_stats AS (
        SELECT 
            SUM(heap_blks_hit) as hits,
            SUM(heap_blks_read) as reads
        FROM pg_statio_user_tables
    )
    SELECT 
        'Performance'::VARCHAR(50),
        'Buffer Cache Hit Ratio'::VARCHAR(100),
        ROUND(100.0 * hits / NULLIF(hits + reads, 0), 2)::TEXT || '%',
        CASE WHEN hits::FLOAT / NULLIF(hits + reads, 0) < 0.95 THEN 'WARNING' ELSE 'OK' END,
        CASE WHEN hits::FLOAT / NULLIF(hits + reads, 0) < 0.95 
             THEN 'Consider increasing shared_buffers' 
             ELSE 'Cache performance is good' END
    FROM cache_stats;
END;
$ LANGUAGE plpgsql;

-- Final usage example
SELECT * FROM system_health_report();
```

## Summary

This comprehensive collection covers 105+ PostgreSQL interview questions with SQL queries suitable for professionals with 5+ years of experience. The topics include:

1. **Advanced SELECT queries** - Complex filtering, aggregation, and data retrieval
2. **Window functions** - Ranking, running totals, and analytical functions
3. **CTEs and recursive queries** - Hierarchical data and complex data transformations
4. **Advanced JOINs** - Multiple table operations and optimization
5. **Date/Time functions** - Complex temporal calculations
6. **JSON and Array operations** - Modern PostgreSQL data types
7. **Performance optimization** - Indexing, query tuning, and monitoring
8. **Advanced aggregations** - Statistical functions and custom aggregates
9. **Data modification** - Complex INSERT, UPDATE, DELETE operations
10. **Functions and procedures** - Custom business logic implementation
11. **Triggers and automation** - Data integrity and audit trails
12. **Partitioning and scaling** - Large dataset management
13. **Full-text search** - Advanced search capabilities
14. **Analytics and BI** - Business intelligence queries
15. **Security and compliance** - Data protection and audit
16. **Database administration** - Monitoring and maintenance
17. **Real-time analytics** - Streaming and live data analysis
18. **Machine learning** - Data science applications in SQL
19. **Advanced business logic** - Complex domain-specific algorithms

These questions test deep PostgreSQL knowledge including performance optimization, advanced SQL features, database design, and real-world problem-solving scenarios that senior developers and database professionals encounter in production environments.
