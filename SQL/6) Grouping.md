#7) Select data from grouped tables (GROUP BY):

---

 - **Basic (allowed selecting columns only by witch table was grouped!!!):**
 ```sql
  SELECT user_id
  FROM comments
  GROUP BY user_id
 ```
Result:
![link](https://drive.google.com/uc?id=16nyugmLnL2uayVQo_hfGKmP1CSpgr86_)


#7.1) Select grouped data by aggregate functions (GROUP BY + aggregation functions):

---

 - **Basic (allowed selecting columns from grouped rows!!!):**
 ```sql
  SELECT MAX(id)
  FROM comments
  GROUP BY user_id
 ```
result:  
![link](https://drive.google.com/uc?id=1UmJqsLCF3ue1jrNFvKvX_pD2EMxTWUDo)

#7.2) Filtering grouped data (GROUP BY + HAVING):  
 ```sql
  SELECT photo_id, COUNT(*)
  FROM comments
  WHERE photo_id < 3
  GROUP BY photo_id
  HAVING COUNT(*) > 2;
 ```
Result:
![link](https://drive.google.com/uc?id=1NX-BU3C2nYta9oXPjy7WY2g3PUrPyPbV)
