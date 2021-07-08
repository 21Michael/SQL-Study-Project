# SQL-Study-Project
Studying SQL language on practise

---
# **1) How information stored inside DB:**  
---

# **- Terminology:**  
![link](https://drive.google.com/uc?id=1r54hPU8Y-GwaD5lM7F0KO5WPLUtzsFAQ)

# **- Components:**  
![link](https://drive.google.com/uc?id=1oT_02oPJaWNOkfVJqdwRop-bS9NFu529)

# **- Blocks (8kb):**  
![link](https://drive.google.com/uc?id=1uXWOe5bXCudyBo1HvZdSPIgm9gmkuekM)

# **- Blocks in decimal format (how it stores on HDD):**  
![link](https://drive.google.com/uc?id=1rbjRJAN5RpK1vRhMbDTS4qPTU4Gb4Lbh)

---
# **2) Loading data by query from DB:**  
---

# **- Reaching data by query:**  
#Downsides (slow): for reaching to certain data, all data from table should be uploaded to RAM and
do search one by one.
![link](https://drive.google.com/uc?id=1ukYLA2UBFZtPPrUTFIoBC2KxWdpcJxS2)

---
# **3) Optimizing loading data by query from DB by indexing it:**  
---
# **- Default indexing:**  
#1. Primary key columns (id) indexing by default;  
#2. Postgres automatically indexing for column with unique constrains (CONSTRAINT UNIQUE (column_name));  

# **- Indexing column (indexed can be a certain column in the table):**  
#1. Adding metadata about disposition (block) and unique index to each value;  
#2. Streamlining values depending from type of value (text: alphabet order, number: 0-999...);  
#3. Organize data-structure (tree);  
#4. Use for searching special algorithms (B-tree - default, Hash, GiST, SP-GiST, GIN, BRIN); 
![link](https://drive.google.com/uc?id=1_jPn1G1Lj1B3FxgMVr0vnqvGcrsB01qq)
#5. Data isn't being loaded to RAM;  

#creation:  
```sql
CREATE INDEX ON table_name (column_name);
```

#removing:  
```sql
DROP INDEX index_name_idx;
```
#B-tree index algorithm:  
![link](https://drive.google.com/uc?id=1K1u2-Fg3kS-b-YJ6RodFHXb9kxyg_IaM)

#Internal index files structure:  
![link](https://drive.google.com/uc?id=1cso4wPMrWiT3AK4bec0iyQjlu_M20lsr)

#Downsides:  
# - engage additional storage for metadata in DB (+ 0.21);  
# - slow down such queries like: insert/update/delete because after manipulating with data all indexes should be updated;  
# - !!!doesn't speed up searching for loading many values:  

#Example:  
#1) Indexed random search vs sequel search:  
![link](https://drive.google.com/uc?id=1HXh3cXg9sffjRyhjV2cr8hG3SaI7uIAu)

#2) Operations speed (random search 4 times slower than sequel):  
![link](https://drive.google.com/uc?id=1Bco2E2vYIwhl9xqrlQ1Pg9aoxnoEGf3O)

#3) Query costs:  
![link](https://drive.google.com/uc?id=1bxoEGYo2yjHsvpphNYnWRhBEKCO5CS4d)

#4) Querying many values (example: 600 000):  
# indexed values loading speed: **26 932**;  
# values loading speed: **6 733**;   

#Conclusion: for selecting many values sequel search (load all data to RAM and search one by one) much faster!!!!  
#*Postgresql automatically change random search (un-indexing column) to sequel search if it sees that indexing doesn't bring benefit!  

---
# **4) Query benchmarking:**
---

#check every query (compare execution time):
```sql
EXPLAIN ANALYSE SQL_QUERY
```

# **- NOT NULL:**  
#set rule when creating table:  
```sql
CREATE TABLE table_name (
  column_name DATA TYPE NOT NULL,
);
```

