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
  
