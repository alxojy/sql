** all solutions are in Oracle
#### ![#f03c15](https://via.placeholder.com/15/f03c15/000000?text=+) BASIC JOIN
  
###### CITY 
| Field       | Type |
|--------------|------------|
ID          | NUMBER
NAME        | VARCHAR2(17)
COUNTRYCODE | VARCHAR2(3)
DISTRICT    | VARCHAR2(20)
POPULATION  | NUMBER
  
###### COUNTRY 
| Field       | Type |
|--------------|------------|
CODE        | VARCHAR2(3)
NAME        | VARCHAR2(17)
CONTINENT | VARCHAR2(13)
REGION    | VARCHAR2(25)
POPULATION  | NUMBER
  
Given the CITY and COUNTRY tables, query the sum of the populations of all cities where the CONTINENT is 'Asia'.  
Note: CITY.CountryCode and COUNTRY.Code are matching key columns.  
```SELECT SUM(CITY.POPULATION) FROM CITY INNER JOIN COUNTRY ON CITY.COUNTRYCODE = COUNTRY.CODE WHERE COUNTRY.CONTINENT = 'Asia';```  
  
Given the CITY and COUNTRY tables, query the names of all cities where the CONTINENT is 'Africa'.  
```SELECT CITY.NAME FROM CITY INNER JOIN COUNTRY ON CITY.COUNTRYCODE = COUNTRY.CODE WHERE COUNTRY.CONTINENT = 'Africa';```
  
Given the CITY and COUNTRY tables, query the names of all the continents (COUNTRY.Continent) and their respective average city populations (CITY.Population) rounded down to the nearest integer.  
```SELECT COUNTRY.CONTINENT, FLOOR(AVG(CITY.POPULATION)) FROM COUNTRY INNER JOIN CITY ON COUNTRY.CODE = CITY.COUNTRYCODE GROUP BY COUNTRY.CONTINENT;```
     
###### STUDENTS 
| Field       | Type |
|--------------|------------|
ID        | Integer
Name        | String
Marks | Integer
  
###### GRADES 
| Grade  | Min_Mark | Max_Mark |
|--------|----------|----------|
1 | 0  |  9
2 | 10 | 19
  
Ketty gives Eve a task to generate a report containing three columns: Name, Grade and Mark. Ketty doesn't want the NAMES of those students who received a grade lower than 8. The report must be in descending order by grade -- i.e. higher grades are entered first. If there is more than one student with the same grade (8-10) assigned to them, order those particular students by their name alphabetically. Finally, if the grade is lower than 8, use "NULL" as their name and list them by their grades in descending order. If there is more than one student with the same grade (1-7) assigned to them, order those particular students by their marks in ascending order. Write a query to help Eve.  
```
SELECT CASE WHEN G.GRADE < 8 THEN NULL ELSE S.NAME END, G.GRADE, S.MARKS 
FROM STUDENTS S, GRADES G WHERE S.MARKS BETWEEN G.MIN_MARK AND G.MAX_MARK 
ORDER BY G.GRADE DESC, S.NAME;
```
  

