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

## @Transactional Annotation

- In Spring Boot, @Transactional annotation is used to manage transactions in a Spring boot application and used to define a scope of transaction.
- This annotation can be applied to the class level or method level.
- It provides data reliability and consistency.
- When a method is indicated with @Transactional annotation, it indicates that the particular method should be executed within the context of that transaction.
- If the transaction becomes successful then the changes made to the database are committed, if any transaction fails, all the changes made to that particular transaction can be rollback and it will ensure that the database remains in a consistent state.

## Example: Configure Transaction in Spring Boot

Reference: (https://www.geeksforgeeks.org/spring-boot-transaction-management-using-transactional-annotation/)

In this example, we will create an application to store user information along with his address information and will use spring transaction management to resolve the transaction break problem.

NOTES: We are going to continue this example using previous (existing) project created in "Spring and Persistence".

1. Create model class.

   In this step, we will create our model class. Here, we will be creating two model classes, Employee and Address.

   ```java
   package com.example.springjpademo;

   import javax.persistence.Column;
   import javax.persistence.Entity;
   import javax.persistence.GeneratedValue;
   import javax.persistence.GenerationType;
   import javax.persistence.Id;
   import javax.persistence.Table;

   @Entity
   @Table(name = "employee")
   public class Employee {

      @Id
    	@GeneratedValue(strategy = GenerationType.AUTO)
    	private int id;
    
    	@Column(name = "name")
    	private String name;

       public int getId() {
           return id;
       }

       public void setId(int id) {
           this.id = id;
       }

       public String getName() {
           return name;
       }

       public void setName(String name) {
           this.name = name;
       }
    }
    ```

   ```java
   package com.example.springjpademo;

   import javax.persistence.Entity;
   import javax.persistence.GeneratedValue;
   import javax.persistence.GenerationType;
   import javax.persistence.Id;
   import javax.persistence.OneToOne;
   import javax.persistence.Table;

   @Entity
   @Table(name = "address")
   public class Address {
       @Id
       @GeneratedValue(strategy = GenerationType.AUTO)
       private Long id;
   
       @Column(name = "address")
       private String address;

       // one to one mapping means, one employee stays at one address only
       @OneToOne
       private Employee employee;

       public Long getId() {
           return id;
       }

       public void setId(Long id) {
           this.id = id;
       }

       public String getAddress() {
           return address;
       }

       public void setAddress(String address) {
           this.address = address;
       }

       public Employee getEmployee() {
           return employee;
       }

       public void setEmployee(Employee employee) {
           this.employee = employee;
       }
   }
   ```

2. Create the repository.

   ```java
   package com.example.springjpademo;

   import org.springframework.data.jpa.repository.JpaRepository;

   public interface EmployeeRepository extends JpaRepository<Employee, Integer> {

   }
   ```

   ```java
   package com.example.springjpademo;

   import org.springframework.data.jpa.repository.JpaRepository;

   public interface AddressRepository extends JpaRepository<Address, Integer> {

   }
   ```

3. Create the service.

   You can use @Transactional annotation in service layer which will result interacting with the database. In this step, we will create a service layer for our application and add business logic to it. For this, we will be creating two classes EmployeeService and AddressService. In EmployeeService class we are throwing an exception.

   ```java
   ```
   
