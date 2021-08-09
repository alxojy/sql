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
  
###### HACKERS 
| Column | Type |
|--------------|------------|
hacker_id  | Integer
name | String
  
###### DIFFICULTY 
| Column | Type |
|--------------|------------|
difficulty_level | Integer
score | Integer
  
###### CHALLENGES 
| Column | Type |
|--------------|------------|
challenge_id  | Integer
hacker_id  | Integer
difficulty_level | Integer
  
###### SUBMISSIONS 
| Column | Type |
|--------------|------------|
submission_id  | Integer
hacker_id  | Integer
challenge_id  | Integer
score | Integer
  
Julia just finished conducting a coding contest, and she needs your help assembling the leaderboard! Write a query to print the respective hacker_id and name of hackers who achieved full scores for more than one challenge. Order your output in descending order by the total number of challenges in which the hacker earned a full score. If more than one hacker received full scores in same number of challenges, then sort them by ascending hacker_id.  
  
```
SELECT H.HACKER_ID, H.NAME FROM SUBMISSIONS S 
INNER JOIN CHALLENGES C ON S.CHALLENGE_ID = C.CHALLENGE_ID
INNER JOIN DIFFICULTY D ON C.DIFFICULTY_LEVEL = D.DIFFICULTY_LEVEL AND S.SCORE = D.SCORE
INNER JOIN HACKERS H ON S.HACKER_ID = H.HACKER_ID
GROUP BY H.HACKER_ID, H.NAME HAVING COUNT(*) > 1 ORDER BY COUNT(*) DESC, H.HACKER_ID;
```
  
###### CITY 
| Field       | Type |
|--------------|------------|
id          | integer
code        | integer
coins_needed | integer
power    | integer
  
###### WANDS_PROPERTY 
| Field       | Type |
|--------------|------------|
code        | integer
age        | integer
is_evil | integer
  
Hermione decides the best way to choose is by determining the minimum number of gold galleons needed to buy each non-evil wand of high power and age. Write a query to print the id, age, coins_needed, and power of the wands that Ron's interested in, sorted in order of descending power. If more than one wand has same power, sort the result in order of descending age.  
  
```
SELECT W.ID, WP.AGE, W.COINS_NEEDED, W.POWER FROM WANDS W
INNER JOIN (SELECT CODE, POWER, MIN(COINS_NEEDED) AS COINS_NEEDED FROM WANDS GROUP BY CODE, POWER) M ON M.COINS_NEEDED = W.COINS_NEEDED AND M.CODE = W.CODE AND M.POWER = W.POWER 
INNER JOIN WANDS_PROPERTY WP ON W.CODE = WP.CODE
WHERE WP.IS_EVIL = 0
ORDER BY W.POWER DESC, WP.AGE DESC;
```
  
###### HACKERS 
| Field       | Type |
|--------------|------------|
hacker_id          | integer
name        | string
  
###### CHALLENGES 
| Field       | Type |
|--------------|------------|
challenge_id        | integer
hacker_id          | integer
  
Julia asked her students to create some coding challenges. Write a query to print the hacker_id, name, and the total number of challenges created by each student. Sort your results by the total number of challenges in descending order. If more than one student created the same number of challenges, then sort the result by hacker_id. If more than one student created the same number of challenges and the count is less than the maximum number of challenges created, then exclude those students from the result.  
  
```
SELECT H.HACKER_ID, H.NAME, COUNT(*) AS TOTAL FROM HACKERS H 
INNER JOIN CHALLENGES C ON H.HACKER_ID = C.HACKER_ID
GROUP BY H.HACKER_ID, H.NAME
HAVING COUNT(*) = (SELECT MAX(COUNT(*)) FROM CHALLENGES C GROUP BY C.HACKER_ID) OR
COUNT(*) IN (SELECT * FROM 
             (SELECT COUNT(*) AS CNT FROM CHALLENGES C GROUP BY C.HACKER_ID) 
             GROUP BY CNT HAVING COUNT(*) = 1)
ORDER BY TOTAL DESC, H.HACKER_ID;
```
  
You did such a great job helping Julia with her last coding contest challenge that she wants you to work on this one, too!
The total score of a hacker is the sum of their maximum scores for all of the challenges. Write a query to print the hacker_id, name, and total score of the hackers ordered by the descending score. If more than one hacker achieved the same total score, then sort the result by ascending hacker_id. Exclude all hackers with a total score of 0 from your result.  
```
SELECT H.HACKER_ID, H.NAME, SUM(S.SCORES) AS TOTAL FROM HACKERS H 
INNER JOIN (SELECT HACKER_ID, MAX(SCORE) AS SCORES FROM SUBMISSIONS GROUP BY HACKER_ID, CHALLENGE_ID) S 
ON H.HACKER_ID = S.HACKER_ID
GROUP BY H.HACKER_ID, H.NAME
HAVING SUM(S.SCORES) > 0
ORDER BY TOTAL DESC, H.HACKER_ID;
```

