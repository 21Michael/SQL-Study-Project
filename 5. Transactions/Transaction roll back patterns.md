# Transaction roll back patterns

## 1) Commit/rollback:
A great feature of traditional ACID transactions is that the business logic can easily
roll back a transaction if it detects the violation of a business rule. It executes a ROLL-
BACK statement, and the database undoes all the changes made so far.

### <ins>Usage:</ins>
  - **Local DB (Monolithic arch);**
    ![link](https://i.ytimg.com/vi/-NQAMrgUiUE/maxresdefault.jpg)
  - **Shared DB / Shared DB per service (Distributed arch);**
    ![link](https://drive.google.com/uc?id=1nur6dQF5hwX163kg9WFnrLoRJKEl7yuD)
    
## 2) Compensatable transactions (sequential):
Sagas can’t be automatically rolled back, because each step commits its changes to the
local database.
Suppose that the (n + 1) th transaction of a saga fails. The effects of the previous n
transactions must be undone. The saga executes the compensation transactions in reverse order.

### <ins>Usage:</ins>
  - **Own DB per service (Distributed arch);**
    
    ![link](https://drive.google.com/uc?id=1o8onJ_aUJDyb4sXNzMlmJHsPZNbg4KTu)
   
    **Consider, for example, the Create Order Saga . This saga can fail for a variety of
    reasons:**
      - The consumer information is invalid or the consumer isn’t allowed to create
        orders.
      - The restaurant information is invalid or the restaurant is unable to accept orders.
      - The authorization of the consumer’s credit card fails.

    In the Create Order Saga , the createOrder() , verifyConsumerDetails() , and create-
    Ticket() steps are compensatable transactions. **The createOrder()** and **createTicket()** 
    transactions have compensating transactions that undo their updates. The
    **verifyConsumerDetails()** transaction is read-only, so doesn’t need a compensating
    transaction.
    
    ![link](https://drive.google.com/uc?id=1ceYW0ysyhrD6E2Gh6ttLPOmgrDj4i_13)

## 3) Pivot transactions:
The go/no-go point in a saga. If the pivot transaction commits, the saga will run until 
completion. A pivot transaction can be a transaction that’s neither compensatable nor 
retriable. Alternatively, it can be the last compensatable transaction or the first retriable
transaction.

![link](https://drive.google.com/uc?id=1ceYW0ysyhrD6E2Gh6ttLPOmgrDj4i_13)

The **authorizeCreditCard()** transaction is this saga’s pivot transaction. If
the consumer’s credit card can be authorized, this saga is guaranteed to complete.

## 4) Retriable transactions:
Transactions that follow the pivot transaction and are guaranteed to succeed.

![link](https://drive.google.com/uc?id=1ceYW0ysyhrD6E2Gh6ttLPOmgrDj4i_13)

The **approveTicket()** and **approveOrder()** steps are retriable transactions that follow the
pivot transaction.