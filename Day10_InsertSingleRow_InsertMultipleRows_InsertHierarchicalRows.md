## Insert a Single Row
```mysql
INSERT INTO customers
VALUES (200)

INSERT INTO customers
VALUES (DEFAULT) -- every value in this col must be unique

INSERT INTO customers
VALUES (DEFAULT, 'John', 'Smith', NULL)

INSERT INTO customers
VALUES (
  DEFAULT, 
  'John', 
  'Smith', 
  '1990-01-01',
  NULL,
  'address',
  'city',
  'CA',
  DEFAULT)
  
INSERT INTO customers (
  first_name,
  last_name,
  birth_date,
  address,
  city,
  state)
VALUES (
  'John', 
  'Smith',
  '1990-01-01',
  'address',
  'city,
  'CA")
-- MySQL auto increments to the next row, to insert new values

```
## Insert Multiple Rows
```mysql
INSERT INTO shippers (name)
VALUES ('Shipper1'),
       ('Shipper2'),
       ('Shipper3')
-- shipper id is auto incremated

```

### Ex
```mysql
-- Insert three rows in the products table

INSERT INTO products (name, quantity_in_stock, unit_price)
VALUES ('Product1', 10, 1.95), 
       ('Product1', 10, 1.95),
       ('Product1', 10, 1.95)
       
-- MySQL will remember previously-added rows (even removed now)
--   and number new rows following them
```
## Insert Hierarchical Rows
```mysql
-- insert into multiple tables

INSERT INTO orders (customer_id, order_date, status)
VALUES (1, '2019-01-02', 1); -- must insert a valid status id in 3rd position
-- Now MySQL auto assigns order_id to this new row;
-- Use a built-in function, LAST_INSERT_ID to access it: 
INSERT INTO order_items
VALUES (LAST_INSERT_ID(), 1, 1, 2.95), 
       (LAST_INSERT_ID(), 2, 1, 3.95)

```

