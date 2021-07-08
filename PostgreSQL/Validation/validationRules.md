# SQL-Study-Project
Studying SQL language on practise

---
# **1) Default validation rules:**  
---

# **- NOT NULL:**  
#set rule when creating table:  
```sql
CREATE TABLE table_name (
  column_name DATA TYPE NOT NULL,
);
```
#add rule to existing table column (if column doesn't contain values = null):  
```sql
ALTER TABLE table_name
ALTER COLUMNT column_name
SET NOT NULL;
```
# **- DEFAULT:**  
#set rule when creating table:  
```sql
CREATE TABLE table_name (
  column_name DATA TYPE DEFAULT value,
);
```
#add rule to existing table column (if value = null than value: default value):  
```sql
ALTER TABLE table_name
ALTER COLUMNT column_name
SET DEFAULT value;
```
# **- UNIQUE:**  
#set rule when creating table:  
```sql
CREATE TABLE table_name (
  column_name DATA TYPE UNIQUE,
);
```
#add rule to existing table column:  
```sql
ALTER TABLE table_name
ADD UNIQUE(column_name);
```
# **- CHECK:**  
#set rule when creating table:  
```sql
CREATE TABLE table_name (
  column_name DATA TYPE CHECK(column_name >,<,!=,=... value),
);
```
#OR, IS, AND:
```sql
CREATE TABLE table_name (
  column_name DATA TYPE CHECK(column_name IS NULL OR (column_name <= 100 AND column_name >= 50)),
);
```
#set rule when creating table (comparing with value from other column):
```sql
CREATE TABLE table_name (
  column_name1 DATA TYPE,
  column_name2 DATA TYPE CHECK(column_name1 >,<,!=,=... column_name2),
);
```
#add rule to existing table column:  
```sql
ALTER TABLE table_name
ADD CHECK (column_name >,<,!=,=... value)
```

---
# **2) Drop default validation rules:**  
---

#drop rules by its name in PgAdmin:  
```sql
ALTER TABLE table_name
DROP CONSTRAINS validation_rule;
```