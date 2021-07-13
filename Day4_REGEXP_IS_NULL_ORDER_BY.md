## REGEXP

```mysql
-- regular expression
-- last time we have: 
SELECT *
FROM customers
WHERE last_name LIKE '%field%'

-- equivalently, 
SELECT *
FROM customers
WHERER last_name REGEXP 'field'

SELECT *
FROM customers
WHERER last_name REGEXP '^field' -- beginning with field

SELECT *
FROM customers
WHERER last_name REGEXP 'field$' -- ending with field

SELECT *
FROM customers
WHERER last_name REGEXP 'field'


SELECT *
FROM customers
WHERER last_name REGEXP 'field|rose|mac' -- containing field OR rose OR mac

SELECT *
FROM customers
WHERER last_name REGEXP '^field|rose|mac' -- beginning with field OR rose OR mac
-- | can connect under ^ of the form ^(..|..); beyond $, of the form (...$)|(...$)
-- only two customers, and none of them having start as field


SELECT *
FROM customers
WHERER last_name REGEXP '[gim]e' -- containing ge OR ie OR me

SELECT *
FROM customers
WHERER last_name REGEXP 'e[fmq]' -- containing ef OR em OR eq; no result

SELECT *
FROM customers
WHERER last_name REGEXP '[a-h]e' -- containing ae OR be OR ce OR... OR he

--Recap: 
-- ^, begining
-- $, end
-- |, logical OR
-- [abcd], a sequence of OR
-- [a-f], a range of R

```

### Ex
```mysql
-- Get the customers whose
--  first names are ELKA or AMBUR
SELECT *
FROM customers
WHERE first_name = 'ELKA' OR 'AMBUR'
-- Or
SELECT *
FROM customers
WHERE first_name REGEXP 'elka|ambur'

--  last names end with EY or ON
SELECT *
FROM customers
WHERE last_name LIKE '%EY' OR '%ON'
-- Or
SELECT *
FROM customers
WHERE last_name REGEXP 'EY$|ON$'

--  last names start with MY or contains SE
SELECT *
FROM customers
WHERE last_name LIKE 'MY%' OR 'SE%'
-- Or
SELECT *
FROM customers
WHERE last_name REGXEP '^MY|SE'

--  last names contain B followed by R or U
SELECT *
FROM customers
WHERE last_name LIKE '%br%' OR '%bu%'
-- Or
SELECT *
FROM customers
WHERE last_name REGEXP 'b[ru]'
-- Or
SELECT *
FROM customers
WHERE last_name REGEXP 'br|bu'

```

## IS NULL

```mysql
-- look for those cells with NULL value
-- e.g. the customers without a phone
SELECT *
FROM customers
WHERE phone IS NULL

-- the customers with a phone
SELECT *
FROM customers
WHERE phone IS NOT NULL

```
### Ex

```mysql
-- Get the orders that are not shipped
SELECT *
FROM orders
WHERE shipper_id IS NULL
-- equivalenly, shipped_date IS NULL
```
## OREDER BY

```mysql
-- default order is sorted by the primary key column
-- e.g. customers ' primary key column is customer_id



SELECT *
FROM customers
ORDER BY first_name -- in ascending order

SELECT *
FROM customers
ORDER BY first_name DESC -- in descending order


SELECT *
FROM customers
ORDER BY state, first_name -- by multiple columns, in state then in first name

SELECT *
FROM customers
ORDER BY state DESC, first_name 

SELECT *
FROM customers
ORDER BY state DESC, first_name DESC

SELECT first_name, last_name
FROM customers
ORDER BY birth_date -- can sort columns by any col, no matter chosen to show up or not

SELECT first_name, last_name, 10 AS points
FROM customers
ORDER BY points, first_name -- can sort by new col

SELECT first_name, last_name, 10 AS points
FROM customers
ORDER BY 1, 2 --this means sorting by first_name, then by last_name

SELECT birth_date, first_name, last_name, 10 AS points
FROM customers
ORDER BY 1, 2 --this means sorting by birth_date, then by first_name

-- can also sort by some calculation result of existing col's
```

### Ex
```mysql
-- Figure out the codes such that
-- picking all the orders from order_items with id 2,
-- and sort them in descending total price=quantity*unit_price

SELECT *, quantity*unit_price AS total_price
FROM order_items
WHERE order_id = 2
ORDER BY quantity*unit_price DESC -- Or: ORDER BY total_price DESC
```
