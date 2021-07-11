# SQL-Study-Project
Studying SQL language on practise

---
# **1) Datatype:**
---

Text types

| Data type        | Description                                                                                                                                                                                                                                                                                      |
|------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| CHAR(size)       | Holds a fixed length string (can contain letters, numbers, and special characters). The fixed size is specified in parenthesis. Can store up to 255 characters                                                                                                                                   |
| VARCHAR(size)    | Holds a variable length string (can contain letters, numbers, and special characters). The maximum size is specified in parenthesis. Can store up to 255 characters. Note: If you put a greater value than 255 it will be converted to a TEXT type                                               |
| TINYTEXT         | Holds a string with a maximum length of 255 characters                                                                                                                                                                                                                                           |
| TEXT             | Holds a string with a maximum length of 65,535 characters                                                                                                                                                                                                                                        |
| BLOB             | For BLOBs (Binary Large OBjects). Holds up to 65,535 bytes of data                                                                                                                                                                                                                               |
| MEDIUMTEXT       | Holds a string with a maximum length of 16,777,215 characters                                                                                                                                                                                                                                    |
| MEDIUMBLOB       | For BLOBs (Binary Large OBjects). Holds up to 16,777,215 bytes of data                                                                                                                                                                                                                           |
| LONGTEXT         | Holds a string with a maximum length of 4,294,967,295 characters                                                                                                                                                                                                                                 |
| LONGBLOB         | For BLOBs (Binary Large OBjects). Holds up to 4,294,967,295 bytes of data                                                                                                                                                                                                                        |
| ENUM(x,y,z,etc.) | Let you enter a list of possible values. You can list up to 65535 values in an ENUM list. If a value is inserted that is not in the list, a blank value will be inserted.Note: The values are sorted in the order you enter them.You enter the possible values in this format: ENUM('X','Y','Z') |
| SET              | Similar to ENUM except that SET may contain up to 64 list items and can store more than one choice                                                                                                                                                                                               |

Number types

| Data type       | Description                                                                                                                                                                                                                           |
|-----------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| TINYINT(size)   | -128 to 127 normal. 0 to 255 UNSIGNED*. The maximum number of digits may be specified in parenthesis                                                                                                                                  |
| SMALLINT(size)  | -32768 to 32767 normal. 0 to 65535 UNSIGNED*. The maximum number of digits may be specified in parenthesis                                                                                                                            |
| MEDIUMINT(size) | -8388608 to 8388607 normal. 0 to 16777215 UNSIGNED*. The maximum number of digits may be specified in parenthesis                                                                                                                     |
| INT(size)       | -2147483648 to 2147483647 normal. 0 to 4294967295 UNSIGNED*. The maximum number of digits may be specified in parenthesis                                                                                                             |
| BIGINT(size)    | -9223372036854775808 to 9223372036854775807 normal. 0 to 18446744073709551615 UNSIGNED*. The maximum number of digits may be specified in parenthesis                                                                                 |
| FLOAT(size,d)   | A small number with a floating decimal point. The maximum number of digits may be specified in the size parameter. The maximum number of digits to the right of the decimal point is specified in the d parameter                     |
| DOUBLE(size,d)  | A large number with a floating decimal point. The maximum number of digits may be specified in the size parameter. The maximum number of digits to the right of the decimal point is specified in the d parameter                     |
| DECIMAL(size,d) | A DOUBLE stored as a string , allowing for a fixed decimal point. The maximum number of digits may be specified in the size parameter. The maximum number of digits to the right of the decimal point is specified in the d parameter |

Date types

