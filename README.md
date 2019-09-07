# SQL_Leetcode
#### Just some SQL queries I wrote to leetcode problems.

1.	getNthHighestSalary

> CREATE FUNCTION getNthHighestSalary(@N INT) RETURNS INT AS
> BEGIN
>     RETURN (
>         /* Write your T-SQL query statement below. */
>        SELECT (
>             SELECT Salary 
>             FROM Employee
>             ORDER BY Salary DESC
>             OFFSET @N-1 ROWS
>             FETCH NEXT 1 ROWS ONLY
>         )
>     );
> END

