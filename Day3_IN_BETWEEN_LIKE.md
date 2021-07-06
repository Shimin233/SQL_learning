## IN

```mysql
-- OR, AND are used to separate (connect) statements which are TRUE or FALSE
-- so do not type this, 
-- SELECT *
-- FROM Customers
-- WHERE state='VA' OR 'FL' OR 'GA'
-- but this instead :)
SELECT *
FROM Customers
WHERE state='VA' OR state='FL' OR state='GA'

__ IN means being an element in
__ the following is equivalent to the codes above using OR
SELECT * 
FROM Customers
WHERE state IN ('VA', 'FL', 'GA')

-- the following is equivalent to 
-- WHERE NOT(state='VA' OR state='FL' OR state='GA')
SELECT * 
FROM Customers
WHERE state NOT IN ('VA', 'FL', 'GA')
```

### Ex
```mysql
-- Return products with quantity in stock equal to 49, 38, 72

-- my solution (correct)
SELECT *
FROM products
WHERE quantity_in_stock IN (49, 38, 72)
-- the result will be only two rows appearing: 
-- Pork with 49 and Lettuce with 38, no row of 72
```

## BETWEEN 

```mysql
SELECT *
FROM customers
WHERE points >= 1000 AND points <= 3000

-- equivalently, use BETWEEN (endpoints included)
SELECT *
FROM customers
WHERE points BETWEEN 1000 AND 3000
-- looks like abuse of AND notation, but just use it like this :P
```

### Ex

```mysql
-- Return customers who were born between 01-01-1990 and 01-01-2000

-- my soln, corrected
SELECT *
FROM customers
WHERE birth_date BETWEEN '1990-01-01' AND '2000-01-01'
-- three people outputted
-- note the format to type dates: order, two-digit and four-digit,  enclosed by ''
```
## LIKE
```mysql
-- LIKE, basically means 'of the form like'
-- only get customers whose last name starts with B 
--(can type b,or B into codes, no matter upper or lowercase)
SELECT *
FROM customers
WHERE las_name LIKE 'b%'

--...last name starts with 'brush'...
SELECT *
FROM customers
WHERE las_name LIKE 'brush%'

-- pick customers whose last name contains b anywhere, 
--  using % to represent other parts in the item (last name here)
SELECT *
FROM customers
WHERE last_name LIKE '%b%' -- b in last name, anywhere, beginning, middle or end

WHERE last_name LIKE '%y' -- ending with y

WHERE last_name LIKE '_____y' -- five underlines with y, meaning five letters with y ending pattern

WHERE last_name LIKE 'b_____y' -- last name that has b followed by five letters and ending with y

WHERE birth_date NOT LIKE '1990%' -- NOT can be used attached before LIKE

--summary: % meaning any part (including nothing), and _ meaning one letter
--   LIKE, NOT LIKE

```
### Ex
```mysql
-- Get the customers whose
--   addresses contain TRAIL or AVENUE, and
--    phone numbers end with 9

SELECT *
FROM customers
WHERE (address LIKE '%TRAIL%' OR address LIKE '%AVENUE%') AND phone LIKE '%9'
-- note the form: LIKE 'anythingFollowingLIKE'
-- OR only connects complete statement which are TRUE or FALSE
```
