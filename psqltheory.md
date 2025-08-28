# 100+ PostgreSQL Questions and Answers

## Basic Concepts (Questions 1-20)

### 1. What is PostgreSQL?
PostgreSQL is an open-source, object-relational database management system (ORDBMS) that emphasizes extensibility and SQL compliance. It supports both relational and non-relational data types.

### 2. What are the main advantages of PostgreSQL over other databases?
- ACID compliance
- Support for complex data types (JSON, arrays, geometric types)
- Extensibility through custom functions and operators
- Strong community support
- Cross-platform compatibility
- Advanced indexing techniques

### 3. What is the difference between PostgreSQL and MySQL?
PostgreSQL is more SQL-compliant, supports complex data types, has better support for concurrent writes, and offers more advanced features like window functions, CTEs, and full-text search. MySQL is generally faster for simple read operations but less feature-rich.

### 4. What are the basic data types in PostgreSQL?
- Numeric types: INTEGER, BIGINT, DECIMAL, NUMERIC, REAL, DOUBLE PRECISION
- Character types: CHAR, VARCHAR, TEXT
- Date/Time types: DATE, TIME, TIMESTAMP, INTERVAL
- Boolean type: BOOLEAN
- Binary types: BYTEA
- Special types: JSON, JSONB, UUID, ARRAY

### 5. What is the difference between CHAR, VARCHAR, and TEXT?
- CHAR(n): Fixed-length, padded with spaces
- VARCHAR(n): Variable-length with maximum limit
- TEXT: Variable-length without limit (preferred in PostgreSQL)

### 6. What is a primary key?
A primary key is a column or combination of columns that uniquely identifies each row in a table. It cannot contain NULL values and must be unique across all rows.

### 7. What is a foreign key?
A foreign key is a column or combination of columns that references the primary key of another table, establishing a link between tables and enforcing referential integrity.

### 8. What is the difference between DELETE and TRUNCATE?
- DELETE removes rows based on conditions, can be rolled back, fires triggers, and is slower
- TRUNCATE removes all rows quickly, cannot be rolled back (in most cases), doesn't fire triggers, and resets auto-increment counters

### 9. What is a database schema?
A schema is a logical container that holds database objects like tables, views, functions, and indexes. It provides a way to organize objects and control access.

### 10. What are constraints in PostgreSQL?
Constraints are rules enforced on data columns to ensure data integrity:
- NOT NULL: Prevents null values
- UNIQUE: Ensures uniqueness
- PRIMARY KEY: Combination of NOT NULL and UNIQUE
- FOREIGN KEY: Maintains referential integrity
- CHECK: Custom validation rules

### 11. What is the purpose of the SERIAL data type?
SERIAL is an auto-incrementing integer type used for generating unique identifiers automatically. It's equivalent to creating an INTEGER column with a DEFAULT value from a sequence.

### 12. What is a sequence in PostgreSQL?
A sequence is a database object that generates a series of unique numeric values, commonly used for auto-incrementing primary keys.

### 13. What is the difference between INNER JOIN and OUTER JOIN?
- INNER JOIN returns only matching rows from both tables
- OUTER JOIN (LEFT, RIGHT, FULL) returns matching rows plus unmatched rows from one or both tables, filling missing values with NULL

### 14. What is a view?
A view is a virtual table based on the result of a query. It doesn't store data physically but provides a way to simplify complex queries and control data access.

### 15. What is an index?
An index is a database object that improves query performance by creating a separate structure that points to the actual data rows, similar to an index in a book.

### 16. What is the difference between clustered and non-clustered indexes?
PostgreSQL doesn't have traditional clustered indexes like SQL Server. However, you can use CLUSTER command to physically reorder table data based on an index.

### 17. What is a transaction?
A transaction is a sequence of database operations that are treated as a single unit of work. It follows ACID properties (Atomicity, Consistency, Isolation, Durability).

### 18. What are the ACID properties?
- Atomicity: All operations succeed or all fail
- Consistency: Database remains in valid state
- Isolation: Concurrent transactions don't interfere
- Durability: Committed changes persist even after system failure

### 19. What is the purpose of COMMIT and ROLLBACK?
- COMMIT saves all changes made in the current transaction
- ROLLBACK undoes all changes made in the current transaction

### 20. What is a stored procedure?
A stored procedure is a set of SQL statements stored in the database that can be executed as a single unit. In PostgreSQL, these are called functions.

## Intermediate Concepts (Questions 21-60)

### 21. What is the difference between UNION and UNION ALL?
- UNION removes duplicate rows and sorts the result
- UNION ALL keeps all rows including duplicates and is faster

