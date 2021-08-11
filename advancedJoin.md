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
