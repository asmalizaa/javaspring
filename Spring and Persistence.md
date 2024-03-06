# Spring and Persistence

Reference: (https://docs.spring.io/spring-data/jpa/reference/jpa.html)

## What is ORM?

![image](https://github.com/asmalizaa/javaspring/assets/23090837/c94dff5f-46b6-4310-8e90-1b11da8f6576)

ORM stands for Object-Relational Mapping.

ORM sets the mapping between the set of objects which are written in the preferred programming language like JavaScript and relational database like SQL. It hides and encapsulates the SQL queries into objects and instead of SQL queries we can directly use the objects to implement the SQL query.

## What is JPA?

The Java Persistence API (JPA) is a specification of Java. It is used to persist data between Java object and relational database. JPA acts as a bridge between object-oriented domain models and relational database systems.

As JPA is just a specification, it does not perform any operation by itself. It requires an implementation. So, ORM tools like Hibernate, TopLink and iBatis implements JPA specifications for data persistence.

## What is Hibernate?

Hibernate is a Java framework that simplifies the development of Java application to interact with the database. It is an open source, lightweight, ORM (Object Relational Mapping) tool. Hibernate implements the specifications of JPA (Java Persistence API) for data persistence.

## What is Spring Boot JPA?

Spring Boot JPA is a Java specification for managing relational data in Java applications. It allows us to access and persist data between Java object/ class and relational database. 

JPA follows Object-Relation Mapping (ORM). It is a set of interfaces. It also provides a runtime EntityManager API for processing queries and transactions on the objects against the database. 

It uses a platform-independent object-oriented query language JPQL (Java Persistent Query Language).