### 22. What are window functions?
Window functions perform calculations across a set of rows related to the current row without grouping the result set, using OVER clause.

### 23. What is the difference between RANK() and DENSE_RANK()?
- RANK() leaves gaps in ranking when there are ties
- DENSE_RANK() doesn't leave gaps in ranking

### 24. What is a Common Table Expression (CTE)?
A CTE is a temporary named result set that exists only within a single query execution, defined using WITH clause.

### 25. What is the difference between HAVING and WHERE?
- WHERE filters rows before grouping
- HAVING filters groups after GROUP BY operation

### 26. What are aggregate functions?
Functions that perform calculations on multiple rows and return a single value, like SUM(), COUNT(), AVG(), MIN(), MAX().

### 27. What is the purpose of GROUP BY?
GROUP BY groups rows with the same values in specified columns into summary rows, typically used with aggregate functions.

### 28. What is a subquery?
A subquery is a query nested inside another query, used to provide data for the main query's conditions or calculations.

### 29. What is the difference between correlated and non-correlated subqueries?
- Correlated subquery references columns from the outer query
- Non-correlated subquery is independent and executes once

### 30. What is normalization?
Normalization is the process of organizing database tables to reduce redundancy and improve data integrity through normal forms.

### 31. What are the different normal forms?
- 1NF: Atomic values, no repeating groups
- 2NF: 1NF + no partial dependencies
- 3NF: 2NF + no transitive dependencies
- BCNF: 3NF + every determinant is a candidate key

### 32. What is denormalization?
Denormalization is intentionally introducing redundancy to improve query performance, trading storage space and update complexity for read speed.

### 33. What is a trigger?
A trigger is a special stored procedure that automatically executes in response to specific database events like INSERT, UPDATE, or DELETE.

### 34. What are the different types of triggers?
- BEFORE triggers: Execute before the triggering event
- AFTER triggers: Execute after the triggering event
- INSTEAD OF triggers: Used with views to handle modifications

### 35. What is the difference between CASE and COALESCE?
- CASE provides conditional logic with multiple conditions
- COALESCE returns the first non-NULL value from a list

### 36. What is the NULLIF function?
NULLIF returns NULL if two expressions are equal, otherwise returns the first expression.

### 37. What are the different isolation levels in PostgreSQL?
- READ UNCOMMITTED
- READ COMMITTED (default)
- REPEATABLE READ
- SERIALIZABLE

### 38. What is a deadlock?
A deadlock occurs when two or more transactions are waiting for each other to release resources, creating a circular dependency.

### 39. How does PostgreSQL handle concurrency?
PostgreSQL uses Multi-Version Concurrency Control (MVCC) to allow multiple transactions to access the same data simultaneously without locking.

### 40. What is MVCC?
Multi-Version Concurrency Control maintains multiple versions of data to allow concurrent access without locking, improving performance.

### 41. What are the different types of locks in PostgreSQL?
- Table locks: ACCESS SHARE, ROW SHARE, ROW EXCLUSIVE, etc.
- Row locks: FOR UPDATE, FOR NO KEY UPDATE, FOR SHARE, FOR KEY SHARE

### 42. What is the difference between optimistic and pessimistic locking?
- Optimistic locking assumes conflicts are rare and checks at commit time
- Pessimistic locking prevents conflicts by acquiring locks early

### 43. What is a savepoint?
A savepoint is a point within a transaction to which you can roll back without rolling back the entire transaction.

### 44. What is the purpose of EXPLAIN?
EXPLAIN shows the execution plan PostgreSQL will use for a query, helping with performance optimization.

### 45. What is the difference between EXPLAIN and EXPLAIN ANALYZE?
- EXPLAIN shows the planned execution without running the query
- EXPLAIN ANALYZE actually executes the query and shows real statistics

### 46. What are materialized views?
Materialized views are views that physically store the result set, can be refreshed periodically, and improve performance for complex queries.

### 47. What is the difference between a view and a materialized view?
- Views are virtual and execute the underlying query each time
- Materialized views store actual data and need manual or scheduled refresh

### 48. What is partitioning?
Partitioning divides large tables into smaller, more manageable pieces based on certain criteria while appearing as a single table to applications.

### 49. What are the types of partitioning in PostgreSQL?
- Range partitioning: Based on value ranges
- List partitioning: Based on specific values
- Hash partitioning: Based on hash function

### 50. What is the purpose of VACUUM?
VACUUM reclaims storage space from deleted or updated rows and updates statistics for the query planner.

### 51. What is the difference between VACUUM and VACUUM FULL?
- VACUUM reclaims space but doesn't compact the table
- VACUUM FULL compacts the table by rewriting it entirely (requires exclusive lock)

