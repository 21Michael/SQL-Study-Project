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
# **- Filter selected data (WHERE):**  
#filter data by comparison operators:
```sql
SELECT name, area FROM cities WHERE area > 4000;
```
#filter data by many diff filters (WHERE + AND):
```sql
SELECT name, area FROM cities WHERE area > 4000 AND name IN ('Kiev', 'Kharkiv');
```
result: { name: 'Kiev' area: 4574}

#filter data by many filters if at least one is true (WHERE + OR):
```sql
SELECT name, area FROM cities WHERE area > 4000 OR name IN ('Kiev', 'Kharkiv');
```
result: {   
  name: 'Kiev' area: 2000,  
  name: 'Odessa' area: 4500,  
}

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

---
# **3) SQL operators and functions:**  
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

# **4) Relationships between tables:**
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
   
# - Select data from joined tables (JOIN ON):  
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
![link](https://drive.google.com/uc?id=1C_7ckv9XOfyV0552c3ybXwmPJ_o3cEmO)

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
SELECT url, photos, username
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
# **5) Transactions:**
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
