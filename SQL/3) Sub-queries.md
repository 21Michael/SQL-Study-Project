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
#Iterations:  
1.1) sub-query (max population for Kiev = Kiev):  
8000  
1.2) city, office, population (population = 8000):  

| city         | office       | population     |
|--------------|--------------|----------------|
| Kiev         | 2            | 8000           |

2.1) sub-query (max population for Kharkiv = Kharkiv):  
12000  
2.2) city, office, population (population = 12000):

| city         | office       | population     |
|--------------|--------------|----------------|
| Kharkiv      | 3            | 12000          |

3.1) sub-query (max population for Lviv = Lviv):  
8000  
3.2) city, office, population (population = 8000):

| city         | office       | population     |
|--------------|--------------|----------------|
| Lviv         | 2            | 8000           |

result:  

| city         | office       | population     |
|--------------|--------------|----------------|
| Kiev         | 2            | 8000           |
| Kharkiv      | 3            | 12000          |
| Lviv         | 2            | 8000           |
