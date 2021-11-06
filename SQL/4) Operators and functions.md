#4) SQL operators and functions:

--- 

## - STRING:  
   - ### ||:
 ```sql
 SELECT name || ', ' || country AS location FROM cities;
 ```
   - ### CONCAT():
 ```sql
SELECT CONCAT(name, ', ', country) AS location FROM cities;
 ```
   - ### LOWER():
 ```sql
 SELECT LOWER(CONCAT(name, ', ', country)) AS location FROM cities;
 ```
   - ### LENGTH():
 ```sql
 SELECT name, LENGTH(name) as LengthOfName FROM cities;
 ```
   - ### UPPER():
 ```sql
SELECT
  UPPER(CONCAT(name, ', ', country)) AS location
FROM
  cities;
 ```
## - COMPARISON OPERATORS:    
   - ### = (Is the value equal to?):
 ```sql
SELECT name, area FROM cities WHERE area = 4000;
 ```
   - ### >:
 ```sql
SELECT name, area FROM cities WHERE area > 4000;
 ```
   - ### <:
 ```sql
SELECT name, area FROM cities WHERE area < 4000;
 ```
   - ### >=:
 ```sql
SELECT name, area FROM cities WHERE area >= 4000;
 ```
   - ### IN (Is value presented in a list?):
 ```sql
 SELECT name, area FROM cities WHERE name IN ('Kharkiv', 'Kiev');
 ```
   - ### <=:
 ```sql
SELECT name, area FROM cities WHERE area <= 4000;
 ```
   - ### <> (!=):
 ```sql
SELECT name, area FROM cities WHERE area <> 4000;
 ```
   - ### !=:
 ```sql
SELECT name, area FROM cities WHERE area != 4000;
 ```
   - ### BETWEEN val1 AND val2 (Is value between two other values?):
 ```sql
SELECT name, area FROM cities WHERE area BETWEEN 4000 AND 5000;
 ``` 
   - ### NOT IN (Is the value not presented in a list?):
 ```sql
  SELECT name, area FROM cities WHERE name NOT IN ('Kharkiv', 'Kiev');
 ```
## - AGGREGATE FUNCTIONS:  
   - ### COUNT() (number of values in column != null):
 ```sql
SELECT COUNT(id) FROM cities;
 ```
**For counting amount of rows in column better use:**
 ```sql
SELECT COUNT(*) FROM cities;
 ```
   - ### SUM() (sum of values from column of numbers):
 ```sql
SELECT SUM(area) FROM cities WHERE country = 'Ukraine';
 ```   
   - ### AVG() (average value from column of numbers):
 ```sql
SELECT AVG(population) FROM cities;
 ```   
   - ### MIN() (min value from column of numbers):
 ```sql
SELECT MIN(population) FROM cities;
 ```   
   - ### MAX() (max value from column of numbers):
 ```sql
SELECT MAX(population) FROM cities;
 ```