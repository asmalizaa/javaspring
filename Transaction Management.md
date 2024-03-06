# Transaction Management

- @Transactional annotation is the metadata used for managing transactions in the Spring Boot application. To configure Spring Transaction, this annotation can be applied at the class level or method level.
- In an enterprise application, a transaction is a sequence of actions performed by the application that together pipelined to perform a single operation.
- For example, booking a flight ticket is also a transaction where the end user has to enter his information and then make a payment to book the ticket.

## Why Do We Need Transaction Management?

- Let’s understand transactions with the above example, if a user has entered his information the user’s information gets stored in the user_info table.
- Now, to book a ticket he makes an online payment and due to some reason(system failure) the payment has been canceled so, the ticket is not booked for him.
- But, the problem is that his information gets stored on the user_info table. On a large scale, more than thousands of these things happen within a single day.
- So, it is not good practice to store a single action of the transaction(Here, only user info is stored not the payment info).

To overcome these problems, spring provides transaction management, which uses annotation to handle these issues. In such a scenario, spring stores the user information in temporary memory and then checks for payment information if the payment is successful then it will complete the transaction otherwise it will roll back the transaction and the user information will not get stored in the database.