### 52. What is ANALYZE?
ANALYZE collects statistics about table contents to help the query planner choose optimal execution plans.

### 53. What is connection pooling?
Connection pooling manages a cache of database connections that can be reused across multiple requests, reducing connection overhead.

### 54. What are the benefits of connection pooling?
- Reduces connection establishment overhead
- Limits maximum concurrent connections
- Improves application performance
- Better resource management

### 55. What is PgBouncer?
PgBouncer is a lightweight connection pooler for PostgreSQL that manages client connections efficiently.

### 56. What is the difference between functions and procedures in PostgreSQL?
PostgreSQL primarily uses functions (which can return values) and procedures (introduced in version 11, which cannot return values but support transaction control).

### 57. What are the different procedural languages supported by PostgreSQL?
- PL/pgSQL (default)
- PL/Python
- PL/Perl
- PL/Tcl
- PL/Java

### 58. What is PL/pgSQL?
PL/pgSQL is PostgreSQL's native procedural language that extends SQL with control structures, variables, and exception handling.

### 59. What are domains in PostgreSQL?
Domains are user-defined data types based on existing types with additional constraints, providing a way to standardize column definitions.

### 60. What is the purpose of LISTEN and NOTIFY?
LISTEN and NOTIFY provide a simple messaging system for PostgreSQL sessions to communicate asynchronously.

## Advanced Concepts (Questions 61-100+)

### 61. What is logical replication?
Logical replication replicates data changes based on their logical representation (not physical), allowing selective replication and cross-version compatibility.

### 62. What is streaming replication?
Streaming replication continuously streams WAL records from primary to standby servers, providing near real-time replication.

### 63. What is the difference between synchronous and asynchronous replication?
- Synchronous replication waits for standby confirmation before committing
- Asynchronous replication doesn't wait, providing better performance but potential data loss

### 64. What is a hot standby?
A hot standby is a standby server that can accept read-only queries while continuously applying changes from the primary server.

### 65. What is WAL (Write-Ahead Logging)?
WAL is a logging mechanism where changes are written to a log file before being applied to data files, ensuring crash recovery.

### 66. What are the benefits of WAL?
- Crash recovery capability
- Point-in-time recovery
- Replication support
- Improved performance for certain workloads

### 67. What is point-in-time recovery (PITR)?
PITR allows restoring a database to any specific point in time using base backups and WAL archives.

### 68. What are the different backup methods in PostgreSQL?
- Logical backups (pg_dump, pg_dumpall)
- Physical backups (file system level, pg_basebackup)
- Continuous archiving with PITR

### 69. What is the difference between pg_dump and pg_basebackup?
- pg_dump creates logical backups (SQL statements)
- pg_basebackup creates physical backups (binary copies of data directory)

### 70. What are tablespaces?
Tablespaces define locations where database objects are stored, allowing database administrators to control disk layout.

### 71. What is the shared_buffers parameter?
shared_buffers determines how much memory PostgreSQL uses for caching data pages in shared memory.

### 72. What is the work_mem parameter?
work_mem specifies the amount of memory used by internal sort operations and hash tables before writing to temporary disk files.

### 73. What is the checkpoint process?
Checkpointing is the process of writing dirty buffers to disk and recording the checkpoint location, ensuring crash recovery consistency.

### 74. What are the different join algorithms in PostgreSQL?
- Nested Loop Join
- Hash Join
- Merge Join

### 75. When does PostgreSQL choose each join algorithm?
- Nested Loop: Small result sets or when indexes are available
- Hash Join: When one table is much smaller than the other
- Merge Join: When both tables are sorted on join columns

### 76. What is the purpose of pg_stat_statements?
pg_stat_statements is an extension that tracks execution statistics of all SQL statements executed by a server.

### 77. What are partial indexes?
Partial indexes are indexes built on a subset of rows that satisfy a WHERE condition, reducing index size and maintenance cost.

### 78. What are expression indexes?
Expression indexes are built on the result of an expression or function rather than simple column values.

### 79. What are the different index types in PostgreSQL?
- B-tree (default): Good for equality and range queries
- Hash: Only for equality comparisons
- GIN: For complex data types like arrays, JSON
- GiST: For geometric data and full-text search
- SP-GiST: For non-balanced data structures
- BRIN: For very large tables with natural ordering

### 80. When would you use a GIN index?
GIN indexes are useful for columns containing multiple values like arrays, JSON documents, or full-text search.

### 81. What is a composite index?
A composite index is an index on multiple columns, useful for queries that filter or sort on multiple columns.

