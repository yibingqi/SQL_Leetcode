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

184. Department Top Three Salaries  
The Employee table holds all employees. Every employee has an Id, and there is also a column for the department Id.  
The Department table holds all departments of the company.  
Write a SQL query to find employees who earn the top three salaries in each of the department. For the above tables, your SQL query should return the following rows (order of rows does not matter).  
```sql
/* Write your T-SQL query statement below */
SELECT d.Name  Department,e.Name Employee,e.Salary Salary
FROM (SELECT *,DENSE_RANK() OVER(partition by DepartmentId ORDER BY Salary DESC) row_num
      FROM Employee) e LEFT JOIN Department d
ON e.DepartmentId = d.Id
WHERE (row_num = 1 OR row_num = 2 OR row_num = 3) AND d.id IS NOT NULL;
```
196. Delete Duplicate Emails
Write a SQL query to delete all duplicate email entries in a table named Person, keeping only unique emails based on its smallest Id.
```sql
# Write your MySQL query statement below
DELETE e2
FROM Person e1, Person e2
WHERE e1.Id < e2.Id AND e2.Email = e1.Email;
```

197. Rising Temperature
Given a Weather table, write a SQL query to find all dates' Ids with higher temperature compared to its previous (yesterday's) dates.  
```sql
/* Write your T-SQL query statement below */
SELECT d1.Id
FROM Weather d1, Weather d2
WHERE d1.Temperature > d2.Temperature AND d2.RecordDate = DATEADD(day, -1, d1.RecordDate)
;
```
262. Trips and Users
The Trips table holds all taxi trips. Each trip has a unique Id, while Client_Id and Driver_Id are both foreign keys to the Users_Id at the Users table. Status is an ENUM type of (‘completed’, ‘cancelled_by_driver’, ‘cancelled_by_client’).  
The Users table holds all users. Each user has an unique Users_Id, and Role is an ENUM type of (‘client’, ‘driver’, ‘partner’).  
Write a SQL query to find the cancellation rate of requests made by unbanned users (both client and driver must be unbanned) between Oct 1, 2013 and Oct 3, 2013. The cancellation rate is computed by dividing the number of canceled (by client or driver) requests made by unbanned users by the total number of requests made by unbanned users.  
```sql
SELECT Request_at Day,ROUND(CAST(cancel_num AS FLOAT)/CAST(total AS FLOAT),2) "Cancellation Rate"
FROM(SELECT Request_at, COUNT(CASE WHEN Status LIKE 'cancelled_by_%' THEN 1 END) AS cancel_num, COUNT(*) total
FROM Trips
WHERE Request_at BETWEEN '2013-10-01' AND '2013-10-03' 
      AND Client_Id NOT IN (SELECT Users_Id FROM Users WHERE Banned = 'Yes')
      AND Driver_Id NOT IN (SELECT Users_Id FROM Users WHERE Banned = 'Yes')
GROUP BY Request_at) AS final;
```
595. Big Countries
A country is big if it has an area of bigger than 3 million square km or a population of more than 25 million.  
Write a SQL solution to output big countries' name, population and area.
```sql
/* Write your T-SQL query statement below */
SELECT name,population,area
FROM
(
SELECT *
FROM World
WHERE area > 3000000 OR population > 25000000
)a
```


