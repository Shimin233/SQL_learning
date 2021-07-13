## Self Joins
```mysql
-- one value is used to refer to different things (in diff col's)
-- in one single table

-- can join one table with itself
USE sql_hr

SELECT * 
FROM employees e -- emplyees
JOIN employees m -- manager
    ON e.reports_to=m.employee_id
    
SELECT * 
  e.employee_id,
  e.first_name,
  m.first_name AS manager
FROM employees e -- emplyees
JOIN employees m -- manager; must use different aliases, when self-joining
    ON e.reports_to=m.employee_id
```
## Joining Multiple Tables

## Compound Join Condtions
