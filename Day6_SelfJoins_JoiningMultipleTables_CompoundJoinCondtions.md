## Self Joins
```mysql
-- one value is used to refer to different things (in diff col's)
-- in one single table

-- can join one table with itself
USE sql_hr

SELECT * 
FROM employees e -- employees' table
JOIN employees m -- manager' table, (actually same as employees' table)
    ON e.reports_to = m.employee_id
    
SELECT  
  e.employee_id,
  e.first_name,
  m.first_name AS manager
FROM employees e -- emplyees
JOIN employees m -- manager; must use different aliases, when self-joining
    ON e.reports_to=m.employee_id
```

## Joining Multiple Tables

```mysql
-- stick two tables: order status, and 
USE sql_store;
-- step1: join three tables one-by-one: o, c and os
SELECT *
FROM orders o
JOIN customers c
    ON o.customer_id = c.customer_id
JOIN order_statuses os
    ON o.status = os.order_status_id
    -- note that although os itself has only three rows, 
    --  it will duplicate by follwoing orders o
    
-- step2: pick needed columns and rename
SELECT 
    o.order_id,
    o.order_date,
    c.first_name,
    c.last_name,
    os.name AS status
FROM orders o
JOIN customers c
    ON o.customer_id = c.customer_id
JOIN order_statuses os
    ON o.status = os.order_status_id
       

```

### Ex

```mysql
-- In the database: sql_invoicing, join the table: invoices, and
-- the tables: payments, payment_method
-- according to client_id and payment_method resp.

USE sql_invoicing; 

SELECT 
    p.payment_id, 
    i.client_id, 
    i.invoice_id, 
    date, 
    amount, 
    pm.name AS payment_method
FROM payments p 
JOIN invoices i
    ON p.client_id = p.client_id
JOIN payment_methods pm
    ON p.payment_method = pm.payment_method_id; 
    -- Remark: add ; to prepare for further coding below
-- Note that it is better to mark alias of tables that col's belong to,
--   (though I did not mark alias for all col's above)

```
## Compound Join Condtions
```mysql
-- composite primary key: more than one primary key col

-- corder_item_notes: the combination of
--   order_id and produc_id uniquely identifies each note
SELECT *
FROM order_items oi
JOIN order_item_notes oin
    ON oi.order_id = oin.order_id
    AND oi.product_id = oin.product_id -- the compound joint condition

```
