Not euqals query in mysql and ms sql
SELECT name 
FROM Customer
WHERE referee_id <> 2 OR referee_id IS NULL;
!= can also be used for ms sql
------------------------------------------------------------------------------------------------------------------------------------------
Write a solution to find the IDs of the invalid tweets. The tweet is invalid if the number of characters used in the content of the tweet is strictly greater than 15.

My sql
# Write your MySQL query statement below
select tweet_id
from Tweets
where CHAR_LENGTH(content) > 15
ms sql
select tweet_id
from Tweets
where len(content) > 15
---------------------------------------------------------------------------------------------------------------
Write a solution to find all dates' id with higher temperatures compared to its previous dates (yesterday).
Ms sql
select w1.id
from Weather w1
join Weather w2
on w1.recordDate = dateadd(day, 1, W2.recordDate)
where w1.temperature > w2.temperature

my sql
SELECT w1.id
FROM Weather w1
JOIN Weather w2
ON w1.recordDate = DATE_ADD(w2.recordDate, INTERVAL 1 DAY)
WHERE w1.temperature > w2.temperature;
+----------------+---------+
| Column Name    | Type    |
+----------------+---------+
| machine_id     | int     |
| process_id     | int     |
| activity_type  | enum    |
| timestamp      | float   |
+----------------+---------+
The table shows the user activities for a factory website.
(machine_id, process_id, activity_type) is the primary key (combination of columns with unique values) of this table.
machine_id is the ID of a machine.
process_id is the ID of a process running on the machine with ID machine_id.
activity_type is an ENUM (category) of type ('start', 'end').
timestamp is a float representing the current time in seconds.
'start' means the machine starts the process at the given timestamp and 'end' means the machine ends the process at the given timestamp.
The 'start' timestamp will always be before the 'end' timestamp for every (machine_id, process_id) pair.
It is guaranteed that each (machine_id, process_id) pair has a 'start' and 'end' timestamp.
 
There is a factory website that has several machines each running the same number of processes. Write a solution to find the average time each machine takes to complete a process.
The time to complete a process is the 'end' timestamp minus the 'start' timestamp. The average time is calculated by the total time to complete every process on the machine divided by the number of processes that were run.
The resulting table should have the machine_id along with the average time as processing_time, which should be rounded to 3 decimal places.
Return the result table in any order.
The result format is in the following example.
 
Example 1:
Input: 
Activity table:
+------------+------------+---------------+-----------+
| machine_id | process_id | activity_type | timestamp |
+------------+------------+---------------+-----------+
| 0          | 0          | start         | 0.712     |
| 0          | 0          | end           | 1.520     |
| 0          | 1          | start         | 3.140     |
| 0          | 1          | end           | 4.120     |
| 1          | 0          | start         | 0.550     |
| 1          | 0          | end           | 1.550     |
| 1          | 1          | start         | 0.430     |
| 1          | 1          | end           | 1.420     |
| 2          | 0          | start         | 4.100     |
| 2          | 0          | end           | 4.512     |
| 2          | 1          | start         | 2.500     |
| 2          | 1          | end           | 5.000     |
+------------+------------+---------------+-----------+
Output: 
+------------+-----------------+
| machine_id | processing_time |
+------------+-----------------+
| 0          | 0.894           |
| 1          | 0.995           |
| 2          | 1.456           |
+------------+-----------------+
Explanation: 
There are 3 machines running 2 processes each.
Machine 0's average time is ((1.520 - 0.712) + (4.120 - 3.140)) / 2 = 0.894
Machine 1's average time is ((1.550 - 0.550) + (1.420 - 0.430)) / 2 = 0.995
Machine 2's average time is ((4.512 - 4.100) + (5.000 - 2.500)) / 2 = 1.456

solution
select
a1.machine_id,
cast(avg(a2.timestamp - a1.timestamp) as decimal(38, 3)) as processing_time
from Activity a1
join Activity a2
on  a1.machine_id = a2.machine_id and a1.process_id = a2.process_id and a1.activity_type = 'start' and a2.activity_type = 'end'
group by a1.machine_id

