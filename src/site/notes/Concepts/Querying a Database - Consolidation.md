---
{"dg-publish":true,"permalink":"/concepts/querying-a-database-consolidation/","dgHomeLink":true,"dgShowToc":true}
---


# Querying a Database: Consolidation

## Selecting and Filtering Data

Two classes ago, you learned how to query a single table in a database:

```sql
SELECT birth_date, first_name, last_name
FROM employees
WHERE emp_id BETWEEN 10004 AND 10008
```

We use the `SELECT` keyword to identify <span style="color:lightpink;">columns</span> that should be included in the result.

We use the `FROM` keyword to identify the <span style="color:dodgerblue;">table</span> to select columns from.

We use the `WHERE` keyword to identify <span style="color:darkseagreen;">rows</span> that should be included in the result.

The <span style="color:gold;">intersection</span> of the  included columns and rows is the data that will be returned:

![Screenshot 2023-03-31 at 9.10.31 AM.png](/img/user/Media/Screenshot%202023-03-31%20at%209.10.31%20AM.png)

![Pasted image 20230331091433.png](/img/user/Media/Pasted%20image%2020230331091433.png)

## Aliases

Aliases can be used to rename the header for a column in a result set:

```sql
SELECT 
	birth_date AS "Date of birth",
	first_name AS "First name",
	last_name AS "Last name"
FROM
	employees
WHERE
	emp_id BETWEEN 10004 AND 10008
```

![Pasted image 20230331091937.png](/img/user/Media/Pasted%20image%2020230331091937.png)

## Functions

Aggregate functions can be used to count or perform arithmetic on numeric values.

- `SUM(column_name)`
	- Add values within a group.
- `AVG(column_name)`
	- Average values within a group.
- `COUNT(column_name)`
	- Count how many values exist within a group.
- `MAX(column_name)`
	- Find the maximum value within a group.
- `MIN(column_name)`
	- Find the minimum value within a group.

For example, we can find the lowest birth date within the same group of rows returned earlier with this query:

```sql
SELECT MIN(birth_date)
FROM employees
WHERE emp_id BETWEEN 10004 AND 10008
```

![Screenshot 2023-03-31 at 9.29.57 AM.png](/img/user/Media/Screenshot%202023-03-31%20at%209.29.57%20AM.png)

![Pasted image 20230331093047.png](/img/user/Media/Pasted%20image%2020230331093047.png)

Further, if we combine the `MIN` function with a `GROUP BY` clause, we can find the lowest birth date within each gender group:

```sql
SELECT MIN(birth_date), gender
FROM employees
WHERE emp_id BETWEEN 10004 AND 10008
GROUP BY gender
```

In this case, values that exist in the `gender` column are `M` and `F`.

So, we get the lowest birth date within rows that contain an `M` in the gender column, and we also get the lowest birth date within rows that contain an `F` in the gender column:

![Screenshot 2023-03-31 at 9.35.29 AM.png](/img/user/Media/Screenshot%202023-03-31%20at%209.35.29%20AM.png)

![Pasted image 20230331093431.png](/img/user/Media/Pasted%20image%2020230331093431.png)

> [!TIP]
> When using a function like `MIN` together with the `GROUP BY` clause, it's usually helpful to also select the column you are grouping by. In this case it helps us to see that the lowest birth date among women is `1953-04-20` and the lowest birth date among men is `1954-05-01`.

## Subqueries

Think of subqueries as if you are asking multiple questions of the database, one by one.

For an example of using sub-queries, refer back to the [[Concepts/Introduction to Databases (Solutions)#^bad187\|solution to question 11 from earlier exercises]].

## Reference Sheet

You are always welcome to refer to the [reference sheet](https://learnsql.com/blog/sql-basics-cheat-sheet/sql-basics-cheat-sheet-letter.pdf) provided earlier while authoring queries.

## Consolidation Exercises

Once you have completed exercises from prior days, check your understanding by trying to answer as many questions in the list below. 

When you feel it is appropriate, join tables to provide more readable results.

Please place screenshots of your responses in a portfolio post [on Notion](https://notion.so).

> [!NOTE]
> Be aware that some of these are pretty challenging! Completing most (not necessarily all) of these exercises would be a great example of exceeding expectations.

1. The number of employees with first name starting with 'A' and last name starting with 'A'.
2. The number of female employees paid more than $100,000.
3. The name and salary of the lowest paid employee *ever* employed by the company.
4. The name and salary of the lowest paid employee *currently* employed by the company.
5. Find all of the employees whose first names end with ‘ase’.
6. Find a list of all the employees who were born in 1952 and were hired in 1990.
7. Find *how many* employees were born in 1952 and were hired in 1990.
9. Find all the employees that make more than 100K. (no duplicates)
10. Now find a count of employees that make more than 100K. (no duplicates)
11. Find the most recent person to be hired and their first name. 
12. Find how many years the employee with the number 10022 worked for. 
13. Find only the maximum and minimum salary paid to every employee with the employee number above 39,000 and below 40,000.
14. Find a list of all the names of the employees that have a salary of exactly $60,000.
15. Find *how many* employees have a salary of $60,000.
16. How many Senior Engineers are *currently* employed by the company?
17. What is the average pay for a Senior Engineer *currently* employed by the company?
18. Find a list of all Senior Engineers that make a pay higher than the average pay of all staff.
19. Find how many employees have the first name "Brendon" and a last name starting with "L".
20. Find the first and last name of the highest paid employee ever employed by the company.
21. Find the first and last name of the highest paid employee *currently* employed by the company.
22. Find the first and last name of male employees *currently* paid between $80,000 and $90,000.
23. What are the names of the 3 oldest employees?
24. Who are the ten most recent hires at the company?
25. Among the 10 most recent hires, which employee has has the highest salary?
26. Who is the youngest employee at the company, and when were they hired?
27. How many employees have birthdays in January and were born in 1999?
28. Who has had the most job titles?
29. Who has had the largest range in pay at the company?