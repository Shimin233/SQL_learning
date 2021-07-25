## Self Outer Joins

```mysql
-- Recall Self Join; only those with managers are shown (CEO not shown); 
--  want every name to be shown no matter with or without manager

USE sql_hr;

SELECT 
  e.employee_id,
  e.first_name,
  m.first_name AS manager
FROM emplyees e
LEFT JOIN emplyees m
  ON e.reports_to = m.employee_id

```

## USING
```mysql
-- alternative way to type JOIN condition, 
--   but only used for col's with same name in different tables
SELECT 
  o.order_id
  c.first_name
  sh.name AS shipper
FROM orders o
JOIN customers c
  USING (customer_id)
LEFT JOIN shippers sh
  USING (shipper_id)

-- Recall: 
SELECT *
FROM order_items oi
JOIN order_item_notes oin
  ON oi.order_id = oin.order_id AND
  oi.product_id = oin.product_id
-- equivalently,
SELECT *
FROM order_items oi
JOIN order_item_notes oin
  USING (order_id, product_id)
  
```

### Ex

```mysql
-- want col's: date (invoice_date), client (name), amount, name (payment method)

USE sql_invoicing;

SELECT
  p.date AS date,
  cl.name AS client,
  p.amount,
  pm.name AS payment_method
FROM payment p
JOIN clients cl
  USING (client_id)
JOIN payment_methods pm
  ON pm.payment_method_id = p.payment_method
 
 -- Method: 1. look at what col's we want to show,
 --   pick the (minimal possible sets of) tables containing them
 -- 2. put the tables with more rows in front (more LEFT) and those with fewer rows after (more RIGHT), JOIN them;
 --   e.g. one customer may place multiple payments, one payment method is used by many diff invoices,
 --   then (LEFT <--) payment --(client_id)-- customers --(payment_method_id)-- payment_methods (--> RIGHT)
```
## Natural Joins
```mysql
-- Third way to JOIN tables based on common col's (col's with same name)
-- Not recommended for ambiguous situations 

SELECT 
  o.order_id,
  c.first_name
FROM orders o
NATURAL JOIN customers c
-- MYSQL just guesses: USING customer_id, or first_name, or last_name


```
