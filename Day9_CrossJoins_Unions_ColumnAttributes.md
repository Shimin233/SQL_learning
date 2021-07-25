## Cross Joins
```mysql
-- Pair each record in 1st table with each record in 2nd table
SELECT 
  c.first_name AS customer,
  p.name AS product
FROM customers c
CROSS JOIN products p
ORDER BY c.first_name
-- Equivalently in terms of result, can use implicit syntax for cross join: 
--  (but the explicit syntax above is clearer)
SELECT 
  c.first_name AS customer,
  p.name AS product
FROM customers c, products p
ORDER BY c.first_name

-- although this result seems not to make sense here
-- It can be useful; eg:
-- given table of sizes, and table of colours; want to combine all the sizes with all the colours


```


### Ex

```mysql
-- Do a cross join between shippers and products
--   usng the implicit syntax
--   and then the explicit syntax

-- Implicit syntax: 
SELECT
  p.name AS product,
  sh.name AS shiiper
FROM products p, shippers sh
ORDER BY p.name
-- Explicit syntax: 
SELECT
  p.name AS product,
  sh.name AS shiiper
FROM products p
CROSS JOIN shippers sh
ORDER BY p.name

```
## Unions
```mysql
-- UNION is to combine results from two queries into one result set
SELECT 
  order_id,
  order_date, 
  'Active' AS status
FROM orders 
WHERE order_date >= '2019-01-01'; 
UNION 
SELECT
  order_id,
  order_date, 
  'Archived' AS status
FROM orders 
WHERE order_date < '2019-01-01'

-- UNION can be used in same or across different tables
-- but it cannot combine two-col with one-col, like: 
-- SELECT first_name, last_name
-- FROM customers
-- UNION
-- SELECT name
-- FROM shippers

-- Renaming col's
SELECT first_name 
FROM customers
UNION
SELECT name AS full_name
FROM shippers

```

### Ex
```mysql
-- Want to show col's: customer_id, first_name (of customers), points, type
--  where type is defined to be Bronze, if points < 2000,
--  Silver, if points BETWEEN 2000 and 3000, gold, if over 2000

SELECT
  customer_id,
  first_name,
  points,
  'Bronze' AS type 
FROM customers
WHERE points < 2000
UNION
SELECT
  customer_id,
  first_name,
  points,
  'Silver' AS type 
FROM customers
WHERE points BTWEEN 2000 AND 3000
UNION
SELECT
  customer_id,
  first_name,
  points,
  'Gold' AS type 
FROM customers
WHERE points > 3000
ORDER BY first_name
-- note that we can order finally
```
## Column Attributes
```mysql
-- click the 2nd icon on the right of a table in Schemas sector
-- Column (its name); dataype: INT(11), integers, 
--   VARCHAR(50), variable character of maximum 50 characters length
--   CHAR(50), character of max 45 length (less space-efficient than VARCHAR)
-- PK, primary key
-- NN, NOT NULL, eg: first_name must be not NULL but birthday can be optionally NULL
-- AI, auto increment, usually used for primary key(in allowable size?)
-- Default/Expression, eg: points is by default '0'


```
