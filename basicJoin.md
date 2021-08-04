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
```SELECT SUM(CITY.POPULATION) FROM CITY JOIN COUNTRY ON CITY.COUNTRYCODE = COUNTRY.CODE WHERE COUNTRY.CONTINENT = 'Asia';```  
  
