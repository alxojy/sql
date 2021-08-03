** all solutions are in Oracle
#### ![#f03c15](https://via.placeholder.com/15/f03c15/000000?text=+) AGGREGATION
  
###### CITY 
| Field       | Type |
|--------------|------------|
ID          | NUMBER
NAME        | VARCHAR2(17)
COUNTRYCODE | VARCHAR2(3)
DISTRICT    | VARCHAR2(20)
POPULATION  | NUMBER
  
Query a count of the number of cities in CITY having a Population larger than 100,000.  
```SELECT COUNT(NAME) FROM CITY WHERE POPULATION > 100000;```  
  
Query the total population of all cities in CITY where District is California.  
```SELECT SUM(POPULATION) FROM CITY WHERE DISTRICT = 'California';```
  
Query the average population of all cities in CITY where District is California.  
```SELECT AVG(POPULATION) FROM CITY WHERE DISTRICT = 'California';```
  
Query the average population for all cities in CITY, rounded down to the nearest integer.  
```SELECT ROUND(AVG(POPULATION)) FROM CITY;```
  
Query the sum of the populations for all Japanese cities in CITY. The COUNTRYCODE for Japan is JPN.  
```SELECT SUM(POPULATION) FROM CITY WHERE COUNTRYCODE = 'JPN';```
  
Query the difference between the maximum and minimum populations in CITY.  
```SELECT MAX(POPULATION)-MIN(POPULATION) FROM CITY;```
  
###### EMPLOYEES 
| Field       | Type |
|--------------|------------|
ID          | Integer
Name        | String
Salary      | Integer
  
Samantha was tasked with calculating the average monthly salaries for all employees in the EMPLOYEES table, but did not realize her keyboard's key was broken until after completing the calculation. She wants your help finding the difference between her miscalculation (using salaries with any zeros removed), and the actual average salary.  
  
Write a query calculating the amount of error (i.e.: actual - miscalculated average monthly salaries), and round it up to the next integer.
  
###### Sample Input
| Field       | Type |
|--------------|------------|
Kristeen       | 1420
Maria          | 2006
Julia          | 2210

###### Samantha's Table
| Field       | Type |
|--------------|------------|
Kristeen       | 142
Maria          | 26
Julia          | 221
  
```SELECT CEIL(AVG(SALARY) - AVG(TO_NUMBER(REPLACE(TO_CHAR(SALARY),'0','')))) FROM EMPLOYEES;```  
  
###### EMPLOYEE 
| Field       | Type |
|--------------|------------|
ID          | Integer
Name        | String
Salary      | Integer
Months      | Integer
  
We define an employee's total earnings to be their monthly salary x months worked, and the maximum total earnings to be the maximum total earnings for any employee in the Employee table. Write a query to find the maximum total earnings for all employees as well as the total number of employees who have maximum total earnings. Then print these values as space-separated integers.  
```
SELECT MAX(SALARY*MONTHS), COUNT(*) FROM EMPLOYEE WHERE SALARY*MONTHS = (SELECT MAX(SALARY*MONTHS) FROM EMPLOYEE);
```  
    
###### STATION 
| Field       | Type |
|--------------|------------|
ID          | NUMBER
CITY        | VARCHAR(21)
STATE      | VARCHAR(2)
LAT_N      | NUMBER
LONG_N      | NUMBER
  
Query the following two values from the STATION table:
The sum of all values in LAT_N rounded to a scale of 2 decimal places.
The sum of all values in LONG_W rounded to a scale of 2 decimal places.  
```SELECT ROUND(SUM(LAT_N), 2), ROUND(SUM(LONG_W), 2) FROM STATION;```

Query the sum of Northern Latitudes (LAT_N) from STATION having values greater than 38.7880 and less than 137.2345. Truncate your answer to 4 decimal places.  
```SELECT ROUND(SUM(LAT_N), 4) FROM STATION WHERE 38.7880 < LAT_N AND LAT_N < 137.2345;```
  
Query the greatest value of the Northern Latitudes (LAT_N) from STATION that is less than 137.2345. Truncate your answer to 4 decimal places.  
```SELECT ROUND(MAX(LAT_N),4) FROM STATION WHERE LAT_N < 137.2345;```
  
Query the Western Longitude (LONG_W) for the largest Northern Latitude (LAT_N) in STATION that is less than 137.2345. Round your answer to 4 decimal places.  
```SELECT ROUND(MAX(LONG_W), 4) FROM STATION WHERE LAT_N = (SELECT MAX(LAT_N) FROM STATION WHERE LAT_N < 137.2345);```
  
Query the smallest Northern Latitude (LAT_N) from STATION that is greater than 38.7780. Round your answer to 4 decimal places.  
```SELECT ROUND(MIN(LAT_N), 4) FROM STATION WHERE LAT_N > 38.7880;```
  
Query the Western Longitude (LONG_W)where the smallest Northern Latitude (LAT_N) in STATION is greater than 38.7780. Round your answer to 4 decimal places.  
```SELECT ROUND(LONG_W, 4) FROM STATION WHERE LAT_N = (SELECT MIN(LAT_N) FROM STATION WHERE LAT_N > 38.7880);```
  



  
