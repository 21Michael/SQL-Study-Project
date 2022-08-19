# DB-Study-Project

## 1. Relational DB:

### 1) SQL:
1) **Data Types:** ✅
    - Text types;
    - Number types;
    - Date types;
2) **Basic Syntax:** ✅
    - CREATE;
    - INSERT;
    - SELECT;
    - WHERE;
    - UPDATE;
    - DELETE;
    - ORDER BY;
    - LIMIT;
    - OFFSET;  
    - **Unit two queries:** ✅
      - UNION ALL;
      - UNION;
      - INTERSECT;
      - INTERSECT ALL;
      - EXCEPT;
      - EXCEPT ALL;

3) **Sub-queries:** ✅
    - in SELECT statement;
    - in FROM statement;
    - in JOIN statement;
    - in WHERE + operator (>,=,!=...) statement;
    - in WHERE + special word (IN, (>,=,!=...) + ALL/SOME/ANY) statement;
    - loop by WHERE + special operator (>,=,!=...) statement;
4) **Operators and functions:** ✅
    - STRING;
    - COMPARISON OPERATORS;
    - AGGREGATE FUNCTIONS;
5) **Relations between tables:** ✅
    - Concepts: ONE TO MANY / MANY TO ONE;
    - Create tables with relation (PRIMARY KEY, REFERENCES);
    - Select data from joined tables (JOIN ON);
    - Delete joined data (ON DELETE);
6) **Grouping:** ✅
    - Select data from grouped tables (GROUP BY);
    - Select grouped data by aggregate functions (GROUP BY + aggregation functions);
7) **Optimizations:** ✅
    - CTE;
    - Views;
    - Materialized view'
8) **Recursive CTE** ✅


### 2) PostgreSQL: 
  - **Migrations;** ✅
  - **Optimizations;** ✅
  - **Validation;** ✅

### 3) Data normalization
  1. **1st Normal Form;** ✅
  2. **2nd Normal Form;** ✅
  3. **3rd Normal Form;** ✅
  4. **Boyce-Codd Normal Form (BCNF);** ✅
  5. **4th Normal Form;** ✅
  6. **5th Normal Form;** ✅
  7. **Domain Key Normal Form (DKNF);** ✅

## 2. Non-Relational DB:

## 3. Data access patterns:
  - **Active Record;** ✅
  - **Data Mapper;**  ✅
  - **DAO;** ✅
  - **Repository;** ✅

## 4. DB patterns:
  -  **Identity Map;**
  -  **Unit of Work;**
  -  **Lazy Load;**

## 5. Transactions: 
  - **ACID;** ✅
  - **Saga ACD:**
    - Lack of Isolation anomalies; ✅
    - Isolation levels;
    - Countermeasures for handling the lack of Isolation; ✅
  - **SQL main transaction commands;** ✅
  - **Architecture transaction patterns:** 
    - **Monolithic arch:**
      - Local transactions / ACID; ✅
    - **Distributed arch (microservices):**
      - Two-phase commit (2PC) / ACID; ✅
      - Saga:
        - Orchestration / ACD; ✅
        - Choreography / ACD; ✅
  - **Transaction roll back patterns:**
    - **Commit/rollback;** ✅
    - **Compensatable transactions (sequential);**  ✅
    - **Pivot transactions;**  ✅
    - **Retriable transactions;**  ✅

## 6. CRUD (классификация функций по манипуляции данными)
