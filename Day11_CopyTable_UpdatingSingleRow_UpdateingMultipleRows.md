## Create a Copy of a Table
```mysql
-- copy data from one table to another
CREATE TABLE orders_archived AS
SELECT * FROM orders
-- click refreshing button of Schemas to see update
-- can see this new table has no primary key, and no auto increment col

-- right click new table, truncate table
--   now this table turns empty

INSERT INTO orders_archived
SELECT *
FROM orders
WHERE order_date < '2019-01-01'
-- this is case: use SELECT as a sorting of INSERT


```

### Ex

```mysql
-- look at invoices table, 
-- those without payment date, i.e. those who has not made payment
-- pick those with payments

USE sql_invoicing;

CREATE TABLE invoices_archived AS
SELECT 
  i.invoice_id,
  i.number,
  c.client_id AS client,
  i.invoice_total,
  i.patment_total,
  i.invoice_date,
  i.payment_date,
  due_date
FROM invoices i
JOIN clients c
  USING (client_id)
WHERE i.payment_date IS NOT NULL -- Or: i.payment_date > '0000-00-00'

-- can right click a table in Schemas, drop it
```
## Updating a Single Row

```mysql
UPDATE invoices
SET payment_total = 10, payment_date='2019-03-01'
WHERE invoice_id=1

-- can turn this back: 
UPDATE invoices
SET payment_total = 0, payment_date=NULL -- Or equivalently: payment_total=DEFAULT 
WHERE invoice_id=1

-- more updating methods: 
UPDATE invoices
SET 
  payment_total = invoice_total * 0.5, 
  payment_date= due_date
WHERE invoice_id=3

```
## Updateing Multiple Rows
```mysql
-- you may want to update all the rows with client_id=3: 
UPDATE invoices
SET 
  payment_total = invoice_total * 0.5, 
  payment_date= due_date
WHERE client_id=3
-- but this will cause only one row updated; 
--   this is an error unique to MySQL Workbench.
--   To solve it, do the following:
--    Click from the menu, MYSQL Workbench, Preferences, SQL Editor,
--    Save update, close this window and re-connect
--    Now the codes above can update all the rows with client_id=3
-- Now, more methods to update multiple rows: 
UPDATE invoices
SET 
  payment_total = invoice_total * 0.5, 
  payment_date= due_date
WHERE invoice_id IN (3, 4)
```
### Ex
```mysql
-- Write a SQL statement to 
--  give any customers born before 1990 50 extra points

USE sql_store; 
UPDATE customers
SET points = points + 50
WHERE birth_date < '1990-01-01'

```
