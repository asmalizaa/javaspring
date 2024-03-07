# Spring and Persistence

Reference: (https://docs.spring.io/spring-data/jpa/reference/jpa.html)

## What is ORM?

![image](https://github.com/asmalizaa/javaspring/assets/23090837/c94dff5f-46b6-4310-8e90-1b11da8f6576)

ORM stands for Object-Relational Mapping.

ORM sets the mapping between the set of objects which are written in the preferred programming language like JavaScript and relational database like SQL. It hides and encapsulates the SQL queries into objects and instead of SQL queries we can directly use the objects to implement the SQL query.

## What is JPA?

Reference: (https://jakarta.ee/learn/docs/jakartaee-tutorial/current/persist/persistence-intro/persistence-intro.html)

The Java Persistence API (JPA) is a specification of Java. It is used to persist data between Java object and relational database. JPA acts as a bridge between object-oriented domain models and relational database systems.

As JPA is just a specification, it does not perform any operation by itself. It requires an implementation. So, ORM tools like Hibernate, TopLink and iBatis implements JPA specifications for data persistence.

## What is Hibernate?

Reference: (https://hibernate.org/)
Reference: (https://docs.spring.io/spring-framework/reference/data-access/orm/hibernate.html)

Hibernate is a Java framework that simplifies the development of Java application to interact with the database. It is an open source, lightweight, ORM (Object Relational Mapping) tool. Hibernate implements the specifications of JPA (Java Persistence API) for data persistence.

## What is Spring Boot JPA?

Spring Boot JPA is a Java specification for managing relational data in Java applications. It allows us to access and persist data between Java object/ class and relational database. 

JPA follows Object-Relation Mapping (ORM). It is a set of interfaces. It also provides a runtime EntityManager API for processing queries and transactions on the objects against the database. 

It uses a platform-independent object-oriented query language JPQL (Java Persistent Query Language).

## JPA Architecture

![image](https://github.com/asmalizaa/javaspring/assets/23090837/489d9462-2852-4994-86af-b1ef285666b4)

1. Entity
   - An entity is a persistence domain object. Each Entity represents a table in a relational database, and each entity instance corresponds to a row in that table.
   - JPA uses Annotations or XML to map entities to a Relational database.
   - The persistent state of an entity fields or properties (setter and getter methods) use object/relational mapping annotations to map the entities and entity relationships to the relational data in the underlying data store.
2. Persistence Unit
   - A persistence unit defines a set of all entity classes that are managed by EntityManager instances in an application.
   - This set of entity classes represents the data contained within a single data store.
   - Persistence units are defined by the persistence.xml configuration file.
   - JPA uses the persistence.xml file to create the connection and setup the required environment. Provides information which is necessary for making database connections.
3. Persistence Class
   - Persistence (javax.persistence.Persistence) class contains java static methods to get EntityManagerFactory instances.
   - Since JPA 2.1 you can generatedatabase schemas and/or tables and/or create DDL scripts as determined by the supplied properties.
4. EntityManagerFactory
   - EntityManagerFactory (javax.persistence.EntityManagerFactory) class is a factory for EntityManagers.
   - During the application startup time EntityManagerFactory is created with the help of Persistence-Unit.
   - Typically, EntityManagerFactory is created once (One EntityManagerfactory object per Database) and kept alive for later use.
5. EntityManager
   - EntityManager is an interface to perform main actual database interactions.
6. Persistence Context: A persistence context handles a set of entities which hold data to be persisted in some persistence store (e.g. database).
   - Each EntityManager instance is associated with a PersistenceContext.
7. EntityTransaction
   - A transaction is a set of operations that either fail or succeed as a unit.
   - A database transaction consists of a set of SQL operations that are committed or rolled back as a single unit
   - Any kind of modifications initiated via EntityManager object are placed within a transaction. An EntityManager object helps creating an EntityTransaction

![image](https://github.com/asmalizaa/javaspring/assets/23090837/df55b885-9d4b-479e-aae0-6f611e40ba2e)

## Activity: Example of Spring Data JPA

Reference: (https://www.bezkoder.com/spring-boot-postgresql-example/)

### Create a new project using Spring Initializr

1. Use Spring Initializr to create a new project with below settings.
   - Project: Maven
   - Language: Java
   - Spring Boot: default
   - Group: com.example
   - Artifact: spring-data-jpa-demo
   - Name: spring-data-jpa-demo
   - Description: Demo project for Spring Data JPA
   - Package name: com.example.spring-data-jpa-demo
   - Packaging: Jar
   - Java: 21
   - Dependencies: Spring Web, Spring Data JPA, PostgreSQL Driver

2. Click Generate. Extract the downloaded zip file then import it into Eclipse.

### Add Spring Data JPA dependency into existing project

If you have already an existing Maven project and want to add Spring Data JPA dependency, add below codes into pom.xml

```xml
<dependency>
	<groupId>org.springframework.boot</groupId>
	<artifactId>spring-boot-starter-data-jpa</artifactId>
</dependency>
```

### Connect to PostgreSQL database

NOTES: Make sure a database called 'testdb' has been created before continuing to next step.

Add below configurations into application.properties file

```
spring.datasource.url=jdbc:postgresql://localhost:5432/testdb
spring.datasource.username=postgres
spring.datasource.password=Pa$$w0rd

spring.jpa.properties.hibernate.jdbc.lob.non_contextual_creation=true 
spring.jpa.properties.hibernate.dialect=org.hibernate.dialect.PostgreSQLDialect

# Hibernate ddl auto (create, create-drop, validate, update) 
spring.jpa.hibernate.ddl-auto=update

#show sql values
logging.level.org.hibernate.type.descriptor.sql=trace
logging.level.org.hibernate.type.descriptor.sql.BasicBinder=TRACE
logging.level.org.hibernate.SQL=DEBUG
```

### Create JPA entity class to represent a table

Our Data model is Tutorial with four fields: id, title, description, published.

```java
package com.example.springjpademo;

import javax.persistence.Column;
import javax.persistence.Entity;
import javax.persistence.GeneratedValue;
import javax.persistence.GenerationType;
import javax.persistence.Id;
import javax.persistence.Table;

@Entity
@Table(name = "tutorials")
public class Tutorial {

	@Id
	@GeneratedValue(strategy = GenerationType.AUTO)
	private long id;

	@Column(name = "title")
	private String title;

	@Column(name = "description")
	private String description;

	@Column(name = "published")
	private boolean published;

	public Tutorial() {

	}

	public Tutorial(String title, String description, boolean published) {
		this.title = title;
		this.description = description;
		this.published = published;
	}

	public long getId() {
		return id;
	}

	public String getTitle() {
		return title;
	}

	public void setTitle(String title) {
		this.title = title;
	}

	public String getDescription() {
		return description;
	}

	public void setDescription(String description) {
		this.description = description;
	}

	public boolean isPublished() {
		return published;
	}

	public void setPublished(boolean isPublished) {
		this.published = isPublished;
	}

	@Override
	public String toString() {
		return "Tutorial [id=" + id + ", title=" + title + ", desc=" + description + ", published=" + published + "]";
	}

}
```

### Create a CRUD Repository interface for JPA entity

Let us create a repository to interact with Tutorials from the database.

```java
package com.example.springjpademo;

import java.util.List;

import org.springframework.data.jpa.repository.JpaRepository;

public interface TutorialRepository extends JpaRepository<Tutorial, Long> {

	List<Tutorial> findByPublished(boolean published);

	List<Tutorial> findByTitleContaining(String title);

}
```

### Using Spring JPA Query Method

Now we can use JpaRepository’s methods: save(), findOne(), findById(), findAll(), count(), delete(), deleteById()… without implementing these methods.

### Using CRUD Repository interface in REST Controller

Finally, we create a controller that provides APIs for creating, retrieving, updating, deleting and finding Tutorials.

```java
package com.example.springjpademo;

import java.util.ArrayList;
import java.util.List;
import java.util.Optional;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.http.HttpStatus;
import org.springframework.http.ResponseEntity;
import org.springframework.web.bind.annotation.DeleteMapping;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.PathVariable;
import org.springframework.web.bind.annotation.PostMapping;
import org.springframework.web.bind.annotation.PutMapping;
import org.springframework.web.bind.annotation.RequestBody;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RequestParam;
import org.springframework.web.bind.annotation.RestController;

@RestController
@RequestMapping("/api")
public class TutorialController {

	@Autowired
	TutorialRepository tutorialRepository;

	@GetMapping("/tutorials")
	public ResponseEntity<List<Tutorial>> getAllTutorials(@RequestParam(required = false) String title) {
		try {
			List<Tutorial> tutorials = new ArrayList<Tutorial>();

			if (title == null)
				tutorialRepository.findAll().forEach(tutorials::add);
			else
				tutorialRepository.findByTitleContaining(title).forEach(tutorials::add);

			if (tutorials.isEmpty()) {
				return new ResponseEntity<>(HttpStatus.NO_CONTENT);
			}

			return new ResponseEntity<>(tutorials, HttpStatus.OK);
		} catch (Exception e) {
			return new ResponseEntity<>(null, HttpStatus.INTERNAL_SERVER_ERROR);
		}
	}

	@GetMapping("/tutorials/{id}")
	public ResponseEntity<Tutorial> getTutorialById(@PathVariable("id") long id) {
		Optional<Tutorial> tutorialData = tutorialRepository.findById(id);

		if (tutorialData.isPresent()) {
			return new ResponseEntity<>(tutorialData.get(), HttpStatus.OK);
		} else {
			return new ResponseEntity<>(HttpStatus.NOT_FOUND);
		}
	}

	@PostMapping("/tutorials")
	public ResponseEntity<Tutorial> createTutorial(@RequestBody Tutorial tutorial) {
		try {
			Tutorial _tutorial = tutorialRepository
					.save(new Tutorial(tutorial.getTitle(), tutorial.getDescription(), tutorial.isPublished()));
			return new ResponseEntity<>(_tutorial, HttpStatus.CREATED);
		} catch (Exception e) {
			return new ResponseEntity<>(null, HttpStatus.INTERNAL_SERVER_ERROR);
		}
	}

	@PutMapping("/tutorials/{id}")
	public ResponseEntity<Tutorial> updateTutorial(@PathVariable("id") long id, @RequestBody Tutorial tutorial) {
		Optional<Tutorial> tutorialData = tutorialRepository.findById(id);

		if (tutorialData.isPresent()) {
			Tutorial _tutorial = tutorialData.get();
			_tutorial.setTitle(tutorial.getTitle());
			_tutorial.setDescription(tutorial.getDescription());
			_tutorial.setPublished(tutorial.isPublished());
			return new ResponseEntity<>(tutorialRepository.save(_tutorial), HttpStatus.OK);
		} else {
			return new ResponseEntity<>(HttpStatus.NOT_FOUND);
		}
	}

	@DeleteMapping("/tutorials/{id}")
	public ResponseEntity<HttpStatus> deleteTutorial(@PathVariable("id") long id) {
		try {
			tutorialRepository.deleteById(id);
			return new ResponseEntity<>(HttpStatus.NO_CONTENT);
		} catch (Exception e) {
			return new ResponseEntity<>(HttpStatus.INTERNAL_SERVER_ERROR);
		}
	}

	@DeleteMapping("/tutorials")
	public ResponseEntity<HttpStatus> deleteAllTutorials() {
		try {
			tutorialRepository.deleteAll();
			return new ResponseEntity<>(HttpStatus.NO_CONTENT);
		} catch (Exception e) {
			return new ResponseEntity<>(HttpStatus.INTERNAL_SERVER_ERROR);
		}

	}

	@GetMapping("/tutorials/published")
	public ResponseEntity<List<Tutorial>> findByPublished() {
		try {
			List<Tutorial> tutorials = tutorialRepository.findByPublished(true);

			if (tutorials.isEmpty()) {
				return new ResponseEntity<>(HttpStatus.NO_CONTENT);
			}
			return new ResponseEntity<>(tutorials, HttpStatus.OK);
		} catch (Exception e) {
			return new ResponseEntity<>(HttpStatus.INTERNAL_SERVER_ERROR);
		}
	}

}
```

### Run and Test

1. Run the project.
2. Use Postman to test the service.

![image](https://github.com/asmalizaa/javaspring/assets/23090837/5cc6ef34-dd97-486b-a662-878ae771b6cc)

3. Table tutorials will be automatically generated in database.

![image](https://github.com/asmalizaa/javaspring/assets/23090837/069a6c36-8f23-4414-8b66-1e63aff6e985)

4. Try to insert a new tutorial record by sending a POST request.

![image](https://github.com/asmalizaa/javaspring/assets/23090837/32db3ede-87a3-4264-83bd-4c44f849d33f)

5. Verify that the new record is added into table tutorials.

![image](https://github.com/asmalizaa/javaspring/assets/23090837/b3a0fc14-701d-42fa-9e40-df156c6f4faa)

6. Try to add another few records into the table and verify.

![image](https://github.com/asmalizaa/javaspring/assets/23090837/aceb52d1-78a8-4a3a-a822-d8a50e66be5c)

7. Try to update existing record.

![image](https://github.com/asmalizaa/javaspring/assets/23090837/89c46f1b-7f38-4d74-bc3c-18169819798c)

8. Verify the update in table tutorials.

![image](https://github.com/asmalizaa/javaspring/assets/23090837/ed139c05-3a82-4396-9b30-4f59834f021c)

9. Get all tutorial records.

![image](https://github.com/asmalizaa/javaspring/assets/23090837/2ed78932-90ef-4d79-a00c-6f298235183b)

10. Get a record by id.

![image](https://github.com/asmalizaa/javaspring/assets/23090837/10fb8365-33f4-4c93-8f96-c4b2f1db697c)

11. Find all published tutorials.

![image](https://github.com/asmalizaa/javaspring/assets/23090837/dad2c9e1-8d1b-4484-9e2d-58efe1cafff9)

12. Find all tutorials which title contains 'ring'.

![image](https://github.com/asmalizaa/javaspring/assets/23090837/73ba0417-e667-468c-986d-b9527f4efe10)

13. Delete a tutorial record.

![image](https://github.com/asmalizaa/javaspring/assets/23090837/b972a0b1-b4b8-4aef-8afa-1d7551e56328)

14. Verify record deleted in database.

![image](https://github.com/asmalizaa/javaspring/assets/23090837/a2160020-d946-4f5a-af46-0cbef725a2d4)

15. Finally, delete all records in table.

![image](https://github.com/asmalizaa/javaspring/assets/23090837/4b7c7445-44d5-4e5d-8367-e8b45f243e48)

16. Verify table is now empty.

![image](https://github.com/asmalizaa/javaspring/assets/23090837/ea993e3d-f2d5-4f0a-b89a-a9458ed48f7a)

The end.
