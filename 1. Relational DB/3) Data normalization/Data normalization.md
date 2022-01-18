# Data Normalization

**Link:** https://t4tutorials.com/fourth-normal-form/

## 1st Normal Form (1NF)
```text
1. Doesn't contain duplicate rows;
2. Every cell contains only one value;
```
**1st Normal Form (1NF)** — Removes repeating fields by creating a new table where the original
and new table are linked together with a master-detail, one-to-many relationship.

### Prevent from:
![link](https://drive.google.com/uc?id=11eUeK5vz_I-gA9mGKexpR0Kch5Zw-z0n)

### Normalized:
![link](https://drive.google.com/uc?id=1o26VqmS6ztkLsNJoZ3LdORvznAGkgpyL)

## 2nd Normal Form (2NF)
```text
1. It fits first 1st Normal Form (1NF);
2. Every non-prime attribute dependent on the whole table of every candidate key; 
```
**2nd Normal Form (2NF)** — Performs a seemingly similar function to that of 1NF, but creates a
table where repeating values (rather than repeating fields as for 1NF) are removed to a new
table. The result is a many-to-one relationship rather than a one-to-many relationship, created
between the original and the new tables. The new table gets a primary key consisting of a single
field. The master table contains a foreign key pointing back to the primary key of the new table.
That foreign key is not part of the primary key in the original table.

### Prime or Key Attributes (unique / form unique relation):
Attributes of the relation which exist in at least one of the possible candidate keys, 
are called prime or key attributes.

### Non Prime or Non Key Attributes (repeating):
Attributes of the relation which does not exist in any of the possible candidate keys of
the relation, such attributes are called non prime or non-key attributes.

### Prevent from:
![link](https://drive.google.com/uc?id=1Hw4Qvgv66DuRFohG3evL9Vx-KJ925ouk)

### Normalized:
![link](https://drive.google.com/uc?id=1NaSkthN0f3FUPnFDf_1h-YK3Zcs6rZoH)

## 3rd Normal Form (3NF)
```text
1. It fits second 2st Normal Form (2NF);
2. Every non-prime attribute is non-transitively dependent on every candidate key;
```
3rd Normal Form (3NF) — It is difficult to explain 3NF without using a mind bogglingly confusing
technical definition. Elimination of a transitive dependency implies creation of a new table for
something indirectly dependent on the primary key in an existing table. There are a multitude of
ways in which 3NF can be interpreted.

Beyond 3NF — Many modern relational database models do not extend beyond 3NF. Sometimes
3NF is not used at all. The reason why is because of the generation of too many tables and the
resulting complex SQL code joins, with resulting terrible database response times. One common
case that bears mentioning is removal of potentially NULL valued fields into new tables, creating
a one-to-one relationship. In modern high-end relational database engines with variable record
lengths, this is largely irrelevant. Disk space is cheap and, as already stated, increased numbers
of tables leads to bigger SQL joins and poorer performance.

### Prevent from:
![link](https://drive.google.com/uc?id=1ef12LA79thFzn8nR4ZkbydZ-Yx8xKsaI)

### Normalized:
![link](https://drive.google.com/uc?id=1jj6yl_MPAdYVlwaYea0E9dWI10dfqmO9)

## Boyce-Codd Normal Form (BCNF);
```text
1. A table must be in 3NF.
2. A table can have only one candidate key.
```

A candidate key has potential for being a table’s primary key. A table is not allowed more than one
primary key because referential integrity requires it as such. It would be impossible to check foreign keys
against more than one primary key. Referential integrity would be automatically invalid, unenforceable,
and, thus, there would be no relational database model.

### Normalized:
![link](https://drive.google.com/uc?id=17GaMjUOqw2l64XZZFVdPMgGN9U2sC0lU)

## 4th Normal Form;
```text
1. A table must be in 3NF or BCNF with 3NF.
2. Multi-valued dependencies must be transformed into functional dependencies. This implies
that one value and not multiple values are dependent on a primary key.
3. Eliminate multiple sets of multiple valued or multi-valued dependencies, sometimes described
as non-trivial multi-valued dependencies.
```

A multiple valued set is a field containing a comma-delimited list or collections of some kind. A collection
could be an array of values of the same type. Those multiple values are dependent as a whole on the
primary key (the “whole” meaning the entire collection in each record).

### Prevent from:
![link](https://drive.google.com/uc?id=1UuD8LYJadCRKsSzCPASKjUN4TSj0nKpu)

### Normalized:
![link](https://drive.google.com/uc?id=1tKHxdKRQVjxIBrcSNb4usmI4FojMDl67)

## 5th Normal Form;
```text
1. A table must be in 4NF.
2. Cyclic dependencies must be eliminated. A cyclic dependency is simply something that depends
on one thing, where that one thing is either directly in indirectly dependent on itself.
```

A cyclic dependency is a form of circular
dependency where three pairs result as a combination of a single three-field composite primary key
table, those three pairs being field 1 with field 2, field 2 with field 3, and field 1 with field 3. The cyclic
dependency is that everything is related to everything else, including itself. In other words, there is a
combination or a permutation excluding repetitions. If tables are joined again using a three-table join, the
resulting records will be the same as that present in the original table. It is a stated requirement of the valid-
ity of 5NF that the post-transformation join must match records for a query on the pre-transformation table.

### Normalized:
![link](https://t4tutorials.com/wp-content/uploads/2020/04/fifth-normal-form-in-database-systems.webp)

## Domain Key Normal Form (DKNF);
```text
1. There can be no insertion, change, or data removal anomalies. In other words, every record in
the database must be directly accessible in all manners, such that no errors can result.

2. Every record in every table must be uniquely identifiable and directly related to the primary key
in its table. This means that every field in every table is directly determined by the primary key
in its table.

3. All validation of data is done within the database model. As far as application and database
performance are concerned this is nearly always an extremely undesirable state in a commercial
environment. It is better to split functionality between database and applications. Some may call
this business rules. It is generally common knowledge that some business rule implementation
is often most effectively divided up between database and applications.
```