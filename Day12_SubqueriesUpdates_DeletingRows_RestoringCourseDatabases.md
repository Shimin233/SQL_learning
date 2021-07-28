## Using Subqueries in Updates
```mysql
UPDATE invoices
SET 
  payment_total = invoice_total * 0.5
  payment_date = due_date
WHERE client_id = 3; 

SELECT client_id
FROM clients
WHERE name = 'Myworks' 
-- this latter set of codes outputs one row

-- want the latter one from above
--   to be subquery in the former set of codes
--    so that the output of the latter is the condition of choice in the former codes: 
UPDATE invoices
SET 
  payment_total = invoice_total * 0.5
  payment_date = due_date
WHERE client_id = 
    (SELECT client_id
    FROM clients
    WHERE name = 'Myworks
--   Note that the SELECT condition is looking at clients table, 
--   i.e. different table from invoices, the table to be updated
--   this is allowable as long as the SELECT-ed table and UPDATE-ed table have same col name: client_id
  
-- can select multiple col's: 
UPDATE invoices
SET 
  payment_total = invoice_total * 0.5
  payment_date = due_date
WHERE client_id IN 
    (SELECT client_id
    FROM clients
    WHERE state IN ('CA', 'NY'))
    
-- Tip: if SELECT-ed table are the same as UPDATE-ed table,
--   then we can simplify the codes: 
--    step1, confirm whether update the correct rows by running this first: 
SELECT * 
FROM invoices
WHERE payment_date IS NULL
-- step2, if correct, then put its condition into codes as subquery: 
UPDATE invoices
SET 
  payment_total = invoice_total * 0.5
  payment_date = due_date
WHERE payment_date IS NULL

```

### Ex
```mysql
-- Update comments (in table, orders) of the customers with over 3000 points
--    to be 'Gold customer'
--     and order them by

USE sql_store; -- Or: double click the database before using it
UPDATE orders
SET comments = 'Gold customer'
WHERE customer_id IN
    (SELECT customer_id
    FROM customers
    WHERE points > 3000)

```
## Deleting Rows
```mysql
-- ths below will delete everything, watch out!
DELETE FROM invoices

DELETE FROM invoices
WHERE invoice_id=1

-- can use subquery: 
SELECT *
FROM clients
WHERE name = 'Myworks'
--   combine it into DELETE FROM clause
DELETE FROM invoices
WHERE client_id = (
  SELECT *
  FROM clients
  WHERE name = 'Myworks'
  )


```
## Restoring Course Databases
```mysql
-- File menu, open sql script, click create-databases.sql, to re-build all databases in Schemas   
      
```
