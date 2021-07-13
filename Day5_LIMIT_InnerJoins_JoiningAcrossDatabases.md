## LIMIT

```mysql
SELECT *
FROM customers
LIMIT 3 -- the number of rows allowed is set to be 3

-- page 1: 1-3
-- page 2: 4-6
-- page 3: 7-9
SELECT *
FROM customers
LIMIT 6, 3 -- skip the first 6 and show the next 3

```
### Ex
```mysql
-- Get the top three loyal customers
SELECT *
FROM customers
ORDER BY points DESC
LIMIT 3 

-- Remakr, clauses always occur in certain order:
-- SELECT
-- FROM
-- WHERE
-- ORDER BY
-- LIMIT

```
## Inner Joins
```mysql
-- select col's from multiple tables
-- two types of combining tables: OUTER JOIN (later) and INNER JOIN
SELECT *
FROM orders 
INNER JOIN customers -- equivalently can type: JOIN customers
    ON orders.customer_id = customers.customer_id
    -- Here orders occurs first and customers later in the outputting form
    -- Recall in R, we merge data frames by equating col's, by.x and by.y
    --  but MySQL keeps both col's rather than combing them in one col
    
   
SELECT order_id, first_name, last_name -- pick some col's from any/both of two forms
FROM orders
JOIN customers
    ON orders.customer_id = customers.customer_id
    
-- Note the following has an ambiguous col, 
--  as the col of this name exists in two forms:     
SELECT order_id, customer_id, first_name, last_name -- customer_id is ambiguous here
FROM orders
JOIN customers
    ON orders.customer_id = customers.customer_id
-- should specify the form it belongs to:     
SELECT order_id, orders.customer_id, first_name, last_name -- the customer_id belonging to orders
FROM orders 
JOIN customers
    ON orders.customer_id = customers.customer_id 
    
-- re-name col's (alias)
--  but as long as renaming a col by some alias, 
--  cannot mix the use of original name and alias 
SELECT order_id, o.customer_id, first_name, last_name 
FROM orders o
JOIN customers c
    ON o.customer_id = c.customer_id 
```
### Ex
```mysql
-- From order_items table, and products
--  by equating product id's

SELECT order_id, oi.product_id, quantity, unit_price -- two differrnt unit prices
FROM order_items oi
JOIN products p ON oi.product_id = p.product_id

SELECT order_id, oi.product_id, quantity, oi.unit_price -- two differrnt unit prices
FROM order_items oi
JOIN products p ON oi.product_id = p.product_id

```
## Joining Across Databases
```mysql
SELECT *
FROM order_items oi
JOIN sql_inventory.products p --can pick such a sql-stored database
    ON oi.product_id=p.product_id
 
 
-- under another certain database, 
--  the forms which need databases specified has swapped
USE sql_inventory
SELECT *
FROM sql_store.order_items oi
JOIN products p --can pick such a sql-stored database
    ON oi.product_id=p.product_id
    
```

### Ex
```mysql
-- one value is used to refer to different things (in diff col's)
-- in one single table

-- can join one table with itself
USE sql_hr

SELECT * 
FROM employees e -- emplyees
JOIN employees m -- manager
    ON e.reports_to=m.employee_id
    
SELECT * 
  e.employee_id,
  e.first_name,
  m.first_name AS manager
FROM employees e -- emplyees
JOIN employees m -- manager; must use different aliases, when self-joining
    ON e.reports_to=m.employee_id
```
