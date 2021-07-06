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

## LIKE
