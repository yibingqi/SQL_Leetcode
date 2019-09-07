# SQL_Leetcode
#### Just some SQL queries I wrote to leetcode problems.

175. Combine Two Tables
```sql
/* Write your T-SQL query statement below */
SELECT Person.FirstName, Person.LastName, Address.City, Address.State
FROM Person LEFT JOIN Address 
ON Person.PersonId = Address.PersonId;
```

176. Second Highest Salary  
Write a SQL query to get the second highest salary from the *Employee* table.
```sql
/* Write your T-SQL query statement below */
SELECT *
FROM(SELECT DISTINCT Salary
     FROM Employee 
     ORDER BY Salary DESC
     LIMIT 1 OFFSET 1
);
```

177. Nth Highest Salary  
Write a SQL query to get the nth highest salary from the *Employee* table.
```sql
/* Write your T-SQL query statement below */
CREATE FUNCTION getNthHighestSalary(@N INT) RETURNS INT AS
BEGIN
    RETURN (
        /* Write your T-SQL query statement below. */
        SELECT (
            SELECT Salary 
            FROM Employee
            ORDER BY Salary DESC
            OFFSET @N-1 ROWS
            FETCH NEXT 1 ROWS ONLY
        )
    );
END
```
