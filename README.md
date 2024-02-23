# TASK IS ABOUT SQL BOLT

# Below I provided Notes Regarding SQL BOLT TASK

# SQL Lesson 1: SELECT queries 101

 Exercise 1 — Tasks

1)Find the title of each film ✓

 SELECT title FROM movies;

2)Find the director of each film ✓

 SELECT director FROM movies;

3)Find the title and director of each film ✓

 SELECT title,director FROM movies;

4)Find the title and year of each film ✓

 SELECT title,year FROM movies;

5)Find all the information about each film ✓

 SELECT * FROM movies;

------------------------------------------------------------------------------------------------------------

# SQL Lesson 2: Queries with constraints (Pt. 1)

Exercise 2 — Tasks

1)Find the movie with a row id of 6 ✓

SELECT title FROM movies
where id=6;

2)Find the movies released in the years between 2000 and 2010 ✓

SELECT * FROM movies
where year  between 2000 and 2010

3)Find the movies not released in the years between 2000 and 2010 ✓

SELECT * FROM movies
where year not between 2000 and 2010

4)Find the first 5 Pixar movies and their release year ✓

SELECT title,year FROM movies
where  id in (1,2,3,4,5)

------------------------------------------------------------------------------------------------------------
# SQL Lesson 3: Queries with constraints (Pt. 2)

Exercise 3 — Tasks
1)Find all the Toy Story movies ✓

SELECT title FROM movies
where title like "%Toy Story%";

2)Find all the movies directed by John Lasseter ✓

SELECT title FROM movies
where director like "%John Lasseter%";

3)Find all the movies (and director) not directed by John Lasseter ✓

SELECT title FROM movies
where director not like "%John Lasseter%";

4)Find all the WALL-* movies ✓

SELECT title FROM movies
where title  like "%WALL-%";

------------------------------------------------------------------------------------------------------------
# SQL Lesson 4: Filtering and sorting Query results

Exercise 4 — Tasks

1)List all directors of Pixar movies (alphabetically), without duplicates ✓

SELECT distinct director FROM movies order by director; 

2)List the last four Pixar movies released (ordered from most recent to least) ✓

SELECT title,year FROM movies order by year desc limit 4 ; 

3)List the first five Pixar movies sorted alphabetically ✓

SELECT title,year FROM movies order by title  limit 5 ; 

4)List the next five Pixar movies sorted alphabetically ✓

SELECT title,year FROM movies order by title  limit 5 offset 5 ; 

------------------------------------------------------------------------------------------------------------
# SQL Review: Simple SELECT Queries

Review 1 — Tasks

1)List all the Canadian cities and their populations ✓

SELECT city, population FROM north_american_cities
where country like "canada";


2)Order all the cities in the United States by their latitude from north to south ✓

SELECT * FROM north_american_cities where country like "%United States%" order by Latitude desc


3)List all the cities west of Chicago, ordered from west to east ✓

SELECT City FROM north_american_cities 
where longitude < (
 SELECT  longitude FROM 
 north_american_cities
 WHERE city like "chicago")
 order by longitude;


4)List the two largest cities in Mexico (by population) ✓

SELECT * FROM north_american_cities where country like "%mexico%" order by population desc limit 2


5)List the third and fourth largest cities (by population) in the United States and their population ✓

SELECT city, population FROM north_american_cities where country like "%United States%" order by population desc limit 2 offset 2

------------------------------------------------------------------------------------------------------------
# SQL Lesson 6: Multi-table queries with JOINs


Exercise 6 — Tasks

1)Find the domestic and international sales for each movie ✓

SELECT title,Domestic_sales,International_sales FROM Boxoffice 
INNER JOIN Movies   
    ON Movies .Id = Boxoffice.Movie_id
    

2)Show the sales numbers for each movie that did better internationally rather than domestically ✓

SELECT * FROM Boxoffice 
INNER JOIN Movies   
    ON Movies .Id = Boxoffice.Movie_id where International_sales > Domestic_sales
    
3)List all the movies by their ratings in descending order ✓

SELECT * FROM Boxoffice 
INNER JOIN Movies   
ON Movies .Id = Boxoffice.Movie_id order by rating desc

 ------------------------------------------------------------------------------------------------------------

# SQL Lesson 7: OUTER JOINs

Exercise 7 — Tasks
1)Find the list of all buildings that have employees ✓

SELECT distinct Building FROM employees 

2)Find the list of all buildings and their capacity ✓

SELECT  * FROM Buildings 


3)List all buildings and the distinct employee roles in each building (including empty buildings)  ✓ 

SELECT distinct Building_name, role FROM  Buildings  left join Employees on Buildings .Building_name=Employees .Building

------------------------------------------------------------------------------------------------------------
# SQL Lesson 8: A short note on NULLs


Exercise 8 — Tasks
1)Find the name and role of all employees who have not been assigned to a building ✓

SELECT Name,role FROM employees
where building is null;

2)Find the names of the buildings that hold no employees ✓

SELECT * from Buildings left join Employees on Buildings.Building_name = Employees .Building where Years_employed is null

------------------------------------------------------------------------------------------------------------
# SQL Lesson 9: Queries with expressions

Exercise 9 — Tasks