### 82. What is index-only scan?
An index-only scan retrieves all required data directly from the index without accessing the table, improving performance.

### 83. What are statistics in PostgreSQL?
Statistics are metadata about table contents (histograms, most common values, etc.) used by the query planner to choose optimal execution plans.

### 84. What is the purpose of pg_stat_user_tables?
pg_stat_user_tables provides statistics about table access patterns, including sequential scans, index scans, and tuple modifications.

### 85. What are foreign data wrappers (FDW)?
FDWs allow PostgreSQL to access and query data stored in external data sources as if they were local tables.

### 86. What are some common FDWs?
- postgres_fdw: Access other PostgreSQL servers
- file_fdw: Read CSV files
- dblink: Legacy method for cross-database queries

### 87. What is row-level security (RLS)?
RLS allows defining policies that restrict which rows users can view or modify based on user identity or role.

### 88. What are security policies?
Security policies are rules that determine which rows are visible or modifiable for specific roles when RLS is enabled.

### 89. What is the difference between PERMISSIVE and RESTRICTIVE policies?
- PERMISSIVE policies use OR logic (more permissive as more are added)
- RESTRICTIVE policies use AND logic (more restrictive as more are added)

### 90. What are extensions in PostgreSQL?
Extensions are packages that add functionality to PostgreSQL, including new data types, functions, operators, and index types.

### 91. What are some popular PostgreSQL extensions?
- PostGIS: Geographic information systems
- pg_crypto: Cryptographic functions
- hstore: Key-value store
- uuid-ossp: UUID generation functions

### 92. What is JSONB?
JSONB is a binary representation of JSON data that supports indexing and efficient querying, preferred over JSON type.

### 93. What is the difference between JSON and JSONB?
- JSON stores exact text representation
- JSONB stores in binary format, supports indexing, faster processing, but loses whitespace and key ordering

### 94. How do you query JSONB data?
Using operators like ->, ->>, #>, @>, ? and functions like jsonb_extract_path, jsonb_array_elements.

### 95. What are arrays in PostgreSQL?
PostgreSQL supports arrays of any data type, allowing storage of multiple values in a single column.

### 96. What is a recursive CTE?
A recursive CTE is a CTE that references itself, useful for hierarchical data like organizational charts or tree structures.

### 97. What is the LATERAL keyword?
LATERAL allows a subquery to reference columns from preceding tables in the FROM clause, enabling more complex joins.

### 98. What are window frames?
Window frames define which rows within a partition are considered for window function calculations using ROWS or RANGE clauses.

### 99. What is the difference between ROW_NUMBER(), RANK(), and DENSE_RANK()?
- ROW_NUMBER(): Sequential numbering without gaps
- RANK(): Ranking with gaps after ties
- DENSE_RANK(): Ranking without gaps after ties

### 100. What is parallel query execution?
PostgreSQL can execute certain queries using multiple worker processes in parallel, improving performance for large data sets.

### 101. What parameters control parallel execution?
- max_parallel_workers: Maximum parallel workers system-wide
- max_parallel_workers_per_gather: Maximum workers per query
- parallel_tuple_cost: Cost of processing a tuple in parallel

### 102. What is autovacuum?
Autovacuum is a background process that automatically runs VACUUM and ANALYZE operations to maintain database health.

### 103. What are the key autovacuum parameters?
- autovacuum_vacuum_threshold: Minimum number of updated/deleted rows
- autovacuum_analyze_threshold: Minimum number of modified rows for ANALYZE
- autovacuum_vacuum_scale_factor: Fraction of table size

### 104. What is bloat in PostgreSQL?
Bloat refers to unused space in tables and indexes caused by UPDATE and DELETE operations, which MVCC doesn't immediately reclaim.

### 105. How do you monitor and reduce bloat?
Monitor using pg_stat_user_tables and queries for bloat estimation. Reduce using VACUUM, REINDEX, or pg_repack extension.

### 106. What is the purpose of pg_repack?
pg_repack is an extension that rebuilds tables and indexes online without blocking concurrent operations, eliminating bloat.

### 107. What are advisory locks?
Advisory locks are application-level locks that don't lock any database objects but provide a mechanism for applications to coordinate access to resources.

### 108. What is the difference between exclusive and shared advisory locks?
- Exclusive advisory locks conflict with all other locks on the same resource
- Shared advisory locks only conflict with exclusive locks

### 109. What are custom data types?
PostgreSQL allows creating custom data types using CREATE TYPE, including composite types, enums, and domains.

### 110. What are enum types?
Enum types are user-defined data types with a static set of values, providing type safety and better performance than text constraints.
