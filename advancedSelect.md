** all solutions are in Oracle
#### ![#f03c15](https://via.placeholder.com/15/f03c15/000000?text=+) ADVANCED SELECT QUERIES

###### TRIANGLES 
| Field | Type  |
|-------|-------|
A       | NUMBER
B       | NUMBER
C       | NUMBER

Write a query identifying the type of each record in the TRIANGLES table using its three side lengths. Output one of the following statements for each record in the table:
- Equilateral: It's a triangle with  sides of equal length.
- Isosceles: It's a triangle with  sides of equal length.
- Scalene: It's a triangle with  sides of differing lengths.
- Not A Triangle: The given values of A, B, and C don't form a triangle.

```
SELECT 
    CASE 
        WHEN A >= (B + C) OR B >= (A + C) OR C >= (A + B) THEN 'Not A Triangle'
        WHEN A = B AND A = C THEN 'Equilateral'
        WHEN A = B OR B = C OR A = C THEN 'Isosceles'
        ELSE 'Scalene'
    END
FROM TRIANGLES;
```

###### OCCUPATIONS 
| Field    | Type  |
|----------|-------|
Name       | String
Occupation | String

A. Generate the following two result sets:
1. Query an alphabetically ordered list of all names in OCCUPATIONS, immediately followed by the first letter of each profession as a parenthetical (i.e.: enclosed in parentheses). For example: AnActorName(A), ADoctorName(D), AProfessorName(P), and ASingerName(S).
2. Query the number of ocurrences of each occupation in OCCUPATIONS. Sort the occurrences in ascending order, and output them in the following format:    
```There are a total of [occupation_count] [occupation]s.```   
where [occupation_count] is the number of occurrences of an occupation in OCCUPATIONS and [occupation] is the lowercase occupation name. If more than one Occupation has the same [occupation_count], they should be ordered alphabetically.  
Note: There will be at least two entries in the table for each type of occupation.  
```
SELECT NAME || '(' || SUBSTR(OCCUPATION,1,1) || ')' FROM OCCUPATIONS ORDER BY NAME;
SELECT 'There are a total of ' || COUNT(OCCUPATION) || ' ' || LOWER(OCCUPATION) || 's.' FROM OCCUPATIONS GROUP BY OCCUPATION ORDER BY COUNT(OCCUPATION), OCCUPATION;
```
    
B. Pivot the Occupation column in OCCUPATIONS so that each Name is sorted alphabetically and displayed underneath its corresponding Occupation. The output column headers should be Doctor, Professor, Singer, and Actor, respectively.
Note: Print NULL when there are no more names corresponding to an occupation.  

###### Sample Input
| Name    | Occupation  |
|----------|-------|
Samantha | Doctor
Julia | Actor
Maria | Actor
Meera | Singer
Ashley | Professor
Ketty | Professor
Christeen | Professor
Jane | Actor
Jenny | Doctor
Priya | Singer
  
###### Sample Output
```
Jenny Ashley Meera Jane
Samantha Christeen Priya Julia
NULL Ketty NULL Maria
```
  
```
SELECT Doctor, Professor, Singer, Actor FROM (
    SELECT NAME, OCCUPATION, ROW_NUMBER() OVER (PARTITION BY OCCUPATION ORDER BY NAME) FROM Occupations) 
        PIVOT (MAX(NAME) FOR OCCUPATION IN ('Doctor' as Doctor, 'Professor' as Professor, 'Singer' as Singer, 'Actor' as Actor)
   ) 
ORDER BY Doctor, Professor, Singer, Actor;
```

Explanation
1. Partition names based on occupation, sort names and assign row number.  
```SELECT NAME, OCCUPATION, ROW_NUMBER() OVER (PARTITION BY OCCUPATION ORDER BY NAME) FROM Occupations```  
  
Output  
```
Jane Actor 1
Julia Actor 2
Maria Actor 3
Jenny Doctor 1
Samantha Doctor 2
Ashley Professor 1
Christeen Professor 2
Ketty Professor 3
Meera Singer 1
Priya Singer 2
```
  
2. For each row value, select name for the occupation.
```
SELECT Doctor, Professor, Singer, Actor FROM (
    SELECT NAME, OCCUPATION, ROW_NUMBER() OVER (PARTITION BY OCCUPATION ORDER BY NAME) FROM Occupations) 
        PIVOT (MAX(NAME) FOR OCCUPATION IN ('Doctor' as Doctor, 'Professor' as Professor, 'Singer' as Singer, 'Actor' as Actor)
   ) 
```
Output  
```
1. Jenny Ashley Meera Jane
3. NULL Ketty NULL Maria
2. Samantha Christeen Priya Julia
```

3. Perform order by to sort names & get expected result.
  
###### BST 
| Column | Type  |
|-------|-------|
N       | Integer
P       | Integer
  
Write a query to find the node type of Binary Tree ordered by the value of the node. Output one of the following for each node:  
Root: If node is root node.  
Leaf: If node is leaf node.  
Inner: If node is neither root nor leaf node.  
  
```
SELECT A.N, 
    CASE WHEN A.P IS NULL THEN 'Root'
         WHEN (SELECT COUNT(*) FROM BST B WHERE A.N = B.P) > 0 THEN 'Inner'
         ELSE 'Leaf'
    END
FROM BST A ORDER BY A.N;
```
