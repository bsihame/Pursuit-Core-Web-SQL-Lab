SQL Lesson 1: SELECT queries 101
Exercise 1 — Tasks
1.Find the title of each film 
SELECT title FROM movies;

2.Find the director of each film
SELECT 	Director FROM movies;

3.Find the title and director of each film
SELECT Title, Director FROM movies;

4.Find the title and year of each film
SELECT Title, Year FROM movies;

5.Find all the information about each film
SELECT * FROM movies;
=======================================================
//SQL Lesson 2: Queries with constraints (Pt. 1)
Exercise 2 — Tasks
1.Find the movie with a row id of 6 
SELECT Id, Title FROM movies WHERE Id =6;

2.Find the movies released in the years between 2000 and 2010
SELECT Title FROM movies WHERE Year BETWEEN 2000 AND 2010;

3.Find the movies not released in the years between 2000 and 2010
SELECT Title FROM movies WHERE Year NOT BETWEEN 2000 AND 2010;

4.Find the first 5 Pixar movies and their release year
SELECT title, year FROM movies WHERE year <= 2003;
======================================================

SQL Lesson 3: Queries with constraints (Pt. 2)
Exercise 3 — Tasks
1.Find all the Toy Story movies
SELECT Title FROM movies WHERE Title LIKE "Toy Story%";
SELECT * FROM movies WHERE title LIKE "TOY%"

2.Find all the movies directed by John Lasseter
SELECT * FROM movies WHERE director LIKE "JOHN%"
SELECT * FROM movies WHERE director NOT LIKE "JOHN%"

SELECT Title, Director FROM movies WHERE Director LIKE "John Lasseter";
SELECT Title, Director FROM movies WHERE Director NOT LIKE "John Lasseter";
SELECT Title, Director FROM movies WHERE Director NOT LIKE "John Lasseter";

3.Find all the movies (and director) not directed by John Lasseter

4.Find all the WALL-* movies
SELECT * FROM movies WHERE title LIKE "WALL-_"
======================================================

SQL Lesson 4: Filtering and sorting Query results

1.List all directors of Pixar movies (alphabetically), without duplicates
SELECT DISTINCT director FROM movies ORDER BY director ASC;

2.List the last four Pixar movies released (ordered from most recent to least)
SELECT title, year FROM movies ORDER BY year DESC LIMIT 4;

3.List the first five Pixar movies sorted alphabetically
SELECT title FROM movies ORDER BY title ASC LIMIT 5;

4.List the next five Pixar movies sorted alphabetically
SELECT title FROM movies ORDER BY title ASC LIMIT 5 OFFSET 5;
================================================================
SQL Lesson 5: SQL Review: Simple SELECT Queries

List all the Canadian cities and their populations
SELECT city, population FROM north_american_cities WHERE country = 'Canada'

Order all the cities in the United States by their latitude from north to south
SELECT city FROM north_american_cities WHERE Country= 'United States' ORDER BY latitude DESC

List all the cities west of Chicago, ordered from west to east
SELECT city, longitude FROM north_american_cities
WHERE longitude < -87.629798
ORDER BY longitude ASC;

List the two largest cities in Mexico (by population)
SELECT * FROM north_american_cities WHERE Country = "Mexico" ORDER BY population DESC limit 2

List the third and fourth largest cities (by population) in the United States and their population
SELECT * FROM north_american_cities WHERE country='United States' ORDER BY population DESC LIMIT 2 OFFSET 2
==================================================
SQL Lesson 6: Multi-table queries with JOINs
1. Find the domestic and international sales for each movie
SELECT * FROM movies JOIN Boxoffice on id = Movie_id;

2. Show the sales numbers for each movie that did better internationally rather than domestically
SELECT * FROM movies JOIN Boxoffice on id = Movie_id WHERE International_sales > Domestic_sales;

3. List all the movies by their ratings in descending order
SELECT * FROM movies JOIN Boxoffice on id = Movie_id ORDER BY Rating DESC;
===============================================================
SQL Lesson 7: OUTER JOINs
exercise 7 — Tasks
1. Find the list of all buildings that have employees 
SELECT DISTINCT building  FROM employees join Buildings on Building_name = building ;

2. Find the list of all buildings and their capacity
SELECT * FROM Buildings

