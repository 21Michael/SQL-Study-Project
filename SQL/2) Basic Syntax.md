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