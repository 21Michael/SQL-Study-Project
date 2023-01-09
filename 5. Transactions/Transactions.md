# Transactions

**Transaction solves the problem of inconsistency and persistent of the data:**  
```text
<transaction>
  1) Put -50$ to users (User Table);
  2) Update users bank account -50$ (Bank Table);
</transaction>
```

## Microservices shared DB per service (without transaction pattern):
![link](https://drive.google.com/uc?id=1yuSmjUFZb3GzafBfO45MmywPt2637Blx)

## The Problem: how to make in persistent and consistent?:
![link](https://drive.google.com/uc?id=1hy1ZBc997YpEjbyU-CNzmNSv7kkZIkls)

**Транзакция** - задает последовательность инструкций языка Transact-SQL, применяемую программистами базы данных для объединения в один пакет операций чтения и записи для того, чтобы система базы данных могла обеспечить согласованность данных. 

**Существует два типа транзакций**:
 - **Неявная транзакция** - задает любую отдельную инструкцию INSERT, UPDATE или DELETE как единицу транзакции.
 - **Явная транзакция** - обычно это группа инструкций языка Transact-SQL, начало и конец которой обозначаются такими инструкциями, как BEGIN TRANSACTION, COMMIT и ROLLBACK.

## 1) ACID

**Основные концепции транзакции описываются аббревиатурой ACID – Atomicity, Consistency, Isolation, Durability (Атомарность, Согласованность, Изолированность, Долговечность):**
 - **Атомарность** гарантирует, что любая транзакция будет зафиксирована только целиком 
   (полностью). Если одна из операций в последовательности не будет выполнена, то вся 
   транзакция будет отменена. Тут вводится понятие “отката” (rollback). Т.е. внутри 
   последовательности будут происходить определённые изменения, но по итогу все они будут
   отменены (“откачены”) и по итогу пользователь не увидит никаких изменений.  

    ![link](https://drive.google.com/uc?id=1B_ZAt8eQwu3jcZF5h_tVDUB7AQbJRrrj)

 - **Согласованность** означает, что любая завершённая транзакция (транзакция, которая 
   достигла завершения транзакции – end of transaction) фиксирует только допустимые 
   результаты. Например, при переводе денег с одного счёта на другой, в случае, если 
   деньги ушли с одного счёта, они должны прийти на другой (это и есть согласованность
   системы). Списание и зачисление – это две разные транзакции, поэтому первая транзакция
   пройдёт без ошибок, а второй просто не будет. Именно поэтому крайне важно учитывать 
   это свойство и поддерживать баланс системы.
   
   ![link](https://drive.google.com/uc?id=1dZDkfOlTZ7UpP5dJ4-tLOWrEzHdhd7rB)
   
 - **Изолированность** - каждая транзакция должна быть изолирована от других, т.е. её 
   результат не должен зависеть от выполнения других параллельных транзакций. На практике,
   изолированность крайне труднодостижимая вещь, поэтому здесь вводится понятие “уровни 
   изолированности” (транзакция изолируется не полностью).

   ![link](https://drive.google.com/uc?id=1bW6_Gnz7656XcGkR7hmIClGkLrPSlBzJ)

 - **Долговечность** - концепция гарантирует, что если мы получили подтверждение о
   выполнении транзакции, то изменения, вызванные этой транзакцией не должны быть 
   отменены из-за сбоя системы (например, отключение электропитания).

   ![link](https://drive.google.com/uc?id=1Rm4cozia4noWfYZR-cNiqRmFRPrtdJCm)
  
## 2) Saga ACD

**Link:** https://microservices.io/microservices/sagas/2019/07/09/microcph-sagas.html

The challenge with using sagas is that they lack the isolation property of ACID
transactions. That’s because the updates made by each of a saga’s local transactions
are immediately visible to other sagas once that transaction commits. This behavior
can cause two problems. First, other sagas can change the data accessed by the saga
while it’s executing. And other sagas can read its data before the saga has completed
its updates, and consequently can be exposed to inconsistent data. 

**You can, in fact, consider a saga to be ACD:**
- **Atomicity** — The saga implementation ensures that all transactions are executed
    or all changes are undone.
- **Consistency** — Referential integrity within a service is handled by local databases.
    Referential integrity across services is handled by the services.
- **Durability** — Handled by local databases.

### The lack of isolation can cause the following three anomalies:

  - **Lost updates** — One saga overwrites without reading changes made by another saga.
    A lost update anomaly occurs when one saga overwrites an update made by another
    saga.    
    ![link](https://i.stack.imgur.com/xqoBg.png)
    __  
    <ins>**Consider, for example, the following scenario:**</ins>  
    **1. The first step of the Create Order Saga creates an Order.**  
    **2. While that saga is executing, the Cancel Order Saga cancels the Order.**  
    **3. The final step of the Create Order Saga approves the Order.**  
    __  
    In this scenario, the Create Order Saga ignores the update made by the Cancel Order
    Saga and overwrites it. As a result, the FTGO application will ship an order that the
    customer had cancelled.
    
  - **Dirty reads** — A transaction or a saga reads the updates made by a saga that has
    not yet completed those updates.
    Let’s imagine a scenario that interleaves the execution of the Cancel Order and Create
    Order Saga s, and the Cancel Order Saga is rolled back because it’s too late to cancel
    the delivery. It’s possible that the sequence of transactions that invoke the Consumer   
    ![link](https://vladmihalcea.com/wp-content/uploads/2018/05/DirtyRead.png)
    __  
    **<ins>Service is as follows:</ins>**            
    **1. Cancel Order Saga — Increase the available credit.**  
    **2. Create Order Saga — Reduce the available credit.**  
    **3. Cancel Order Saga — A compensating transaction that reduces the available credit.**  
    __    
    In this scenario, the Create Order Saga does a dirty read of the available credit that
    enables the consumer to place an order that exceeds their credit limit. It’s likely that
    this is an unacceptable risk to the business.
    
  - **Fuzzy/nonrepeatable reads** — Two different steps of a saga read the same data and
    get different results because another saga has made updates.  
    ![link](https://i.stack.imgur.com/iPI0C.png)
    
  - **Phantom Read** - A transaction re-executes a query returning a set of rows that satisfy
    a search condition and finds that the set of rows satisfying the condition has changed 
    due to another recently-committed transaction. This is similar to a non-repeatable read
    except it involves a changing collection matching a predicate rather than a single item.
    ![link](https://i.stack.imgur.com/aCtew.png)
    
### Countermeasures for handling the lack of isolation:
  - **Semantic lock** — An application-level lock.  
    When using the semantic lock countermeasure, a saga’s compensatable transaction
    sets a **flag** in any record that it creates or updates. The flag indicates that the record
    isn’t committed and could potentially change. The flag can either be a lock that prevents
    other transactions from accessing the record or a warning that indicates that other
    transactions should treat that record with suspicion. It’s cleared by either a retriable
    transaction—saga is completing successfully—or by a compensating transaction: the
    saga is rolling back.   
    **<ins>Preventing Lost updates:</ins>**    
    ```text
    The PENDING state prevents this problem. The cancelOrder() command will only cancel an
    Order if its state is APPROVED. If the state is PENDING, cancelOrder() returns an error
    to the client indicating that it should try again later. The semantic lock counter-measure
    is a kind of application-level locking. As I describe in the presentation, it’s a way to
    make sagas, which are inherently ACD, ACID again.  
    ``` 
  - **Commutative updates** — Design update operations to be executable in any order.  
    One straightforward countermeasure is to design the update operations to be com-
    mutative. Operations are commutative if they can be executed in any order. An
    Account ’s debit() and credit() operations are commutative (if you ignore overdraft
    checks). This countermeasure is useful because it eliminates lost updates.  
  - **Pessimistic view** — Reorder the steps of a saga to minimize business risk.  
    Another way to deal with the lack of isolation is the pessimistic view countermeasure. It
    reorders the steps of a saga to minimize business risk due to a dirty read.  
    **<ins>Preventing Dirty read:</ins>**  
    ```text
    In that scenario, the Create Order Saga performed a dirty read of the available credit 
    and created an order that exceeded the consumer credit limit. To reduce the risk of that
    happening, this countermeasure would reorder the Cancel Order Saga :
    1) Order Service — Change the state of the Order to cancelled.
    2) Delivery Service — Cancel the delivery.
    3) Customer Service — Increase the available credit.
    In this reordered version of the saga, the available credit is increased in a retriable
    transaction, which eliminates the possibility of a dirty read.
    ```
  - **Reread value** — Prevent dirty writes by rereading data to verify that it’s unchanged
    before overwriting it.  
    The reread value countermeasure prevents lost updates. A saga that uses this counter-
    measure rereads a record before updating it, verifies that it’s unchanged, and then
    updates the record. If the record has changed, the saga aborts and possibly restarts.  
    **<ins>Preventing Lost updates:</ins>**  
    ```text 
    The Create Order Saga could use this countermeasure to handle the scenario
    where the Order is cancelled while it’s in the process of being approved. The transac-
    tion that approves the Order verifies that the Order is unchanged since it was created
    earlier in the saga. If it’s unchanged, the transaction approves the Order . But if the
    Order has been cancelled, the transaction aborts the saga, which causes its compensat-
    ing transactions to be executed.  
    ```
  - **Version file** — Record the updates to a record so that they can be reordered.
    The version file countermeasure is so named because it records the operations that are
    performed on a record so that it can reorder them. It’s a way to turn noncommutative
    operations into commutative operations.    
    **<ins>Preventing Lost updates:</ins>**  
    ```text 
     To see how this countermeasure works, consider a scenario where the Create Order Saga 
     executes concurrently with a Cancel Order Saga . Unless the sagas use the semantic lock
     countermeasure, it’s possible that the Cancel Order Saga cancels the authorization of
     the consumer’s credit card before the Create Order Saga authorizes the card.      
     One way for the Accounting Service to handle these out-of-order requests is for it
     to record the operations as they arrive and then execute them in the correct order. In
     this scenario, it would first record the Cancel Authorization request. Then, when the
     Accounting Service receives the subsequent Authorize Card request, it would notice
     that it had already received the Cancel Authorization request and skip authorizing
     the credit card.  
    ```
  - **By value** — Use each request’s business risk to dynamically select the concurrency 
    mechanism.  
    The final countermeasure is the by value countermeasure. It’s a strategy for selecting
    concurrency mechanisms based on business risk. An application that uses this
    countermeasure uses the properties of each request to decide between using sagas
    and distributed transactions. It executes low-risk requests using sagas, perhaps apply-
    ing the countermeasures described in the preceding section. But it executes high-risk
    requests involving, for example, large amounts of money, using distributed transactions.
    
### Transaction Isolation levels
The SQL standard defines four levels of transaction isolation. The most strict is Serializable
, which is defined by the standard in a paragraph which says that any concurrent execution of
a set of Serializable transactions is guaranteed to produce the same effect as running them
one at a time in some order. The other three levels are defined in terms of phenomena, 
resulting from interaction between concurrent transactions, which must not occur at each level
. The standard notes that due to the definition of Serializable, none of these phenomena are
possible at that level. (This is hardly surprising -- if the effect of the transactions must
be consistent with having been run one at a time, how could you see any phenomena caused by
interactions?).

**PostgreSQL example:**  
In PostgreSQL, you can request any of the four standard transaction isolation levels, but
internally only three distinct isolation levels are implemented, i.e., PostgreSQL's Read 
Uncommitted mode behaves like Read Committed. This is because it is the only sensible way
to map the standard isolation levels to PostgreSQL's multiversion concurrency control 
architecture.

The table also shows that PostgreSQL's Repeatable Read implementation does not allow phantom
reads. Stricter behavior is permitted by the SQL standard: the four isolation levels only
define which phenomena must not happen, not which phenomena must happen. The behavior of 
the available isolation levels is detailed in the following subsections.

|Isolation Level|	Dirty Read|	Nonrepeatable Read|	Phantom Read|	Serialization Anomaly|
|---------------|-----------|-------------------|-------------|----------------------|
|**1. Read uncommitted**|	Allowed, but not in PG|	Possible|	Possible|	Possible|
|**2. Read committed**|	Not possible|	Possible|	Possible|	Possible|
|**3. Repeatable read**|	Not possible	|Not possible	|Allowed, but not in PG|	Possible|
|**4. Serializable**|Not possible	|Not possible	|Not possible	|Not possible|

**Link:** https://www.postgresql.org/docs/9.5/transaction-iso.html

## 3) SQL transaction commands

**SQL main transaction commands**:
 - **BEGIN** (начинает блок транзакций);
 - **COMMIT** (сохраняет изменения);
 - **ROLLBACK** (откатывает (отменяет) изменения);
 - **SAVEPOINT** (создаёт точку к которой группа транзакций может откатиться);

### Example:

**Connection1:**
```sql
BEGIN;
UPDATE users SET bank_account = bank_account - 50.00
WHERE name = 'User 1';
-- etc etc
COMMIT;
SAVEPOINT my_savepoint;
```

**Connection3:** 
```sql
BEGIN;
UPDATE users SET bank_account = bank_account + 250.00
WHERE name = 'User 1';
-- etc etc
-- oops ... ERROR!!!!!!!!!!!
ROLLBACK TO my_savepoint;
```
### Shared DB per service (CLASSIC ACID transaction pattern):
![link](https://drive.google.com/uc?id=1Tm9KDexBT4cegeNG8rGMqhR10pm_3uyE)


