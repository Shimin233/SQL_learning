## Implicit Join Syntax
```mysql
--Recap: we have learned the following
SELECT *
FROM orders o
JOIN customers c
  ON o.customer_id = c.customer_id;
  
-- equivalent (but not recommended) way: Implicit Join Syntax
SELECT *
FROM orders o, customers c
WHERE o.customer_id = c.customer_id
-- get 10 rows here

-- if accidently not typing WHERE here, 
SELECT *
FROM orders o, customers c
-- then will get ~100 rows,
-- as each record in o is joined with each record in c (cross turn?)
-- Instead, JOIN...ON... forces you to type the join condition

```
## Outer Joins
```mysql
-- (INNER) JOIN and OUTER JOIN; today we look at OUTER JOIN
SELECT 
  c.customer_id,
  c.first_name,
  o.order_id
FROM orders o
JOIN customers c
  ON o.customer_id = c.customer_id
ORDER BY c.customer_id; 

-- the result from above only cover the customers with orders
--  but we want customers both with /without orders

-- So we use OUTER JOIN, which has two types: LEFT and RIGHT JOIN
-- LEFT JOIN: according to the 'left' table (orders o), JOIN the other table to it
-- so only show those with orders, same as (INNER) JOIN before
SELECT 
  c.customer_id,
  c.first_name,
  o.order_id
FROM orders o
LEFT OUTER JOIN customers c  -- Or simply: LEFT JOIN
  ON o.customer_id = c.customer_id
ORDER BY c.customer_id; 

-- RIGHT JOIN: according to the 'right' table (customers c), JOIN the other table to it
-- so get all the customers, no matter with/without orders
SELECT 
  c.customer_id,
  c.first_name,
  o.order_id
FROM orders o
RIGHT OUTER JOIN customers c  -- Or simply: RIGHT JOIN
  ON o.customer_id = c.customer_id
ORDER BY c.customer_id; 

-- Swap orders to input tables to swap results
SELECT 
  c.customer_id,
  c.first_name,
  o.order_id
FROM customers c
RIGHT JOIN orders o
  ON o.customer_id = c.customer_id
ORDER BY c.customer_id; 
```

### Ex

```mysql
-- want to show col's: product_id, name, quantity
-- want to show all products with id and names, no matter thayhave quantity or not

SELECT 
  p.product_id, 
  p.name, 
  oi.quantity
FROM porducts p 
LEFT JOIN order_items oi
  ON p.product_id = oi.product_id
  

```
## Outer Join Multiple Tables
```mysql
SELECT 
  c.customer_id,
  c.first_name,
  o.order_id
FROM customers c
LEFT JOIN orders o
  ON o.customer_id = c.customer_id
LEFT JOIN shippers sh -- can simply (INNER) JOIN, get only those with shippers
  ON o.shipper_id = sh.shipper_id
ORDER BY c.customer_id; 

-- Remark: better to keep using LEFT JOIN, for clarity
```

### Ex
```mysql
--  want col's: order_date, order_id, customers' first_name, shipper, status
-- no matter with or without shipper or not

SELECT 
  o.order_date, 
  o.order_id, 
  c.first_name AS customer,
  sh.name AS shipper, 
  os.name AS status
FROM orders o
JOIN customers c -- INNER/OUTER JOIN both work, as each order has a customer
  ON o.customer_id = c.customer_id
LEFT JOIN shippers sh
  ON o.shipper_id = sh.shipper_id 
JOIN order_statuses os
  ON o.status = os.order_status_id
```