| Data type   | Description                                                                                                                                                                                                                              |
|-------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| DATE()      | A date. Format: YYYY-MM-DDNote: The supported range is from '1000-01-01' to '9999-12-31'                                                                                                                                                 |
| DATETIME()  | *A date and time combination. Format: YYYY-MM-DD HH:MI:SSNote: The supported range is from '1000-01-01 00:00:00' to '9999-12-31 23:59:59'                                                                                                |
| TIMESTAMP() | *A timestamp. TIMESTAMP values are stored as the number of seconds since the Unix epoch ('1970-01-01 00:00:00' UTC). Format: YYYY-MM-DD HH:MI:SSNote: The supported range is from '1970-01-01 00:00:01' UTC to '2038-01-09 03:14:07' UTC |
| TIME()      | A time. Format: HH:MI:SSNote: The supported range is from '-838:59:59' to '838:59:59'                                                                                                                                                    |
| YEAR()      | A year in two-digit or four-digit format.Note: Values allowed in four-digit format: 1901 to 2155. Values allowed in two-digit format: 70 to 69, representing years from 1970 to 2069                                                     |

---
# **2) SQL syntax:**  
---
# **- Create table (CREATE):**  
#basic:
```sql
CREATE TABLE table_name (
  column_name DATA TYPE,
);
```
# **- Insert data (INSERT):**  
#insert one row:
```sql
INSERT INTO table_name (column1, column2, column3, column4)
VALUES (value1, value2, value3, value4);
```
#insert many rows:
```sql
INSERT INTO table_name (column1, column2, column3, column4)
VALUES
(value1, value2, value3, value4),
(value1, value2, value3, value4),
(value1, value2, value3, value4);
```
# **- Select data (SELECT):**  
#select all:
```sql
SELECT * FROM cities;
```
#select certain columns:
```sql
SELECT name, country FROM cities;
```
#select column with new name (AS):
```sql
SELECT name AS location FROM cities;

SELECT name || ', ' || country AS location FROM cities;

SELECT CONCAT(name, ', ', country) AS location FROM cities;
```
#select unique values from column (DISTINCT):  
existing table:  

| id         |city         | office       | population     |
|------------|-------------|--------------|----------------|
| 25543      | Kiev        | 1            | 5000           |
| 24542      | Kiev        | 2            | 8000           |
| 26545      | Kiev        | 3            | 1000           |
| 46346      | Kharkiv     | 1            | 5000           |
| 45366      | Kharkiv     | 2            | 6000           |
| 48336      | Kharkiv     | 3            | 12000          |

```sql
SELECT DISTINCT city FROM offices;
```
result:  

| city       |
|------------|
| Kiev       |
| Kharkiv    |

#select the greatest value from list of values (GREATEST):
```sql
SELECT GREATEST(300, 400, 200);
```
result:  
400  

select values grater than 30 or less:   
existing table:  

| price      |
|------------|
| 23         |
| 106        |
| 13         |
| 56         |
| 02         |
| 73         |

```sql
SELECT GREATEST(30, price) FROM price;
```
result:  

| greatest   |
|------------|
| less       |
| 106        |
| less       |
| 56         |
| less       |
| 73         |

#select the least value from list of values (LEAST):  
```sql
SELECT GREATEST(300, 400, 200);
```
result:  
200

select values least than 30 or :  
```sql
SELECT LEAST(price, 30) FROM price;
```
result:

| least      |
|------------|
| 23         |
| high       |
| 13         |
| high       |
| 02         |
| high       |

#select by switch case analog (CASE):
```sql
SELECT 
CASE
  WHEN price > 50 THEN 'high'
  WHEN pricce < 20 THEN 'low'
  ELSE 'medium'
END
FROM price;
```
result:  

| price      |
|------------|
| 'medium'   |
| 'high'     |
| 'low'      |
| 'high'     |
| 'low'      |
| 'high'     |

# **- Filter selected data (WHERE):**  
#filter data by comparison operators:
```sql
SELECT name, area FROM cities WHERE area > 4000;
```
#filter data by many diff filters (WHERE + AND):
```sql
SELECT name, area FROM cities WHERE area > 4000 AND name IN ('Kiev', 'Kharkiv');
```
result:  

| id   | name   | area |
|------|--------|------|
| 1    | Kiev   | 5000 |

#filter data by many filters if at least one is true (WHERE + OR):
```sql
SELECT name, area FROM cities WHERE area > 4000 OR name IN ('Kiev', 'Kharkiv');
```
result:  

| id   | name   | area |
|------|--------|------|
| 1    | Kiev   | 2000 |
| 2    | Odessa | 4500 |

