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

Q2. Query the two cities in STATION with the shortest and longest CITY names, as well as their respective lengths (i.e.: number of characters in the name). If there is more than one smallest or largest city, choose the one that comes first when ordered alphabetically.

```SQL
 select city,LENGTH(city) from station 
order by length(city) desc, City ASC 
limit 1;
select  CITY, LENGTH(city) from station 
order by length(city) asc, City ASC
limit 1;
```
Q3. Query the greatest value of the Northern Latitudes (LAT_N) from STATION that is less than 137.2345 . Truncate your answer to 4  decimal places.
```SQL
select ROUND(max(LAT_N),4) from station where LAT_N IN
(select (LAT_N) from station where LAT_N<137.2345);
```
Q4.Query the Western Longitude (LONG_W) for the largest Northern Latitude (LAT_N) in STATION that is less than 137.2345. Round your answer to 4 decimal places.

```sql
SELECT ROUND(LONG_W,4) from station where LAT_N=(select max(LAT_N) from station where LAT_N <137.2345);
```