After Join (Intermediate Table):
+------------+------------+---------------+-----------+------------+------------+---------------+-----------+
| machine_id | process_id | activity_type | timestamp | machine_id | process_id | activity_type | timestamp |
+------------+------------+---------------+-----------+------------+------------+---------------+-----------+
| 0          | 0          | start         | 0.712     | 0          | 0          | end           | 1.520     |
| 0          | 1          | start         | 3.140     | 0          | 1          | end           | 4.120     |
| 1          | 0          | start         | 0.550     | 1          | 0          | end           | 1.550     |
| 1          | 1          | start         | 0.430     | 1          | 1          | end           | 1.420     |
| 2          | 0          | start         | 4.100     | 2          | 0          | end           | 4.512     |
| 2          | 1          | start         | 2.500     | 2          | 1          | end           | 5.000     |
+------------+------------+---------------+-----------+------------+------------+---------------+-----------+

+---------------+---------+
| Column Name   | Type    |
+---------------+---------+
| student_id    | int     |
| student_name  | varchar |
+---------------+---------+
student_id is the primary key (column with unique values) for this table.
Each row of this table contains the ID and the name of one student in the school.
 
Table: Subjects
+--------------+---------+
| Column Name  | Type    |
+--------------+---------+
| subject_name | varchar |
+--------------+---------+
subject_name is the primary key (column with unique values) for this table.
Each row of this table contains the name of one subject in the school.
 
Table: Examinations
+--------------+---------+
| Column Name  | Type    |
+--------------+---------+
| student_id   | int     |
| subject_name | varchar |
+--------------+---------+
There is no primary key (column with unique values) for this table. It may contain duplicates.
Each student from the Students table takes every course from the Subjects table.
Each row of this table indicates that a student with ID student_id attended the exam of subject_name.
 
Write a solution to find the number of times each student attended each exam.
Return the result table ordered by student_id and subject_name.
The result format is in the following example.
 
Example 1:
Input: 
Students table:
+------------+--------------+
| student_id | student_name |
+------------+--------------+
| 1          | Alice        |
| 2          | Bob          |
| 13         | John         |
| 6          | Alex         |
+------------+--------------+
Subjects table:
+--------------+
| subject_name |
+--------------+
| Math         |
| Physics      |
| Programming  |
+--------------+
Examinations table:
+------------+--------------+
| student_id | subject_name |
+------------+--------------+
| 1          | Math         |
| 1          | Physics      |
| 1          | Programming  |
| 2          | Programming  |
| 1          | Physics      |
| 1          | Math         |
| 13         | Math         |
| 13         | Programming  |
| 13         | Physics      |
| 2          | Math         |
| 1          | Math         |
+------------+--------------+
Output: 
+------------+--------------+--------------+----------------+
| student_id | student_name | subject_name | attended_exams |
+------------+--------------+--------------+----------------+
| 1          | Alice        | Math         | 3              |
| 1          | Alice        | Physics      | 2              |
| 1          | Alice        | Programming  | 1              |
| 2          | Bob          | Math         | 1              |
| 2          | Bob          | Physics      | 0              |
| 2          | Bob          | Programming  | 1              |
| 6          | Alex         | Math         | 0              |
| 6          | Alex         | Physics      | 0              |
| 6          | Alex         | Programming  | 0              |
| 13         | John         | Math         | 1              |
| 13         | John         | Physics      | 1              |
| 13         | John         | Programming  | 1              |
+------------+--------------+--------------+----------------+
Explanation: 
The result table should contain all students and all subjects.
Alice attended the Math exam 3 times, the Physics exam 2 times, and the Programming exam 1 time.
Bob attended the Math exam 1 time, the Programming exam 1 time, and did not attend the Physics exam.
Alex did not attend any exams.
John attended the Math exam 1 time, the Physics exam 1 time, and the Programming exam 1 time.

SELECT 
    s.student_id,
    s.student_name,
    sub.subject_name,
    COUNT(e.subject_name) AS attended_exams
FROM Students s
CROSS JOIN Subjects sub
LEFT JOIN Examinations e ON s.student_id = e.student_id AND sub.subject_name = e.subject_name
GROUP BY s.student_id, s.student_name, sub.subject_name
ORDER BY s.student_id, sub.subject_name;