#filter data by calculated filter (WHERE + operators):
```sql
SELECT population, area FROM cities WHERE population / area > 4000;
```

#  **- Update data (UPDATE):**  
#basic (update every coincidence!!!):
```sql
UPDATE cities SET popuation = 36346 WHERE name = 'Odessa';
```
#  **- Delete data (DELETE):**  
#basic (delete every coincidence!!!):
```sql
DELETE FROM cities WHERE name = 'Kiev';
```

#  **- Sort data (ORDER BY):**
#descending (DESC):
```sql
SELECT name FROM cities ORDER BY name DESC;
```
result:  

| id   | name      |
|------|-----------|
| 1    | Chicago   |
| 3    | Budapest  |
| 2    | Alushta   |

#ascending *default (ASC):
```sql
SELECT name FROM cities ORDER BY name ASC;
```
result:  

| id   | name      |
|------|-----------|
| 2    | Alushta   |
| 3    | Budapest  |
| 1    | Chicago   |

#  **- Limit amount of selecting data (LIMIT):**
#basic:
```sql
SELECT name FROM cities LIMIT 1;
```
result:  

| id   | name      |
|------|-----------|
| 2    | Alushta   |

#  **- Offset (start from) selecting data (OFFSET):**
#basic:
```sql
SELECT name FROM cities OFFSET 1;
```
result:  

| id   | name      |
|------|-----------|
| 3    | Budapest  |
| 1    | Chicago   |

---
# **2.1) Unit two queries (can unite only columns with same names and data types!!!):**
---

#  **- Select data from two queries with all common rows from both queries (UNION ALL):**
#basic:
```sql
(
  SELECT * FROM cities 
  ORDER BY name
  LIMIT 3
)
UNION ALL
(
  SELECT * FROM cities 
  ORDER BY population
  LIMIT 3
);
```
result:
1) order by name:  

| id   | name      | population |
|------|-----------|------------|
| 9    | Alushta   | 1000       |
| 3    | Budapest  | 3000       |
| 1    | Chicago   | 2000       |

2) order by population:  

| id   | name        | population |
|------|-------------|------------|
| 7    | New York    | 8000       |
| 35   | Los Angeles | 5000       |
| 3    | Budapest    | 3000       |

3) united:  

| id   | name        | population |
|------|-------------|------------|
| 9    | Alushta     | 1000       |
| 3    | Budapest    | 3000       |
| 1    | Chicago     | 2000       |
| 7    | New York    | 8000       |
| 35   | Los Angeles | 5000       |
| 3    | Budapest    | 3000       |

#  **- Select data from two queries excepting all common rows from both queries (UNION):**  
result (senseless, every order are broken!!!):

| id   | name        | population |
|------|-------------|------------|
| 9    | Alushta     | 1000       |
| 35   | Los Angeles | 5000       |
| 1    | Chicago     | 2000       |

#  **- Select same rows from two queries without duplicates (INTERSECT):**  
result:

| id   | name        | population |
|------|-------------|------------|
| 3    | Budapest    | 3000       |

#  **- Select same rows from two queries (INTERSECT ALL):**  
result:

| id   | name        | population |
|------|-------------|------------|
| 3    | Budapest    | 3000       |

#  **- Select rows that exist in first query but doesn't in second without duplicates (EXCEPT):**  
result:

| id   | name      | population |
|------|-----------|------------|
| 9    | Alushta   | 1000       |
| 1    | Chicago   | 2000       |

#  **- Select rows that exist in first query but doesn't in second (EXCEPT ALL):**  
result:

| id   | name      | population |
|------|-----------|------------|
| 9    | Alushta   | 1000       |
| 1    | Chicago   | 2000       |

---
# **3) Sub-queries (sub-query AS):**  
--- 

#  **- Sub-query in SELECT statement:**  
#basic (can be selected only **single value**):  
```sql
SELECT name, population, (
 SELECT COUNT(area) FROM cities WHERE country = 'Ukraine'
) AS country_area
 FROM cities WHERE country = 'Ukraine';
```
result:  

