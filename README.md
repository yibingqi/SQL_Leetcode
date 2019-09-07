# SQL_Leetcode
#### Just some SQL queries I wrote to leetcode problems.

1.	getNthHighestSalary
'''SQL
/* Write your T-SQL query statement below */
SELECT Person.FirstName, Person.LastName, Address.City, Address.State
FROM Person LEFT JOIN Address 
ON Person.PersonId = Address.PersonId;
'''SQL
