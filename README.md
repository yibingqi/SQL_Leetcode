# SQL_Leetcode
#### Just some SQL queries I wrote to leetcode problems.

SELECT d.Name AS Department,e.Name AS Employee,Salary
FROM Employee e
JOIN Department d
ON e.DepartmentId=d.Id
WHERE (DepartmentId, Salary) IN
(select DepartmentId, max(Salary)
 FROM Employee
 GROUP BY DepartmentId
)      # here we need to select the employee's name, so we cannot use groupby() directly