3. List all buildings and the distinct employee roles in each building (including empty buildings)
SELECT DISTINCT building_name, role FROM buildings LEFT JOIN employees ON building_name = building;
======================================================================
SQL Lesson 8: A short note on NULLs
Exercise 8 — Tasks
1. Find the name and role of all employees who have not been assigned to a building
SELECT name, role FROM employees WHERE building is null
2. Find the names of the buildings that hold no employees
SELECT DISTINCT building_name FROM buildings LEFT JOIN employees ON building_name = building WHERE role IS NULL;
==================================================================
QL Lesson 10: Queries with aggregates (Pt. 1)

Exercise 10 - Tasks

1. Find the longest time that an employee has been at the studio
SELECT Name, MAX(Years_employed) AS Longest_Time
FROM Employees

2. For each role, find the average number of years employed by employees in that role
SELECT Role, AVG(Years_employed)
FROM Employees
GROUP BY Role

3. Find the total number of employee years worked in each building
SELECT Building, SUM(Years_employed)
FROM Employees
GROUP BY Building

====================================================================
SQL Lesson 11: Queries with aggregates (Pt. 2)

Exercise 11 - Tasks
1. Find the number of Artists in the studio (without a HAVING clause)
SELECT COUNT(ROLE)
FROM employees
WHERE Role = 'Artist'

2. Find the number of Employees of each role in the studio
SELECT Role, COUNT(ROLE) AS Number_of_Employees
FROM employees
GROUP BY Role

3. Find the total number of years employed by all Engineers
SELECT Role, SUM(Years_employed) 
FROM employees
GROUP BY Role
HAVING Role = 'Engineer'
====================================================================
SQL Lesson 12: Order of execution of a Query

Exercise 12 — Tasks

1. Find the number of movies each director has directed
SELECT Director, COUNT(*) AS Number_of_movies
FROM movies
GROUP BY Director;
2. Find the total domestic and international sales that can be attributed to each director
SELECT Director, 
    SUM(Domestic_sales + International_sales) AS Total_Sales
FROM movies
INNER JOIN Boxoffice
ON movies.Id = Boxoffice.Movie_id
GROUP BY Director;
SQL Lesson 13: Inserting rows
Exercise 13 — Tasks
1. Add the studio's new production, Toy Story 4 to the list of movies (you can use any director)
INSERT INTO Movies 
VALUES (4, "Toy Story 4", "Karen Morisset", 2019, 98);
2. Toy Story 4 has been released to critical acclaim! It had a rating of 8.7, and made 340 million domestically and 270 million internationally. Add the record to the BoxOffice table.
INSERT INTO Boxoffice  VALUES (4, 8.7, 340000000, 270000000);
===================================================================
SQL Lesson 14: Updating rows
Exercise 14 — Tasks
1. The director for A Bug's Life is incorrect, it was actually directed by John Lasseter
UPDATE Movies
SET Director = "John Lasseter" WHERE Title = "A Bug's Life"
2. The year that Toy Story 2 was released is incorrect, it was actually released in 1999
UPDATE Movies SET Year = 1999 WHERE Id = 3
3. Both the title and director for Toy Story 8 is incorrect! The title should be "Toy Story 3" and it was directed by Lee Unkrich
UPDATE Movies
SET Title = "Toy Story 3", Director = "Lee Unkrich" WHERE Id = 11;
===================================================================
SQL Lesson 15: Deleting rows
Exercise 15 — Tasks
1. This database is getting too big, lets remove all movies that were released before 2005.
DELETE FROM Movies WHERE Year < 2005;
2. Andrew Stanton has also left the studio, so please remove all movies directed by him.
DELETE FROM Movies WHERE Director = "Andrew Stanton";
===================================================================
SQL Lesson 16: Creating tables
Exercise 16 — Tasks
1. Create a new table named Database with the following columns:
– Name A string (text) describing the name of the database
– Version A number (floating point) of the latest version of this database
– Download_count An integer count of the number of times this database was downloaded
CREATE TABLE Database (Name TEXT, Version FLOAT, Download_count INTEGER);
===================================================================
SQL Lesson 17: Altering tables
Exercise 17 — Tasks
1. Add a column named Aspect_ratio with a FLOAT data type to store the aspect-ratio each movie was released in.
ALTER TABLE Movies
ADD Aspect_ratio FLOAT;
2. Add another column named Language with a TEXT data type to store the language that the movie was released in. Ensure that the default for this language is English.
ALTER TABLE Movies ADD Language TEXT DEFAULT English;
===================================================================
SQL Lesson 18: Dropping tables
Exercise 18 — Tasks
1. We've sadly reached the end of our lessons, lets clean up by removing the Movies table
DROP TABLE IF EXISTS Movies;
2. And drop the BoxOffice table as well
DROP TABLE IF EXISTS Boxoffice;
