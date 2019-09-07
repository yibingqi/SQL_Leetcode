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

178. Rank Scores

Write a SQL query to rank scores. If there is a tie between two scores, both should have the same ranking. Note that after a tie, the next ranking number should be the next consecutive integer value. In other words, there should be no "holes" between ranks
```sql
SELECT Score, DENSE_RANK() OVER(ORDER BY Score DESC) Rank
FROM Scores;
```

180. Consecutive Numbers
Write a SQL query to find all numbers that appear at least three times consecutively.
```sql
SELECT DISTINCT l1.Num AS ConsecutiveNums
FROM Logs l1, Logs l2, Logs l3
WHERE l1.Id = l2.Id + 1 AND l2.Id = l3.Id+1 AND l1.Id = l3.Id+2 AND l1.Num = l2.Num AND l1.Num = l3.Num AND l2.Num = l3.Num;
```