--SQL standard requires all columns in the SELECT clause (that are not part of an aggregate function like COUNT) to also be included in the GROUP BY clause. Here for student_name


Step 1: After CROSS JOIN
The CROSS JOIN will generate every combination of student_id and subject_name from the Students and Subjects tables.
plaintext
CopyEdit
+------------+--------------+--------------+
| student_id | student_name | subject_name |
+------------+--------------+--------------+
| 1          | Alice        | Math         |
| 1          | Alice        | Physics      |
| 1          | Alice        | Programming  |
| 2          | Bob          | Math         |
| 2          | Bob          | Physics      |
| 2          | Bob          | Programming  |
| 6          | Alex         | Math         |
| 6          | Alex         | Physics      |
| 6          | Alex         | Programming  |
| 13         | John         | Math         |
| 13         | John         | Physics      |
| 13         | John         | Programming  |
+------------+--------------+--------------+
Step 2: After LEFT JOIN with Examinations
The LEFT JOIN adds data from the Examinations table based on matching student_id and subject_name. If no record exists for a student and subject combination, the Examinations columns will be NULL.
plaintext
CopyEdit
+------------+--------------+--------------+------------+------------+--------------+
| student_id | student_name | subject_name | student_id | subject_name | student_id   |
+------------+--------------+--------------+------------+------------+--------------+
| 1          | Alice        | Math         | 1          | Math         | 1            |
| 1          | Alice        | Math         | 1          | Math         | 1            |
| 1          | Alice        | Math         | 1          | Math         | 1            |
| 1          | Alice        | Physics      | 1          | Physics      | 1            |
| 1          | Alice        | Physics      | 1          | Physics      | 1            |
| 1          | Alice        | Programming  | 1          | Programming  | 1            |
| 2          | Bob          | Programming  | 2          | Programming  | 2            |
| 2          | Bob          | Math         | 2          | Math         | 2            |
| 13         | John         | Math         | 13         | Math         | 13           |
| 13         | John         | Physics      | 13         | Physics      | 13           |
| 13         | John         | Programming  | 13         | Programming  | 13           |
| 6          | Alex         | Math         | NULL       | NULL         | NULL          |
| 6          | Alex         | Physics      | NULL       | NULL         | NULL          |
| 6          | Alex         | Programming  | NULL       | NULL         | NULL          |
+------------+--------------+--------------+------------+------------+--------------+

In this case it is possible without cross join.

For joining table to itself IN query can be used(one of the way)
SELECT name
FROM Employee
WHERE id IN (
    SELECT managerId
    FROM Employee
    WHERE managerId IS NOT NULL
    GROUP BY managerId
    HAVING COUNT(id) >= 5
);

Using select inside select
https://leetcode.com/problems/percentage-of-users-attended-a-contest/description/?envType=study-plan-v2&envId=top-sql-50
https://leetcode.com/problems/consecutive-numbers/submissions/1425739430/?envType=study-plan-v2&envId=top-sql-50

using case inside select, after applying group by
https://leetcode.com/problems/queries-quality-and-percentage/?envType=study-plan-v2&envId=top-sql-50

https://leetcode.com/problems/monthly-transactions-i/?envType=study-plan-v2&envId=top-sql-50

https://leetcode.com/problems/last-person-to-fit-in-the-bus/submissions/1425779219/?envType=study-plan-v2&envId=top-sql-50
understand WITH Clause Common Table Expression (CTE)
+-----------------------------+---------+
| Column Name                 | Type    |
+-----------------------------+---------+
| delivery_id                 | int     |
| customer_id                 | int     |
| order_date                  | date    |
| customer_pref_delivery_date | date    |
+-----------------------------+---------+
delivery_id is the column of unique values of this table.
The table holds information about food delivery to customers that make orders at some date and specify a preferred delivery date (on the same order date or after it).
 
If the customer's preferred delivery date is the same as the order date, then the order is called immediate; otherwise, it is called scheduled.
The first order of a customer is the order with the earliest order date that the customer made. It is guaranteed that a customer has precisely one first order.
Write a solution to find the percentage of immediate orders in the first orders of all customers, rounded to 2 decimal places.
The result format is in the following example.
 
