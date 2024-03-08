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

1. Create model classes.

   In this step, we will create our model class. Here, we will be creating two model classes, Employee and Address.

   ```java
   import jakarta.persistence.Column;
   import jakarta.persistence.Entity;
   import jakarta.persistence.GeneratedValue;
   import jakarta.persistence.GenerationType;
   import jakarta.persistence.Id;
   import jakarta.persistence.Table;

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
   import jakarta.persistence.Column;
   import jakarta.persistence.Entity;
   import jakarta.persistence.GeneratedValue;
   import jakarta.persistence.GenerationType;
   import jakarta.persistence.Id;
   import jakarta.persistence.OneToOne;
   import jakarta.persistence.Table;

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

2. Create the repositories.

   ```java
   import org.springframework.data.jpa.repository.JpaRepository;

   public interface EmployeeRepository extends JpaRepository<Employee, Integer> {

   }
   ```

   ```java
   import org.springframework.data.jpa.repository.JpaRepository;

   public interface AddressRepository extends JpaRepository<Address, Integer> {

   }
   ```

3. Create the services.

   You can use @Transactional annotation in service layer which will result interacting with the database. In this step, we will create a service layer for our application and add business logic to it. For this, we will be creating two classes EmployeeService and AddressService. In EmployeeService class we are throwing an exception.

   ```java
   import jakarta.transaction.Transactional;
   import org.springframework.beans.factory.annotation.Autowired;
   import org.springframework.stereotype.Service;

   @Service
   public class EmployeeService {
      @Autowired
      private EmployeeRepository employeeRepository;

      @Autowired
      private AddressService addressService;

      @Transactional
      public Employee addEmployee(Employee employee) throws Exception {
         Employee employeeSavedToDB = this.employeeRepository.save(employee);

         Address address = new Address();
         address.setId(123L);
         address.setAddress("Varanasi");
         address.setEmployee(employee);

         // calling addAddress() method of AddressService class
         this.addressService.addAddress(address);
         return employeeSavedToDB;
      }
   }
   ```

   ```java
   import org.springframework.beans.factory.annotation.Autowired;
   import org.springframework.stereotype.Service;

   @Service
   public class AddressService {
       @Autowired
       private AddressRepository addressRepository;

       public Address addAddress(Address address) {
           Address addressSavedToDB = this.addressRepository.save(address);
           return addressSavedToDB;
       }
   }
   ```

4. Create the controller.

   In this step, we will create a controller for our application. For this, we will create a Controller class and add all the mappings to it.

   ```java
   import org.springframework.beans.factory.annotation.Autowired;
   import org.springframework.http.HttpStatus;
   import org.springframework.http.ResponseEntity;
   import org.springframework.web.bind.annotation.PostMapping;
   import org.springframework.web.bind.annotation.RequestBody;
   import org.springframework.web.bind.annotation.RequestMapping;
   import org.springframework.web.bind.annotation.RestController;

   @RestController
   @RequestMapping("/api/employee")
   public class TransactionController {
       @Autowired
       private EmployeeService employeeService;

       @PostMapping("/add")
       public ResponseEntity<Employee> saveEmployee(@RequestBody Employee employee) throws Exception {
           Employee employeeSavedToDB = this.employeeService.addEmployee(employee);
           return new ResponseEntity<Employee>(employeeSavedToDB, HttpStatus.CREATED);
       }
   }
   ```

5. Run the application and test it using postman.

   ![image](https://github.com/asmalizaa/javaspring/assets/23090837/e1a97d66-6223-4609-9ae2-9fa384d374a6)

   Check database to see if the new record is added.

   ![image](https://github.com/asmalizaa/javaspring/assets/23090837/a9e1ebbd-cd3b-4d8d-94c0-78b5c1b1a2ef)

   ![image](https://github.com/asmalizaa/javaspring/assets/23090837/0a4babab-cf76-407a-b677-40b066a1219c)

6. Interrupt the transaction.

   In this step, we will break down our transaction. For this, we will initialize the address object with a NULL value in our EmployeeService class.

   ```java
   import jakarta.transaction.Transactional;
   import org.springframework.beans.factory.annotation.Autowired;
   import org.springframework.stereotype.Service;

   @Service
   public class EmployeeService {
       @Autowired
       private EmployeeRepository employeeRepository;

       @Autowired
       private AddressService addressService;

       @Transactional
       public Employee addEmployee(Employee employee) throws Exception {
           Employee employeeSavedToDB = this.employeeRepository.save(employee);

           // we will initialize the address object as null
           Address address = null;
           address.setId(123L);
           address.setAddress("Varanasi");
           address.setEmployee(employee);

           // calling addAddress() method of AddressService class
           this.addressService.addAddress(address);
           return employeeSavedToDB;
       }
   }
   ```

   Now, we will delete our table from the database and again run our application and will request the application to create an employee.

   As a result, we have initialized the address object as null and requested the application, we have an employee created in the database but the address information is not, as we have received a null pointer exception. But, this is not good practice in transaction management, as employees should be saved only when the address is saved and vice-versa.

7. Transaction management.

   To overcome this problem, we will use @Transactional annotation. This will ensure that the transaction should be complete. That is, either both employee and address data should be stored or nothing will get stored. For using transaction management, we need to use @EnableTransactionManagement in the main class of our spring boot application and also, and we need to annotate our addEmployee() method in EmployeeService class with @Transactional annotation.

   ```java
   import org.springframework.boot.SpringApplication;
   import org.springframework.boot.autoconfigure.SpringBootApplication;
   import org.springframework.transaction.annotation.EnableTransactionManagement;

   @SpringBootApplication
   @EnableTransactionManagement
   public class TransactionManagementApplication {
       public static void main(String[] args) {
           SpringApplication.run(TransactionManagementApplication.class, args);
       }
   }
   ```

8. Run the application.

   Now, we have enabled transaction management for our application. We will again delete the tables from our database and request our application to add an employee.

   As a result, this time the employee data do not get stored in the database, nor did the address data. This way the spring has handled the transaction that both employees and address data gets stored or no data gets stored.