| id   | name      | population | country_area |
|------|-----------|------------|--------------|
| 1    | Kiev      | 7000       | 603 628      |
| 2    | Lviv      | 4000       | 603 628      |
| 3    | Kharkiv   | 6000       | 603 628      |
| 4    | Dnipro    | 4000       | 603 628      |

#mixing sub-queries (can be selected only **single value**):
```sql
SELECT (
  SELECT MAX(area) FROM cities WHERE country = 'Ukraine'  
) /
(
  SELECT MIN(area) FROM cities WHERE country = 'Ukraine'  
);
```
result:  
2767.56  

#select data from joined table (can be selected only **single value**):  
```sql
SELECT name, population, (
  SELECT COUNT(*) 
  FROM cities 
  WHERE cities.country_id = country.id
) AS cities_amount
FROM country;
```
result:

| id   | name      | population | cities_amount |
|------|-----------|------------|---------------|
| 1    | Ukraine   | 67000      | 93            |
| 2    | Litva     | 46000      | 46            |
| 3    | UK        | 62000      | 69            |
| 4    | Spain     | 44000      | 78            |

#  **- Sub-query in FROM statement:**  
#basic (can be selected only **columns** that will be extracted in outside SELECT statement):
```sql
SELECT AVG(amount_of_cities)
FROM (
  SELECT country, COUNT(name) AS amount_of_cities 
  FROM cities
  GROUP BY country
) 
AS p;
```
result:  
1)sub-query:  

| country  | amount_of_cities  |
|----------|-------------------|
| UK       | 697               | 
| Ukraine  | 235               |
| USA      | 2678              |
| France   | 798               |

2)average amount of cities ((697 + 235 + 2678 + 798) / 4):  
1099.75  

#  **- Sub-query in JOIN statement:**  
#basic (can be selected only **columns** that will be extracted in outside SELECT statement):
```sql
SELECT id, name 
FROM counties
JOIN (
  SELECT country_id FROM unions WHERE union_name = 'European union'
) AS EU_countries
ON EU_countries.country_id = countries.id
```
result:  
1)sub-query (EU_countries):  

| country_id |
|------------|
| 25543      |
| 46346      |
| 76577      |
| 34534      |

2)id, name:  

| id         | name        |
|------------|-------------|
| 25543      | Germany     |
| 46346      | France      |
| 76577      | Italy       |
| 34534      | Netherlands |  

#  **- Sub-query in WHERE + operator (>,=,!=...) statement:**  
#basic (can be selected only **single value** that will be extracted in outside SELECT statement):  
```sql
SELECT name, country_id 
FROM cities
WHERE id = (
  SELECT id FROM countries WHERE name = 'Ukraine'
);
```
result:  
1)sub-query:  

| id            |
|---------------|
| 56522876837   |

2)id, name:  

| name        | country_id  |
|-------------|-------------|
| Kiev        | 56522876837 |
| Odessa      | 56522876837 |
| Lviv        | 56522876837 |
| Kharkiv     | 56522876837 |  

#  **- Sub-query in WHERE + special word (IN, (>,=,!=...) + ALL/SOME/ANY) statement:**  
#IN operator (can be selected only **single column** that will be extracted in outside SELECT statement):
```sql
SELECT id, name 
FROM counties
WHERE id IN (
  SELECT country_id FROM unions WHERE union_name = 'European union'
);
```
result:  
1)sub-query:  

| country_id |
|------------|
| 25543      |
| 46346      |
| 76577      |
| 34534      |

2)id, name:  

| id         | name        |
|------------|-------------|
| 25543      | Germany     |
| 46346      | France      |
| 76577      | Italy       |
| 34534      | Netherlands |  

# >ALL (grater than all column values) operator:  
```sql
SELECT name, population 
FROM counties
WHERE population > ALL (
  SELECT population FROM countries WHERE partisipant_of_EU = true
);
```
result:  
1)sub-query:

| population |
|------------|
| 9000       |
| 7000       |
| 4000       |
| 5000       |

2)name, population:

| name        | population |
|-------------|------------|
| UK          | 16000      |
| Russia      | 29000      |
| Ukraine     | 12000      |
| Turkey      | 19000      |  

