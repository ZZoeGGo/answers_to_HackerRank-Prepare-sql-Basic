# answers_to_HackerRank-Prepare-sql-Basic
My Answers to the Basic sql questions on HackerRank
### 4.Find the difference between the total number of CITY entries in the table and the number of distinct CITY entries in the table.

SELECT COUNT(CITY) - COUNT(DISTINCT CITY) FROM STATION;

### 5.Query the two cities in STATION with the shortest and longest CITY names, as well as their respective lengths (i.e.: number of characters in the name). 
If there is more than one smallest or largest city, choose the one that comes first when ordered alphabetically.

(select city, length(city) from station order by length(city) desc, city asc limit 1)
union
(select city, length(city) from station order by length(city) asc, city asc limit 1);

### 6.Query the list of CITY names starting with vowels (i.e., a, e, i, o, or u) from STATION. Your result cannot contain duplicates.

Select distinct CITY
from STATION
where city Regexp "^[aeiou].*";

### 7.Query the list of CITY names ending with vowels (a, e, i, o, u) from STATION. Your result cannot contain duplicates.

SELECT DISTINCT CITY 
FROM STATION
WHERE CITY REGEXP"[a,e,i,o,u]$"

### 8.Query the list of CITY names from STATION which have vowels (i.e., a, e, i, o, and u) as both their first and last characters. Your result cannot contain duplicates.

Select Distinct CITY
from STATION
WHERE CITY REGEXP "^[A,E,I,O,U].*[A,E,I,O,U]$"

### 11.Query the list of CITY names from STATION that do not start with vowels or do not end with vowels. Your result cannot contain duplicates.

SELECT DISTINCT CITY
FROM STATION 
WHERE CITY NOT REGEXP "^[A,E,I,O,U].*[A,E,I,O,U]$" 

### 12.Query the list of CITY names from STATION that do not start with vowels and do not end with vowels. Your result cannot contain duplicates.

SELECT DISTINCT CITY
FROM STATION
WHERE CITY REGEXP "^[^A,E,I,O,U].*[^A,E,I,O,U]$"

### Students Performance: Query the Name of any student in STUDENTS who scored higher than  Marks. Order your output by the last three characters of each name. 
If two or more students both have names ending in the same last three characters (i.e.: Bobby, Robby, etc.), secondary sort them by ascending ID.

SELECT NAME 
FROM STUDENTS 
WHERE MARKS > 75 
ORDER BY RIGHT(NAME, 3), ID ASC;

### Combine two dataset:left join
select FirstName, LastName,City, State
from Person left join Address
on Person.PersonID = Address.PersonID
;

### Finding Duplicate Email
SELECT Email
FROM Person
GROUP BY Email
HAVING COUNT(Email) > 1

### Delete Duplicate Emails

SELECT p1.*
FROM Person p1,
    Person p2
WHERE
    p1.Email = p2.Email;
    
SELECT p1.*
FROM Person p1,
    Person p2
WHERE
    p1.Email = p2.Email AND p1.Id > p2.Id
;

DELETE p1 FROM Person p1,
    Person p2
WHERE
    p1.Email = p2.Email AND p1.Id > p2.Id

### or

DELETE FROM Person WHERE Id NOT IN 
(SELECT * FROM(
    SELECT MIN(Id) FROM Person GROUP BY Email) as p);



