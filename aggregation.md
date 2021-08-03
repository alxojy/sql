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
  
