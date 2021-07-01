# SQL-Study-Project
Studying SQL language on practise

---
# **1) SQL syntax:**  
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
# **2) SQL operators and functions:**  
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
 
---
# **3) Transactions:**
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
