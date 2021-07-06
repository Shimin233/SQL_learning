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
-- WHERE state 
SELECT * 
FROM Customers
WHERE state NOT IN ('VA', 'FL', 'GA')
```

## BETWEEN 

## LIKE
