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
WHERE first_name == 'ELKA' OR 'AMBUR'
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

## OREDER BY
