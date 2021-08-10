** all solutions are in Oracle
#### ![#f03c15](https://via.placeholder.com/15/f03c15/000000?text=+) AGGREGATION
  
###### CITY 
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