# >SOME/ANY (grater than at least one of values from column) operator:  
```sql
SELECT name, population 
FROM counties
WHERE population > ANY (
  SELECT population FROM countries WHERE partisipant_of_EU = true
);
```
result:  
1)sub-query:

| population |
|------------|
| 9000       |
| 7000       |
| 4000       |
| 5000       | 

2)name, population:

| name        | population |
|-------------|------------|
| Iceland     | 5300       |
| UK          | 16000      |
| Norway      | 4200       |
| Russia      | 29000      |
| Ukraine     | 12000      |
| Switzerland | 8000       |
| Turkey      | 19000      | 

#  **- Sub-query loop by WHERE + special operator (>,=,!=...) statement:**  
# executing table:   

| id         |city         | office       | population     |
|------------|-------------|--------------|----------------|
| 25543      | Kiev        | 1            | 5000           |
| 24542      | Kiev        | 2            | 8000           |
| 26545      | Kiev        | 3            | 1000           |
| 46346      | Kharkiv     | 1            | 5000           |
| 45366      | Kharkiv     | 2            | 6000           |
| 48336      | Kharkiv     | 3            | 12000          |
| 72577      | Lviv        | 1            | 900            |
| 76575      | Lviv        | 2            | 8000           |
| 76572      | Lviv        | 3            | 2000           |

#basic (the biggest office in each city):
```sql
SELECT city, office, population 
FROM offices AS of1
WHERE population = (
  SELECT MAX(population) 
  FROM offices AS of2
  WHERE of2.city = of1.city
);
```
iterations:  
1.1)sub-query (max population for Kiev = Kiev):  
8000  
1.2)city, office, population (population = 8000):

| city         | office       | population     |
|--------------|--------------|----------------|
| Kiev         | 2            | 8000           |

2.1)sub-query (max population for Kharkiv = Kharkiv):  
12000  
2.2)city, office, population (population = 12000):

| city         | office       | population     |
|--------------|--------------|----------------|
| Kharkiv      | 3            | 12000          |

3.1)sub-query (max population for Lviv = Lviv):  
8000  
3.2)city, office, population (population = 8000):

| city         | office       | population     |
|--------------|--------------|----------------|
| Lviv         | 2            | 8000           |

result:  

| city         | office       | population     |
|--------------|--------------|----------------|
| Kiev         | 2            | 8000           |
| Kharkiv      | 3            | 12000          |
| Lviv         | 2            | 8000           |

---
# **4) SQL operators and functions:**  
--- 

# - STRING:  
   - # ||:
 ```sql
 SELECT name || ', ' || country AS location FROM cities;
 ```
   - # CONCAT():
 ```sql
SELECT CONCAT(name, ', ', country) AS location FROM cities;
 ```
   - # LOWER():
 ```sql
 SELECT LOWER(CONCAT(name, ', ', country)) AS location FROM cities;
 ```
   - # LENGTH():
 ```sql
 SELECT name, LENGTH(name) as LengthOfName FROM cities;
 ```
   - # UPPER():
 ```sql
SELECT
  UPPER(CONCAT(name, ', ', country)) AS location
FROM
  cities;
 ```
# - COMPARISON OPERATORS:    
   - # = (Is the value equal to?):
 ```sql
SELECT name, area FROM cities WHERE area = 4000;
 ```
   - # >:
 ```sql
SELECT name, area FROM cities WHERE area > 4000;
 ```
   - # <:
 ```sql
SELECT name, area FROM cities WHERE area < 4000;
 ```
   - # >=:
 ```sql
SELECT name, area FROM cities WHERE area >= 4000;
 ```
   - # IN (Is value presented in a list?):
 ```sql
 SELECT name, area FROM cities WHERE name IN ('Kharkiv', 'Kiev');
 ```
   - # <=:
 ```sql
SELECT name, area FROM cities WHERE area <= 4000;
 ```
   - # <> (!=):
 ```sql
SELECT name, area FROM cities WHERE area <> 4000;
 ```
   - # !=:
 ```sql
SELECT name, area FROM cities WHERE area != 4000;
 ```
   - # BETWEEN val1 AND val2 (Is value between two other values?):
 ```sql
SELECT name, area FROM cities WHERE area BETWEEN 4000 AND 5000;
 ``` 
   - # NOT IN (Is the value not presented in a list?):
 ```sql
  SELECT name, area FROM cities WHERE name NOT IN ('Kharkiv', 'Kiev');
 ```
