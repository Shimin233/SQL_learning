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

## Updateing Multiple Rows


