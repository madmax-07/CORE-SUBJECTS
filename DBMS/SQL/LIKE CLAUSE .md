Q1. Query the list of CITY names from STATION that do not start with vowels and do not end with vowels. Your result cannot contain duplicates.

```SQL
SELECT DISTINCT CITY 
FROM STATION 
WHERE (CITY NOT IN (SELECT DISTINCT CITY FROM STATION WHERE CITY LIKE '%a' OR CITY LIKE '%e' OR CITY LIKE '%i' OR CITY LIKE '%o' OR CITY LIKE '%u'))
OR 
(CITY NOT IN (SELECT CITY FROM STATION WHERE CITY LIKE 'A%' OR CITY LIKE 'E%' OR CITY LIKE 'I%' OR CITY LIKE 'O%' OR CITY LIKE 'U%'));
```
### A more optimal way is 

```SQL
select distinct city 
from station 
where city not rlike '^[aeiou]' and city not rlike '[aeiou]$';
```
MySQL RLIKE operator performs a pattern match of a string expression against a pattern. The pattern is supplied as an argument.
* ^	caret(^) : matches Beginning of string
* $	End of string
* [abc]	Any character listed between the square brackets

