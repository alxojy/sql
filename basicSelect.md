** all solutions are in Oracle
#### ![#f03c15](https://via.placeholder.com/15/f03c15/000000?text=+) BASIC SELECT QUERIES

###### CITY 
| Field       | Type |
|--------------|------------|
ID          | NUMBER
NAME        | VARCHAR2(17)
COUNTRYCODE | VARCHAR2(3)
DISTRICT    | VARCHAR2(20)
POPULATION  | NUMBER

Query all columns for all American cities in the CITY table with populations larger than 100000. The CountryCode for America is USA.  
```SELECT * FROM CITY WHERE POPULATION > 100000 AND COUNTRYCODE ='USA';```
  
Query the NAME field for all American cities in the CITY table with populations larger than 120000. The CountryCode for America is USA.  
```SELECT NAME FROM CITY WHERE POPULATION > 120000 AND COUNTRYCODE ='USA';```
  
Query all columns (attributes) for every row in the CITY table.  
```SELECT * FROM CITY;```  
  
Query all columns for a city in CITY with the ID 1661.  
```SELECT * FROM CITY WHERE ID = 1661;```  
  
Query all attributes of every Japanese city in the CITY table. The COUNTRYCODE for Japan is JPN.  
```SELECT * FROM CITY WHERE COUNTRYCODE ='JPN';```  

Query the names of all the Japanese cities in the CITY table. The COUNTRYCODE for Japan is JPN.   
```SELECT NAME FROM CITY WHERE COUNTRYCODE = 'JPN';```
  
  
###### STATION 
| Field     | Type |
|-----------|------------|
ID          | NUMBER
CITY        | VARCHAR2(21)
STATE       | VARCHAR2(2)
LAT_N       | NUMBER
LONG_W      | NUMBER

Query a list of CITY and STATE from the STATION table.   
```SELECT CITY, STATE FROM STATION;```  

Query a list of CITY names from STATION for cities that have an even ID number. Print the results in any order, but exclude duplicates from the answer.   
```SELECT DISTINCT CITY FROM STATION WHERE MOD(ID,2) = 0;```  

Find the difference between the total number of CITY entries in the table and the number of distinct CITY entries in the table.   
```SELECT (COUNT(CITY) - COUNT(DISTINCT CITY)) FROM STATION;```

Query the two cities in STATION with the shortest and longest CITY names, as well as their respective lengths (i.e.: number of characters in the name). If there is more than one smallest or largest city, choose the one that comes first when ordered alphabetically.  
```
SELECT * FROM (SELECT CITY, LENGTH(CITY) FROM STATION ORDER BY LENGTH(CITY), CITY) WHERE ROWNUM = 1;
SELECT * FROM (SELECT CITY, LENGTH(CITY) FROM STATION ORDER BY LENGTH(CITY) DESC, CITY) WHERE ROWNUM = 1;
```  

Query the list of CITY names starting with vowels (i.e., a, e, i, o, or u) from STATION. Your result cannot contain duplicates.  
```SELECT DISTINCT CITY FROM STATION WHERE UPPER(SUBSTR(CITY, 1, 1)) IN ('A','E','I','O','U');```  

Query the list of CITY names ending with vowels (a, e, i, o, u) from STATION. Your result cannot contain duplicates.  
```SELECT DISTINCT CITY FROM STATION WHERE UPPER(SUBSTR(CITY,-1,1)) IN ('A','E','I','O','U');```
  
Query the list of CITY names from STATION which have vowels (i.e., a, e, i, o, and u) as both their first and last characters. Your result cannot contain duplicates.  
```
SELECT DISTINCT CITY FROM STATION WHERE UPPER(SUBSTR(CITY,1,1)) IN ('A','E','I','O','U') AND UPPER(SUBSTR(CITY,-1,1)) IN ('A','E','I','O','U');
```  
OR
```SELECT DISTINCT CITY FROM STATION WHERE REGEXP_LIKE(CITY, '^[AEIOU].*[aeiou]$');```  

Query the list of CITY names from STATION that do not start with vowels. Your result cannot contain duplicates.  
```SELECT DISTINCT CITY FROM STATION WHERE REGEXP_LIKE(CITY, '^[^AEIOU].*$');```
  
Query the list of CITY names from STATION that do not end with vowels. Your result cannot contain duplicates.  
```SELECT DISTINCT CITY FROM STATION WHERE REGEXP_LIKE(CITY,'[^aeiou]$');```
  
Query the list of CITY names from STATION that either do not start with vowels or do not end with vowels. Your result cannot contain duplicates. 
```SELECT DISTINCT CITY FROM STATION WHERE REGEXP_LIKE(CITY,'^[^AEIOU]|[^aeiou]$');```  
  
Query the list of CITY names from STATION that do not start with vowels and do not end with vowels. Your result cannot contain duplicates.  
```SELECT DISTINCT CITY FROM STATION WHERE REGEXP_LIKE(CITY,'^[^AEIOU].*[^aeiou]$');```


###### STUDENTS 
| Field     | Type |
|-----------|------------|
ID          | NUMBER
Name        | VARCHAR2(21)
Marks       | NUMBER

Query the Name of any student in STUDENTS who scored higher than 75 Marks. Order your output by the last three characters of each name. If two or more students both have names ending in the same last three characters (i.e.: Bobby, Robby, etc.), secondary sort them by ascending ID.  
```SELECT Name FROM (SELECT * FROM STUDENTS ORDER BY SUBSTR(Name,-3,3), ID) WHERE Marks > 75;```


###### EMPLOYEE 
| Field     | Type |
|-----------|------------|
employee_id | NUMBER
name        | VARCHAR2(21)
months      | NUMBER
salary      | NUMBER

Write a query that prints a list of employee names (i.e.: the name attribute) from the Employee table in alphabetical order.  
```SELECT name FROM EMPLOYEE ORDER BY name;```

Write a query that prints a list of employee names (i.e.: the name attribute) for employees in Employee having a salary greater than $2000 per month who have been employees for less than 10 months. Sort your result by ascending employee_id.  
```SELECT name FROM EMPLOYEE WHERE salary > 2000 AND months < 10 ORDER BY employee_id;```
