## WHERE clause
The WHERE clause makes us only pick columns that makes a statement TRUE, in the following way: 
```mysql
SELECT *
FROM Customers
WHERE points > 3000 -- only columns making this statement TRUE

-- comparison operators used in the statement include:
-- >, >=, <, <=
-- =, (equality)
-- !=, <> (both means inequality) 

--E.g.
SELECT *
FROM Customers
WHERE state = 'VA' -- use quotation marks for a string, '' (conventional choice) or ""


SELECT *
FROM Customers
WHERE state = 'va' #same result as above


SELECT *
FROM Customers
WHERE state <> 'va'


SELECT *
FROM Customers
WHERE birth_date > '1990-01-01' -- can also use comparison operators for strings
 
```

### Ex 
```mysql
-- Get the orders placed this year
SELECT *
FROM orders
WHERE order_date >= '2021-01-01'

--later improve this such that it automatically detects which year is currently when coding
```

## AND, OR, NOT operators
