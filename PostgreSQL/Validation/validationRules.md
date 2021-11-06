# 1) Default validation rules:

---

### **- NOT NULL:**  
**Set rule when creating table:**  
```sql
CREATE TABLE table_name (
  column_name DATA TYPE NOT NULL,
);
```
**Add rule to existing table column (if column doesn't contain values = null):**  
```sql
ALTER TABLE table_name
ALTER COLUMNT column_name
SET NOT NULL;
```
### **- DEFAULT:**  
**Set rule when creating table:**  
```sql
CREATE TABLE table_name (
  column_name DATA TYPE DEFAULT value,
);
```
**Add rule to existing table column (if value = null than value: default value):**  
```sql
ALTER TABLE table_name
ALTER COLUMNT column_name
SET DEFAULT value;
```
### **- UNIQUE:**  
**Set rule when creating table:**  
```sql
CREATE TABLE table_name (
  column_name DATA TYPE UNIQUE,
);
```
**Add rule to existing table column:**  
```sql
ALTER TABLE table_name
ADD UNIQUE(column_name);
```
### **- CHECK:**  
**Set rule when creating table:**  
```sql
CREATE TABLE table_name (
  column_name DATA TYPE CHECK(column_name >,<,!=,=... value),
);
```
### OR, IS, AND:
```sql
CREATE TABLE table_name (
  column_name DATA TYPE CHECK(column_name IS NULL OR (column_name <= 100 AND column_name >= 50)),
);
```
##**Set rule when creating table (comparing with value from other column):**
```sql
CREATE TABLE table_name (
  column_name1 DATA TYPE,
  column_name2 DATA TYPE CHECK(column_name1 >,<,!=,=... column_name2),
);
```
##**Add rule to existing table column:**  
```sql
ALTER TABLE table_name
ADD CHECK (column_name >,<,!=,=... value)
```


# **2) Drop default validation rules:**  

---

**Drop rules by its name in PgAdmin:**  
```sql
ALTER TABLE table_name
DROP CONSTRAINS validation_rule;
```