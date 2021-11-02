---
# **1) Materialized view - view that doesn't being updated automatically if data in tables, on which view referenced, updated and every time gets cached value (CREATE MATERIALIZED VIEW ... AS ...). For updating is used special query (REFRESH MATERIALIZED VIEW ...):**  
---

#Usage:
#Used for difficult queries with long processing time (instead updating every time when referenced table was changed, update certain amount of times in some time):  

#1. query expression (execution time: 15sec):  
![link](https://drive.google.com/uc?id=1CyU5xnGDbp3YVuzFQgv45A3ZuVqwKT8e)

#2. create materialized view (first execution time: 15sec, next: 0.0425sec):
![link](https://drive.google.com/uc?id=1cw2NEXcZ_iZhRlOXDvsuZ0i9R1z_iKME)

#3. updating materialized view (one's per week):
```sql
REFRESH MATERIALIZED VIEW weekly_likes;
```