1)List all movies and their combined sales in millions of dollars ✓

SELECT title, (Domestic_sales+International_sales)/1000000 as sales 
FROM movies
inner join Boxoffice on movies.id = Boxoffice.Movie_id ;

2)List all movies and their ratings in percent ✓

SELECT title,rating*10 as ratings
FROM movies
inner join Boxoffice on movies.id = Boxoffice.Movie_id ;

3)List all movies that were released on even number years ✓

SELECT title, year
FROM movies
inner join Boxoffice ON movies.id=Boxoffice.Movie_id
WHERE year%2=0

------------------------------------------------------------------------------------------------------------
# SQL Lesson 10: Queries with aggregates (Pt. 1)

Exercise 10 — Tasks

1)Find the longest time that an employee has been at the studio ✓

  SELECT max(Years_employed) FROM employees;

2)For each role, find the average number of years employed by employees in that role ✓

  SELECT avg(Years_employed) as avg_employee, role FROM employees group by role;

3)Find the total number of employee years worked in each building ✓

  SELECT Building,sum(Years_employed) FROM employees group by building


------------------------------------------------------------------------------------------------------------
# SQL Lesson 11: Queries with aggregates (Pt. 2)

Exercise 11 — Tasks

1)Find the number of Artists in the studio (without a HAVING clause) ✓

SELECT count(Role) as number_of_Artists FROM employees
where role= "Artist";

2)Find the number of Employees of each role in the studio ✓

SELECT role, count(Role) as number_of_Artists FROM employees
group by role

3)Find the total number of years employed by all Engineers ✓

SELECT  role, sum(years_employed) as number_of_Artists FROM employees
group by role HAVING role="Engineer"

------------------------------------------------------------------------------------------------------------
# SQL Lesson 12: Order of execution of a Query

Exercise 12 — Tasks

1)Find the number of movies each director has directed ✓

SELECT director, count(*) as director_movies FROM movies
group by director;

2)Find the total domestic and international sales that can be attributed to each director ✓

SELECT director, sum(International_sales+Domestic_sales) as director_movies
FROM movies inner join Boxoffice
on Movies .id= Boxoffice.Movie_id
group by director;

------------------------------------------------------------------------------------------------------------

# SQL Lesson 13: Inserting rows

Exercise 13 — Tasks

1)Add the studio's new production, Toy Story 4 to the list of movies (you can use any director) ✓

INSERT INTO Movies 
VALUES (4, "Toy Story 4","John Lasseter",2,80);

2)Toy Story 4 has been released to critical acclaim! It had a rating of 8.7, and made 340 million domestically and 270 million internationally. Add the record to the BoxOffice table. ✓

INSERT INTO Boxoffice  
VALUES (4, "8.7",340000000,270000000)

------------------------------------------------------------------------------------------------------------
# SQL Lesson 14: Updating rows

Exercise 14 — Tasks

1)The director for A Bug's Life is incorrect, it was actually directed by John Lasseter ✓

UPDATE Movies
SET Director = "John Lasseter"
   where title="A Bug's Life"

2)The year that Toy Story 2 was released is incorrect, it was actually released in 1999 ✓

UPDATE Movies
SET year = 1999
   where title="Toy Story 2"

3)Both the title and director for Toy Story 8 is incorrect! The title should be "Toy Story 3" and it was directed by Lee Unkrich ✓

UPDATE Movies
SET director = "Lee Unkrich",
title="Toy Story 3"
   where title="Toy Story 8"

------------------------------------------------------------------------------------------------------------
# SQL Lesson 15: Deleting rows

Exercise 15 — Tasks

1)This database is getting too big, lets remove all movies that were released before 2005. ✓

  DELETE FROM Movies
  WHERE year<2005;

2)Andrew Stanton has also left the studio, so please remove all movies directed by him. ✓

 DELETE FROM Movies
 WHERE Director="Andrew Stanton";

------------------------------------------------------------------------------------------------------------
# SQL Lesson 16: Creating tables

Exercise 16 — Tasks

1)Create a new table named Database with the following columns:
– Name A string (text) describing the name of the database
– Version A number (floating point) of the latest version of this database
– Download_count An integer count of the number of times this database was downloaded
This table has no constraints. ✓


 CREATE TABLE Database (
 name text,
 version float,
 download_count integer
 );

------------------------------------------------------------------------------------------------------------
# SQL Lesson 17: Altering tables

Exercise 17 — Tasks

1)Add a column named Aspect_ratio with a FLOAT data type to store the aspect-ratio each movie was released in. ✓

 ALTER TABLE Movies
 ADD Aspect_ratio FLOAT 
    DEFAULT 16;

2)Add another column named Language with a TEXT data type to store the language that the movie was released in. Ensure that the default for this language is English. ✓

 ALTER TABLE Movies
 ADD Language  TEXT  
 DEFAULT English;

------------------------------------------------------------------------------------------------------------

# SQL Lesson 18: Dropping tables

Exercise 18 — Tasks

1)We've sadly reached the end of our lessons, lets clean up by removing the Movies table ✓

 DROP TABLE IF EXISTS Movies ;

2)And drop the BoxOffice table as well ✓

 DROP TABLE IF EXISTS BoxOffice  ;
