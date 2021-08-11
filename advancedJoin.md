** all solutions are in Oracle
#### ![#f03c15](https://via.placeholder.com/15/f03c15/000000?text=+) ADVANCED JOIN
  
###### PROJECTS 
| Field       | Type |
|--------------|------------|
Task_id          | Integer
Start_date        | Integer
End_date | Date
  
If the End_Date of the tasks are consecutive, then they are part of the same project. Samantha is interested in finding the total number of different projects completed.  
Write a query to output the start and end dates of projects listed by the number of days it took to complete the project in ascending order. If there is more than one project that have the same number of completion days, then order by the start date of the project.
  
```
select a.start_date, min(b.end_date) from
(select start_date from projects where start_date not in (select end_date from projects)) a,
(select end_date from projects where end_date not in (select start_date from projects)) b
where a.start_date < b.end_date
group by a.start_date
order by to_date(min(b.end_date), 'yyyy-mm-dd') - to_date(a.start_date, 'yyyy-mm-dd'), to_date(a.start_date, 'yyyy-mm-dd');
```
  
###### STUDENTS 
| Field       | Type |
|--------------|------------|
ID          | Integer
Name        | String
  
###### FRIENDS 
| Field       | Type |
|--------------|------------|
ID          | Integer
Friend_ID        | Integer
  
###### PACKAGES 
| Field       | Type |
|--------------|------------|
ID          | Integer
Salary        | Integer
  
Write a query to output the names of those students whose best friends got offered a higher salary than them. Names must be ordered by the salary amount offered to the best friends. It is guaranteed that no two students got same salary offer.  
  
```
SELECT S.NAME FROM FRIENDS F 
INNER JOIN PACKAGES P1 ON F.ID = P1.ID
INNER JOIN PACKAGES P2 ON F.FRIEND_ID = P2.ID
INNER JOIN STUDENTS S ON F.ID = S.ID
WHERE P2.SALARY > P1.SALARY
ORDER BY P2.SALARY;
```
  
###### FUNCTIONS 
| Field       | Type |
|--------------|------------|
X          | Integer
Y        | Integer
  
Two pairs (X1, Y1) and (X2, Y2) are said to be symmetric pairs if X1 = Y2 and X2 = Y1.  
Write a query to output all such symmetric pairs in ascending order by the value of X. List the rows such that X1 ≤ Y1.  
  
```
SELECT X, Y FROM 
(SELECT X,Y FROM FUNCTIONS WHERE X=Y GROUP BY X,Y HAVING COUNT(*) > 1)
UNION
(SELECT F1.X AS X, F1.Y AS Y FROM FUNCTIONS F1, FUNCTIONS F2 
 WHERE F1.X <> F1.Y AND F1.X = F2.Y AND F1.Y = F2.X AND F1.X < F1.Y)
ORDER BY X, Y;
```
  
###### CONTESTS 
| Field       | Type |
|--------------|------------|
contest_id         | Integer
hacker_id        | Integer
name | String
  
###### COLLEGES 
| Field       | Type |
|--------------|------------|
college_id          | Integer
contest_id        | Integer
  
###### CHALLENGES 
| Field       | Type |
|--------------|------------|
challenge_id          | Integer
college_id        | Integer
  
###### VIEW_STATS 
| Field       | Type |
|--------------|------------|
challenge_id          | Integer
total_views        | Integer
total_unique_views        | Integer
  
###### SUBMISSION_STATS 
| Field       | Type |
|--------------|------------|
challenge_id          | Integer
total_submissions        | Integer
total_unique_submissions        | Integer
  
Samantha interviews many candidates from different colleges using coding challenges and contests. Write a query to print the contest_id, hacker_id, name, and the sums of total_submissions, total_accepted_submissions, total_views, and total_unique_views for each contest sorted by contest_id. Exclude the contest from the result if all four sums are 0.  
Note: A specific contest can be used to screen candidates at more than one college, but each college only holds 1 screening contest.  
  
```
select con.contest_id, con.hacker_id, con.name, 
sum(s.total_submissions), sum(s.total_accepted_submissions), 
sum(v.total_views), sum(v.total_unique_views)
from contests con
inner join colleges col on con.contest_id = col.contest_id
inner join challenges chal on col.college_id = chal.college_id
left join (select challenge_id, sum(total_views) as total_views, 
           sum(total_unique_views) as total_unique_views 
           from view_stats group by challenge_id) v 
           on chal.challenge_id = v.challenge_id
left join (select challenge_id, sum(total_submissions) as total_submissions,
           sum(total_accepted_submissions) as total_accepted_submissions 
           from submission_stats group by challenge_id) s 
           on chal.challenge_id = s.challenge_id
group by con.contest_id, con.hacker_id, con.name
having sum(v.total_views) + 
       sum(v.total_unique_views) + 
       sum(s.total_submissions) + 
       sum(s.total_accepted_submissions) > 0
order by con.contest_id;
```
