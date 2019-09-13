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

181. Employees Earning More Than Their Managers
The Employee table holds all employees including their managers. Every employee has an Id, and there is also a column for the manager Id.
Given the Employee table, write a SQL query that finds out employees who earn more than their managers. For the above table, Joe is the only employee who earns more than his manager.
```sql
/* Write your T-SQL query statement below */
SELECT e1.Name AS Employee
FROM Employee e1, Employee m1
WHERE e1.ManagerId = m1.Id AND e1.Salary > m1.Salary;
```

182. Duplicate Emails
Write a SQL query to find all duplicate emails in a table named Person.
```sql
SELECT DISTINCT e1.Email
FROM Person e1, Person e2
WHERE e1.Id <> e2.Id AND e1.Email = e2.Email;
```

183. Customers Who Never Order
Suppose that a website contains two tables, the Customers table and the Orders table. Write a SQL query to find all customers who never order anything.
```sql
/* Write your T-SQL query statement below */
SELECT c.Name Customers
FROM Customers c
WHERE c.Id NOT IN (SELECT o.CustomerId FROM orders o);
```