# - AGGREGATE FUNCTIONS:  
   - # COUNT() (number of values in column != null):
 ```sql
SELECT COUNT(id) FROM cities;
 ```
#for counting amount of rows in column better use:
 ```sql
SELECT COUNT(*) FROM cities;
 ```
   - # SUM() (sum of values from column of numbers):
 ```sql
SELECT SUM(area) FROM cities WHERE country = 'Ukraine';
 ```   
   - # AVG() (average value from column of numbers):
 ```sql
SELECT AVG(population) FROM cities;
 ```   
   - # MIN() (min value from column of numbers):
 ```sql
SELECT MIN(population) FROM cities;
 ```   
   - # MAX() (max value from column of numbers):
 ```sql
SELECT MAX(population) FROM cities;
 ```

---
# **5) Relationships between tables:**
---

# - Concepts: ONE TO MANY / MANY TO ONE:
![link](https://drive.google.com/uc?id=1Hk3QN_KgQsuucXoiz8sS_eSm1rrLmqVB)
# - Create tables with relation (PRIMARY KEY, REFERENCES):
 ```sql
CREATE TABLE users (
  id SERIAL PRIMARY KEY,
  username VARCHAR(50)
);

INSERT INTO users (username)
VALUES
	('monahan93'),
  ('pferrer'),
  ('si93onis'),
  ('99stroman');

CREATE TABLE photos (
  id SERIAL PRIMARY KEY,
  url VARCHAR(200),
  user_id INTEGER REFERENCES users(id)
);

INSERT INTO photos (url, user_id)
VALUES
	('http://two.jpg', 1),
  ('http://25.jpg', 1),
  ('http://36.jpg', 1),
  ('http://754.jpg', 2),
  ('http://35.jpg', 3),
  ('http://256.jpg', 4);
 ```
result: 
 1) users

| id   | username  |
|------|-----------|
| 1    | monahan93 |
| 2    | pferrer   |
| 3    | si93onis  |
| 4    | 99stroman |

2) photos

 | id   | url               | user_id  |
 |------|-------------------|----------|
 | 1    | http://two.jpg    | 1        |
 | 2    | http://25.jpg     | 3        |
 | 3    | http://36.jpg     | 4        |
 | 4    | http://754.jpg    | 2        |
 | 5    | http://35.jpg     | 2        |
 | 6    | http://256.jpg    | 2        |
 
![link](https://drive.google.com/uc?id=1T0fglgZVUTgzWr7az4EuvhgpzBP9VfZI)

---
# **6) Select data from joined tables (JOIN ON):**   
---

#basic:
 ```sql
SELECT url, username FROM photos
JOIN users ON users.id = photos.user_id;
 ```
result:

 | url               | username  |
 |-------------------|-----------|
 | http://two.jpg    | monahan93 |
 | http://754.jpg    | pferrer   |
 | http://35.jpg     | pferrer   |
 | http://256.jpg    | pferrer   |
 | http://25.jpg     | si93onis  |
 | http://36.jpg     | 99stroman |
 
#if id of table1 doesn't exist in table2:  
 ```sql
SELECT * FROM photos
 ```
1) users

 | id   | username  |
 |------|-----------|
 | 1    | monahan93 |

2) photos

 | id   | url               | user_id  |
 |------|-------------------|----------|
 | 1    | http://two.jpg    | 2686     |
 
result: **Error**    
#if id of table1 doesn't exist in table2 (id: NULL):  
1) users

 | id   | username  |
 |------|-----------|
 | 1    | monahan93 |

2) photos

 | id   | url               | user_id  |
 |------|-------------------|----------|
 | 1    | http://two.jpg    | null     | 
 
result:

 | id   | url               | user_id  |
 |------|-------------------|----------|
 | 1    | http://two.jpg    | null     |