Example 1:
Input: 
Delivery table:
+-------------+-------------+------------+-----------------------------+
| delivery_id | customer_id | order_date | customer_pref_delivery_date |
+-------------+-------------+------------+-----------------------------+
| 1           | 1           | 2019-08-01 | 2019-08-02                  |
| 2           | 2           | 2019-08-02 | 2019-08-02                  |
| 3           | 1           | 2019-08-11 | 2019-08-12                  |
| 4           | 3           | 2019-08-24 | 2019-08-24                  |
| 5           | 3           | 2019-08-21 | 2019-08-22                  |
| 6           | 2           | 2019-08-11 | 2019-08-13                  |
| 7           | 4           | 2019-08-09 | 2019-08-09                  |
+-------------+-------------+------------+-----------------------------+
Output: 
+----------------------+
| immediate_percentage |
+----------------------+
| 50.00                |
+----------------------+
Explanation: 
The customer id 1 has a first order with delivery id 1 and it is scheduled.
The customer id 2 has a first order with delivery id 2 and it is immediate.
The customer id 3 has a first order with delivery id 5 and it is scheduled.
The customer id 4 has a first order with delivery id 7 and it is immediate.
Hence, half the customers have immediate first orders.
WITH first_order AS (
    SELECT 
        customer_id, 
        delivery_id,
        (CASE 
            WHEN order_date = customer_pref_delivery_date THEN 'immediate' 
            ELSE 'scheduled' 
        END) AS order_type,
        ROW_NUMBER() OVER (PARTITION BY customer_id ORDER BY order_date) AS row_num
    FROM 
        Delivery
)
SELECT 
    CAST(
        SUM(CASE 
            WHEN order_type = 'immediate' THEN 1 
            ELSE 0 
        END) * 100.0 / COUNT(customer_id)
    AS DECIMAL(38, 2)
    ) AS immediate_percentage
FROM 
    first_order
WHERE 
    row_num = 1;

 
Partition by actually groups based on customer_id
So purpose here is to, group it, addd new temp(hypothetical col) and provide row number within grp
Inside Query in from()
https://leetcode.com/problems/biggest-single-number/?envType=study-plan-v2&envId=top-sql-50
select query inside having
https://leetcode.com/problems/customers-who-bought-all-products/?envType=study-plan-v2&envId=top-sql-50
The primary difference between DENSE_RANK and ROW_NUMBER is how they assign ranks in case of ties (duplicate values in the ORDER BY column). Here's a detailed explanation:
________________________________________
1. DENSE_RANK
•	Definition: Assigns consecutive ranks, and ties (duplicate values) share the same rank. The next rank after a tie is NOT skipped.
•	Behavior:
o	If two employees in a department have the same salary, they get the same rank.
o	The next rank after a tie does not skip numbers.
Example:
If the salaries are 85K, 85K, 80K, and ranked in descending order:
•	85K: Rank 1
•	85K: Rank 1 (tie)
•	80K: Rank 2
________________________________________
2. ROW_NUMBER
•	Definition: Assigns a unique rank to every row, even if there are ties (no duplicate ranks are assigned). It essentially numbers the rows sequentially.
•	Behavior:
o	For employees with the same salary, the rank differs.
o	Ties are broken arbitrarily (or based on additional criteria in the query).
Example:
If the salaries are 85K, 85K, 80K, and ranked in descending order:
•	85K: Rank 1
•	85K: Rank 2 (not a tie, unique rank assigned)
•	80K: Rank 3
________________________________________
3. Difference in Ranking
Here’s how the two functions differ in ranking when there are ties:
Salary	DENSE_RANK	ROW_NUMBER
100K	1	1
85K	2	2
85K	2 (tie)	3
80K	3	4
________________________________________
3. Summary
•	Use DENSE_RANK when ties should receive the same rank, and you want the next rank to remain consecutive.
•	Use ROW_NUMBER when each row needs a unique rank, regardless of ties.
Group concat
https://leetcode.com/problems/group-sold-products-by-the-date/?envType=study-plan-v2&envId=top-sql-50
