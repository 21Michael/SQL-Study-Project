---
# **1) Common Table Expression (optimizing sub-query expressions):**  
---
#sub-query expression:  
```sql
SELECT id, name 
FROM counties
JOIN (
  SELECT country_id FROM unions WHERE union_name = 'European union'
) AS EU_countries
ON EU_countries.country_id = countries.id
```
#sub-query optimized by common-table-expression (WITH ... AS):
```sql
WITH EU_countries AS (
  SELECT country_id FROM unions WHERE union_name = 'European union'
)
SELECT id, name 
FROM counties
JOIN ON EU_countries.country_id = countries.id
```