#if column with same name repeated in both tables (table.column):
 ```sql
SELECT photos.id FROM photos
JOIN users ON users.id = photos.user_id;
 ```
![link](https://drive.google.com/uc?id=1Ruokio9nZ2kiyAZgouDzGpNQ-f6PdATz)

#if some of the rows doesn't have relation (JOIN TYPES):
![link](https://drive.google.com/uc?id=1JvMmO2aZzxLMbyT3_6KEfhcNN014CV4a)

#filter joined data (JOIN + WHERE):
 ```sql
SELECT url, photos
FROM comments
JOIN photos ON photos.id = comments.photo_id;
WHERE comments.user_id - photos.user_id;
 ```
![link](https://drive.google.com/uc?id=10jVMi3Z_JRnBeFJhTAzgmRkgKtsHTQ5T)

#join 3 tables (JOIN ON):
 ```sql
SELECT contents, url, username
FROM comments
JOIN photos ON photos.id = comments.photo_id;
Join users ON users.id = photos.user_id AND users.id = comments.user_id
 ```
![link](https://drive.google.com/uc?id=1Io8I2dBaQszIkWCqsgRBfsQ8Gpu6EqfA)

# - Delete joined data (ON DELETE):  
#basic:
 ```sql
DELETE FROM users WHERE id = 1;
 ```
result: **Error**    
#cascade:
 ```sql
CREATE TABLE photos (
  id SERIAL PRIMARY KEY,
  url VARCHAR(200),
  user_id INTEGER REFERENCES users(id)
  ON DELETE CASCADE
);

DELETE FROM users WHERE id = 1;
 ```
result:

| id   | url               | user_id  |
|------|-------------------|----------|
| 2    | http://25.jpg     | 3        |
| 3    | http://36.jpg     | 4        |
| 4    | http://754.jpg    | 2        |
| 5    | http://35.jpg     | 2        |
| 6    | http://256.jpg    | 2        |

#set null:
 ```sql
CREATE TABLE photos (
  id SERIAL PRIMARY KEY,
  url VARCHAR(200),
  user_id INTEGER REFERENCES users(id)
  ON DELETE SET NULL
);

DELETE FROM users WHERE id = 1;
 ```
result:

| id   | url               | user_id  |
|------|-------------------|----------|
| 1    | http://two.jpg    | null     |
| 2    | http://25.jpg     | 3        |
| 3    | http://36.jpg     | 4        |
| 4    | http://754.jpg    | 2        |
| 5    | http://35.jpg     | 2        |
| 6    | http://256.jpg    | 2        |

![link](https://drive.google.com/uc?id=1JyxYvcPwbZIWnjYBVBrqJzn4e9hw6UJh)

---
# **7) Select data from grouped tables (GROUP BY):**  
---
#basic (allowed selecting columns only by witch table was grouped!!!):
 ```sql
SELECT user_id
FROM comments
GROUP BY user_id
 ```
result:
![link](https://drive.google.com/uc?id=16nyugmLnL2uayVQo_hfGKmP1CSpgr86_)

---
# **7.1) Select grouped data by aggregate functions (GROUP BY + aggregation functions):**  
---
#basic (allowed selecting columns from grouped rows!!!):
 ```sql
SELECT MAX(id)
FROM comments
GROUP BY user_id
 ```
result:  
![link](https://drive.google.com/uc?id=1UmJqsLCF3ue1jrNFvKvX_pD2EMxTWUDo)

# - Filtering grouped data (GROUP BY + HAVING):  
 ```sql
SELECT photo_id, COUNT(*)
FROM comments
WHERE photo_id < 3
GROUP BY photo_id
HAVING COUNT(*) > 2;
 ```
result:
![link](https://drive.google.com/uc?id=1NX-BU3C2nYta9oXPjy7WY2g3PUrPyPbV)
---
# **8) Transactions:**  
---

- ACID:
  - Atomicity;
  - Consistency;
  - Isolation;
  - Durability;
- SQL syntax:
  - COMMIT;
  - ROLLBACK;
  - SAVEPOINT;
  - SET TRANSACTION;
