#2) View - table that referenced to other tables data "if data in tables, on which view referenced, updated, view will be automatically updated too" (CREATE VIEW ... AS ...):

---

## Usage:  
### 1) Creating reference tables based on sub-query for simplifying SQL query:  
**Sub-query expression:**
```sql
SELECT id, name 
FROM counties
JOIN (
  SELECT country_id FROM unions WHERE union_name = 'European union'
) AS EU_countries
ON EU_countries.country_id = countries.id;
```
**1. Creating view (EU_countries reference table):**  
```sql
CREATE VIEW EU_countries AS (
  SELECT country_id FROM unions WHERE union_name = 'European union'
);
```
**2. Referencing right to view table (EU_countries) instead of making a sub-query:**  
```sql
SELECT id, name 
FROM counties
JOIN ON EU_countries.country_id = countries.id;
```
### 2) Creating reference tables for often used tables (top 10...) instead of ordering and selecting query every time:  
**1. Selecting an ordering query (top biggest):**
```sql
SELECT id, name 
FROM cities
ORDER BY population
LIMIT 5;
```
**2. Creating view (top_biggest):**
```sql
CREATE VIEW top_biggest AS (
  SELECT id, name 
  FROM cities
  ORDER BY population
  LIMIT 5
);
```
**3. Selecting from view:**
```sql
SELECT * FROM top_biggest;
```
Result (top_biggest view):  

| id  | name       | population |
|-----|------------|------------|
| 2   | Kiev       | 20 000     |
| 8   | Kharkiv    | 13 000     |
| 5   | Odessa     | 10 000     |
| 6   | Dnepr      | 8 000      |
| 4   | Donetsk    | 7 500      |

**4. Updating view referenced table (city):**  
```sql
INSERT INTO cities (name, population)
VALUES (Moscow, 90 000)
```
**5. View table was updated automatically:**   
```sql
SELECT * FROM top_biggest;
```
Result (top_biggest view):  

| id  | name       | population |
|-----|------------|------------|
| 586 | Moscow     | 90 000     |
| 2   | Kiev       | 20 000     |
| 8   | Kharkiv    | 13 000     |
| 5   | Odessa     | 10 000     |
| 6   | Dnepr      | 8 000      |
| 4   | Donetsk    | 7 500      | 

##  **Syntax:**  
### 1) Creating (CREATE VIEW ... AS ...):  
```sql
CREATE VIEW table_name AS (query for creating view table);
```
### 2) Updating (REPLACE VIEW ... AS ...):  
```sql
REPLACE VIEW table_name AS (query for creating new view table);
```
### 3) Deleting (DROP VIEW ...):  
```sql
DROP VIEW table_name;
```