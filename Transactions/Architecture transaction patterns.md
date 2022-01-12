# Architecture transaction patterns

**Links:** 
  - https://medium.com/trendyol-tech/saga-pattern-briefly-5b6cf22dfabc
  - https://developers.redhat.com/articles/2021/09/21/distributed-transaction-patterns-microservices-compared#parallel_pipelines
  - https://microservices.io/patterns/data/saga.html

## <ins>Monolithic arch:</ins>

  - ### Local transactions / ACID;
    ![link](https://developers.redhat.com/blog/wp-content/uploads/2018/09/Untitled-UML-4.png) 
    
    In the customer order example above, if a user sends a Put Order action to a monolithic system,
    the system will create a  local database transaction that works over multiple database tables.
    If any step fails, the transaction can roll back. This is known as **ACID (Atomicity, Consistency,
    Isolation, Durability),** which is guaranteed by the database system.

## <ins>Distributed arch (microservices):</ins>
When a microservice architecture decomposes a monolithic system into self-encapsulated services,
it can break transactions. This means a local transaction in the monolithic system is now
distributed into multiple services that will be called in a sequence.

![link](https://developers.redhat.com/blog/wp-content/uploads/2018/09/Untitled-UML-5.png)

When a Put Order request comes from the user, both microservices will be called to apply changes
into their own database. Because the transaction is now across multiple databases, it is now
considered a **distributed transaction.**

## The problem (no ACID):

- **How do we keep the transaction atomic?**  
  In a database system, atomicity means that in a transaction either all steps complete or no
  steps complete. The microservice-based system does not have a global transaction coordinator
  by default. In the example above, if the CreateOrder method fails, how do we roll back the
  changes we applied by the CustomerMicroservice?

- **Do we isolate user actions for concurrent requests?**  
  If an object is written by a transaction and at the same time (before the transaction ends),
  it is read by another request, should the object return old data or updated data? In the
  example above, once UpdateCustomerFund succeeds but is still waiting for a response from
  CreateOrder, should requests for the current customer's fund return the updated amount or
  not?
  
## The solution:
  - ### Two-phase commit (2PC) / ACID;
    **As its name hints, 2pc has two phases:**
      - **Prepare phase:**  
        In the prepare phase, all microservices will be asked to prepare for some data change that
        could be done atomically.
      - **Commit phase:**  
        Once all microservices are prepared, the commit phase will ask all the microservices to make the actual changes.
    
    Normally, there needs to be a global coordinator to maintain the lifecycle of the transaction,
    and the coordinator will need to call the microservices in the prepare and commit phases.
    
    ![link](https://developers.redhat.com/blog/wp-content/uploads/2018/09/Untitled-UML-6.png)
    
    If at any point a single microservice fails to prepare, the Coordinator will abort the
    transaction and begin the **rollback process.**
    
    ![link](https://developers.redhat.com/blog/wp-content/uploads/2018/09/Untitled-UML-7.png)
    
    **Pros:**
    -  First, the prepare and commit phases guarantee that the transaction is **atomic.** The
       transaction will end with either all microservices returning successfully or all
       microservices have nothing changed.
    - Secondly, 2pc allows **read-write isolation.** This means the changes on a field are not
      visible until the coordinator commits the changes.
    
    **Cons:**
    - **Synchronous (blocking):**  
      While 2pc has solved the problem, it is not really recommended for many microservice-based
      systems because 2pc is synchronous (blocking). The protocol will need to lock the object
      that will be changed before the transaction completes.   
      This is not good. In a database system, transactions tend to be fast—normally within 50 ms.
      However, microservices have long delays with RPC calls, especially when integrating with
      external services such as a payment service. The lock could become a system performance
      bottleneck. Also, it is possible to have two transactions mutually lock each other (deadlock)
      when each transaction requests a lock on a resource the other requires.
      
  - ### Saga:
    The Saga pattern is another widely used pattern for distributed transactions. It is different
    from 2pc, which is synchronous. The Saga pattern is asynchronous and reactive. In a Saga pattern,
    the distributed transaction is fulfilled by asynchronous local transactions on all related
    microservices. The microservices communicate with each other through an event bus.
    
    - ### Orchestration / ACD;
      When using orchestration, you define an orchestrator class whose sole responsibility is to tell the saga participants
      what to do. The saga orchestrator communicates with the participants using command/
      async reply-style interaction. To execute a saga step, it sends a command message to a
      participant telling it what operation to perform. After the saga participant has per-
      formed the operation, it sends a reply message to the orchestrator. The orchestrator
      then processes the message and determines which saga step to perform next.

      **The happy path through this saga is as follows:**
        1) The saga orchestrator sends a Verify Consumer command to Consumer Service.
        2) Consumer Service replies with a Consumer Verified message.
        3) The saga orchestrator sends a Create Ticket command to Kitchen Service.
        4) Kitchen Service replies with a Ticket Created message.
        5) The saga orchestrator sends an Authorize Card message to Accounting Service.
        6) Accounting Service replies with a Card Authorized message.
        7) The saga orchestrator sends an Approve Ticket command to Kitchen Service.
        8) The saga orchestrator sends an Approve Order command to Order Service.
      
      ![link](https://drive.google.com/uc?id=1cvWNPeK-Vy2IHqZ7K776Z8YsK1_nXLwm)
      
      **Pros:**
        - **Simpler dependencies** — One benefit of orchestration is that it doesn’t introduce
          cyclic dependencies. The saga orchestrator invokes the saga participants, but
          the participants don’t invoke the orchestrator. As a result, the orchestrator
          depends on the participants but not vice versa, and so there are no cyclic
          dependencies.
        - **Less coupling** — Each service implements an API that is invoked by the orches-
          trator, so it does not need to know about the events published by the saga
          participants.
        - **Improves separation of concerns and simplifies the business logic** — The saga coordina-
          tion logic is localized in the saga orchestrator. The domain objects are simpler
          and have no knowledge of the sagas that they participate in. For example, when
          using orchestration, the Order class has no knowledge of any of the sagas, so it
          has a simpler state machine model. During the execution of the Create Order
          Saga , it transitions directly from the APPROVAL_PENDING state to the APPROVED
          state. The Order class doesn’t have any intermediate states corresponding to the
          steps of the saga. As a result, the business is much simpler.

      **Cons:**
        - **The risk of centralizing too much business logic** in the orchestrator. This 
          results in a design where the smart orchestrator tells the dumb services what 
          operations to do. Fortunately, you can avoid this problem by designing 
          orchestrators that are solely responsible for sequencing and don’t contain any
          other business logic.
          
    - ### Choreography / ACD;
      When using choreography, there’s no central coordinator telling the saga participants 
      what to do. Instead, the saga participants subscribe to each other’s events and respond
      accordingly.

      **The happy path through this saga is as follows:**  
        1) Order Service creates an Order in the APPROVAL_PENDING state and publishes
        an OrderCreated event.
        2) Consumer Service consumes the OrderCreated event, verifies that the con-
        sumer can place the order, and publishes a ConsumerVerified event.
        3) Kitchen Service consumes the OrderCreated event, validates the Order , cre-
        ates a Ticket in a CREATE_PENDING state, and publishes the TicketCreated event.
        4) Accounting Service consumes the OrderCreated event and creates a Credit-
        CardAuthorization in a PENDING state.
        5) Accounting Service consumes the TicketCreated and ConsumerVerified
        events, charges the consumer’s credit card, and publishes the CreditCard-
        Authorized event.
        6) Kitchen Service consumes the CreditCardAuthorized event and changes the
        state of the Ticket to AWAITING_ACCEPTANCE .
        7) Order Service receives the CreditCardAuthorized events, changes the state of
        the Order to APPROVED , and publishes an OrderApproved event.

      ![link](https://drive.google.com/uc?id=1NjHT6RCRedwtSdR8BHOty_HyP07VDsje)

      **The authorization of the consumer’s credit card might fail. The saga must execute the 
      compensating transactions to undo what’s already been done:**
        1) Order Service creates an Order in the APPROVAL_PENDING state and publishes
        an OrderCreated event.
        2) Consumer Service consumes the OrderCreated event, verifies that the con-
        sumer can place the order, and publishes a ConsumerVerified event.
        3) Kitchen Service consumes the OrderCreated event, validates the Order , creates
        a Ticket in a CREATE_PENDING state, and publishes the TicketCreated event.
        4) Accounting Service consumes the OrderCreated event and creates a Credit-
        CardAuthorization in a PENDING state.
        5) Accounting Service consumes the TicketCreated and ConsumerVerified
        events, charges the consumer’s credit card, and publishes a Credit Card
        Authorization Failed event.
        6) Kitchen Service consumes the Credit Card Authorization Failed event and
        changes the state of the Ticket to REJECTED.
        7) Order Service consumes the Credit Card Authorization Failed event and
        changes the state of the Order to REJECTED.
           
      ![link](https://drive.google.com/uc?id=1gYTphn0VnfX8dGiPuQMRlSvsqhICOsSR)
  
      **Pros:**  
        - **Simplicity** — Services publish events when they create, update, or delete business
          objects.
        - **Loose coupling** — The participants subscribe to events and don’t have direct knowl-
          edge of each other.
          
      **Cons:**
        - **More difficult to understand** — Unlike with orchestration, there isn’t a single place
          in the code that defines the saga. Instead, choreography distributes the imple-
          mentation of the saga among the services. Consequently, it’s sometimes difficult
          for a developer to understand how a given saga works.
        - **Cyclic dependencies between the services** — The saga participants subscribe to each
          other’s events, which often creates cyclic dependencies. For example, if you
          carefully examine figure 4.4, you’ll see that there are cyclic dependencies, such
          as Order Service  Accounting Service  Order Service . Although this isn’t
          necessarily a problem, cyclic dependencies are considered a design smell.
        - **Risk of tight coupling** — Each saga participant needs to subscribe to all events that
          affect them. For example, Accounting Service must subscribe to all events that
          cause the consumer’s credit card to be charged or refunded. As a result, there’s
          a risk that it would need to be updated in lockstep with the order lifecycle
          implemented by Order Service.
      
  - ### Parallel pipeline / ACD;