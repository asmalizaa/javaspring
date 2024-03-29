# Introduction to Spring

Reference: (https://spring.io/)

Spring Framework is a Java platform that provides comprehensive infrastructure support for developing Java applications. Spring handles the infrastructure so you can focus on your application.

Spring enables you to build applications from "plain old Java objects" (POJOs) and to apply enterprise services non-invasively to POJOs. This capability applies to the Java SE programming model and to full and partial Java EE.

Examples of how you, as an application developer, can use the Spring platform advantage:
- Make a Java method execute in a database transaction without having to deal with transaction APIs.
- Make a local Java method a remote procedure without having to deal with remote APIs.
- Make a local Java method a management operation without having to deal with JMX APIs.
- Make a local Java method a message handler without having to deal with JMS APIs.

## Features of the Spring Framework

The features of the Spring framework such as IoC, AOP, and transaction management, make it unique among the list of frameworks. Some of the most important features of the Spring framework are as follows:

- IoC container

  Refers to the core container that uses the DI or IoC pattern to implicitly provide an object reference in a class during runtime. This pattern acts as an alternative to the service locator pattern. The IoC container contains assembler code that handles the configuration management of application objects.
The Spring framework provides two packages, namely org.springframework.beans and org.springframework.context which helps in providing the functionality of the IoC container.

- Data access framework

  Allows the developers to use persistence APIs, such as JDBC and Hibernate, for storing persistence data in database. It helps in solving various problems of the developer, such as how to interact with a database connection, how to make sure that the connection is closed, how to deal with exceptions, and how to implement transaction management It also enables the developers to easily write code to access the persistence data throughout the application.
  
- Spring MVC framework

  Allows you to build Web applications based on MVC architecture. All the requests made by a user first go through the controller and are then dispatched to different views, that is, to different JSP pages or Servlets. The form handling and form validating features of the Spring MVC framework can be easily integrated with all popular view technologies such as ISP, Jasper Report, FreeMarker, and Velocity.
  
- Transaction management

  Helps in handling transaction management of an application without affecting its code. This framework provides Java Transaction API (JTA) for global transactions managed by an application server and local transactions managed by using the JDBC Hibernate, Java Data Objects (JDO), or other data access APIs. It enables the developer to model a wide range of transactions on the basis of Spring’s declarative and programmatic transaction management.
  
- Spring Web Service

  Generates Web service endpoints and definitions based on Java classes, but it is difficult to manage them in an application. To solve this problem, Spring Web Service provides layered-based approaches that are separately managed by Extensible Markup Language (XML) parsing (the technique of reading and manipulating XML). Spring provides effective mapping for transmitting incoming XML message request to an object and the developer to easily distribute XML message (object) between two machines.
  
- JDBC abstraction layer

  Helps the users in handling errors in an easy and efficient manner. The JDBC programming code can be reduced when this abstraction layer is implemented in a Web application. This layer handles exceptions such as DriverNotFound. All SQLExceptions are translated into the DataAccessException class. Spring’s data access exception is not JDBC specific and hence Data Access Objects (DAO) are not bound to JDBC only.
  
- Spring TestContext framework

  Provides facilities of unit and integration testing for the Spring applications. Moreover, the Spring TestContext framework provides specific integration testing functionalities such as context management and caching DI of test fixtures, and transactional test management with default rollback semantics.

## Spring Architecture

The Spring Framework consists of features organized into about 20 modules. These modules are grouped into Core Container, Data Access/Integration, Web, AOP (Aspect Oriented Programming), Instrumentation, and Test, as shown in the following diagram.

![image](https://github.com/asmalizaa/javaspring/assets/23090837/76bc5bd7-bcf5-4e81-aeee-2e15def7f7c3)

### Core Container

The Core Container consists of the Core, Beans, Context, and Expression Language modules.

The Core and Beans modules provide the fundamental parts of the framework, including the IoC and Dependency Injection features. The BeanFactory is a sophisticated implementation of the factory pattern. It removes the need for programmatic singletons and allows you to decouple the configuration and specification of dependencies from your actual program logic.

The Context module builds on the solid base provided by the Core and Beans modules: it is a means to access objects in a framework-style manner that is similar to a JNDI registry. The Context module inherits its features from the Beans module and adds support for internationalization (using, for example, resource bundles), event-propagation, resource-loading, and the transparent creation of contexts by, for example, a servlet container. The Context module also supports Java EE features such as EJB, JMX ,and basic remoting. The ApplicationContext interface is the focal point of the Context module.

The Expression Language module provides a powerful expression language for querying and manipulating an object graph at runtime. It is an extension of the unified expression language (unified EL) as specified in the JSP 2.1 specification. The language supports setting and getting property values, property assignment, method invocation, accessing the context of arrays, collections and indexers, logical and arithmetic operators, named variables, and retrieval of objects by name from Spring's IoC container. It also supports list projection and selection as well as common list aggregations.

### Data Access/Integration

The Data Access/Integration layer consists of the JDBC, ORM, OXM, JMS and Transaction modules.

The JDBC module provides a JDBC-abstraction layer that removes the need to do tedious JDBC coding and parsing of database-vendor specific error codes.

The ORM module provides integration layers for popular object-relational mapping APIs, including JPA, JDO, Hibernate, and iBatis. Using the ORM package you can use all of these O/R-mapping frameworks in combination with all of the other features Spring offers, such as the simple declarative transaction management feature mentioned previously.

The OXM module provides an abstraction layer that supports Object/XML mapping implementations for JAXB, Castor, XMLBeans, JiBX and XStream.

The Java Messaging Service (JMS) module contains features for producing and consuming messages.

The Transaction module supports programmatic and declarative transaction management for classes that implement special interfaces and for all your POJOs (plain old Java objects).

### Web

The Web layer consists of the Web, Web-Servlet, Web-Struts, and Web-Portlet modules.

Spring's Web module provides basic web-oriented integration features such as multipart file-upload functionality and the initialization of the IoC container using servlet listeners and a web-oriented application context. It also contains the web-related parts of Spring's remoting support.

The Web-Servlet module contains Spring's model-view-controller (MVC) implementation for web applications. Spring's MVC framework provides a clean separation between domain model code and web forms, and integrates with all the other features of the Spring Framework.

The Web-Struts module contains the support classes for integrating a classic Struts web tier within a Spring application. Note that this support is now deprecated as of Spring 3.0. Consider migrating your application to Struts 2.0 and its Spring integration or to a Spring MVC solution.

The Web-Portlet module provides the MVC implementation to be used in a portlet environment and mirrors the functionality of Web-Servlet module.

### AOP and Instrumentation

Spring's AOP module provides an AOP Alliance-compliant aspect-oriented programming implementation allowing you to define, for example, method-interceptors and pointcuts to cleanly decouple code that implements functionality that should be separated. Using source-level metadata functionality, you can also incorporate behavioral information into your code, in a manner similar to that of .NET attributes.

The separate Aspects module provides integration with AspectJ.

The Instrumentation module provides class instrumentation support and classloader implementations to be used in certain application servers.

### Test

The Test module supports the testing of Spring components with JUnit or TestNG. It provides consistent loading of Spring ApplicationContexts and caching of those contexts. It also provides mock objects that you can use to test your code in isolation.

## Setup Spring

There are two ways to start creating Spring project.

1. Spring Tools (STS)

   You can download the installer from [here](https://spring.io/tools)
   - Choose Spring Tools 4 for Eclipse.
   - Download installer for you respective OS eg. Windows.
   - Once downloaded, double-click to extract the files.
   - Move the extracted files to your working directory (optional).
   - Launch the STS.

2. Spring Initializr (https://start.spring.io/)

   This is web-based project bootstrap portal. You can configure your project here, generate and download the zip file, extract and import it into your IDE eg. Eclipse.
   

   
   
## Activity: A First Spring Application

This example was referenced from these two tutorials.
1. [Spring Quickstart Guide](https://spring.io/guides/gs/serving-web-content)
2. [Serving Web Content with Spring MVC](https://spring.io/guides/gs/serving-web-content)

**Steps**

1. Create a new spring project using Spring Initializr. Configure the new project with below settings.
   - Project: Maven
   - Language: Java
   - Spring Boot: default
   - Project Metadata:
     - Group: com.example
     - Artifact: firstdemo
     - Name: firstdemo
     - Description: First demo project for Spring
     - Package name: com.example.demo
   - Packaging: JAR
   - Java: choose the installed on your machine, else use default
   - Dependencies: Spring Web, Thymeleaf

   Once done, click "Generate", this will download the zip file.

2. Extract the zip file. Then import the maven project into Eclipse.
   - Right-click anywhere in Package Explorer > Import > Maven > Existing Maven Projects > browse to the location of the extracted project > Finish
   - Wait until project loaded completely before proceed to the next step.

3. Review the newly created project.
   - It should contain one java class: DemoApplication.java, this will be your project starting file.
   - Maven configuration file: pom.xml

4. At this moment, you cannot run and test your application, since it is still empty. So we are going to write a simple service that will display "Hello World!" message.
5. To do that, replace DemoApplication.java with codes below.

   ```java
   package com.example.demo;

    import org.springframework.boot.SpringApplication;
    import org.springframework.boot.autoconfigure.SpringBootApplication;
    import org.springframework.web.bind.annotation.GetMapping;
    import org.springframework.web.bind.annotation.RequestParam;
    
    @SpringBootApplication
    @RestController
    public class DemoApplication {
    
    	public static void main(String[] args) {
    		SpringApplication.run(DemoApplication.class, args);
    	}
    
    	 @GetMapping("/hello")
    	    public String hello(@RequestParam(value = "name", defaultValue = "World") String name) {
    	      return String.format("Hello %s!", name);
    	    }
    }
   ```
   This is all the code required to create a simple "Hello World" web service in Spring Boot.

   - The hello() method we’ve added is designed to take a String parameter called name, and then combine this parameter with the word "Hello" in the code.     This means that if you set your name to "Amy" in the request, the response would be "Hello Amy".
   - The @RestController annotation tells Spring that this code describes an endpoint that should be made available over the web. The @GetMapping(“/hello”) tells Spring to use our hello() method to answer requests that get sent to the http://localhost:8080/hello address. Finally, the @RequestParam is telling Spring to expect a name value in the request, but if it’s not there, it will use the word "World" by default.

6. Run the application by right-click the project > Run As > Java Application > select DemoApplication from the list > OK

   To test > type in your browser's address > (http://localhost:8080/hello)

7. Create an index.html in src/main/resources/static folder with codes below.

   ```html
   <!DOCTYPE html>
   <html>
   <head>
       <meta charset="UTF-8">
       <title>Welcome Page</title>
   </head>
   <body>
       <h1>Welcome Page</h1>
       <p>Hello! Please click <a href="/hello">here</a> to say "Hello World!"</p>
   </body>
   </html>
   ```
   Re-run the application and test. This time, use this instead (http://localhost:8080)

8. Create a Web Controller

   In Spring’s approach to building web sites, HTTP requests are handled by a controller. You can easily identify the controller by the @Controller annotation. In the following example, GreetingController handles GET requests for /greeting by returning the name of a View (in this case, greeting). A View is responsible for rendering the HTML content. The following listing (from src/main/java/com/example/servingwebcontent/GreetingController.java) shows the controller:

   - Create a new Java class called GreetingController.
   - Replace the codes with below.

     ```java
     package com.example.demo;

     import org.springframework.stereotype.Controller;
     import org.springframework.ui.Model;
     import org.springframework.web.bind.annotation.GetMapping;
     import org.springframework.web.bind.annotation.RequestParam;
    
     @Controller
     public class GreetingController {
    
    	@GetMapping("/greeting")
    	public String greeting(@RequestParam(name = "name", required = false, defaultValue = "World") String name,
    			Model model) {
    		model.addAttribute("name", name);
    		return "greeting";
    	}
     }
     ```

     This controller is concise and simple, but there is plenty going on. We break it down step by step.

     - The @GetMapping annotation ensures that HTTP GET requests to /greeting are mapped to the greeting() method.
     - @RequestParam binds the value of the query string parameter name into the name parameter of the greeting() method. This query string parameter is not required. If it is absent in the request, the defaultValue of World is used. The value of the name parameter is added to a Model object, ultimately making it accessible to the view template.
     - The implementation of the method body relies on a view technology (in this case, Thymeleaf) to perform server-side rendering of the HTML. Thymeleaf parses the greeting.html template and evaluates the th:text expression to render the value of the ${name} parameter that was set in the controller.The following listing (from src/main/resources/templates/greeting.html) shows the greeting.html template:

        ```html
        <!DOCTYPE HTML>
        <html xmlns:th="http://www.thymeleaf.org">
        <head> 
            <title>Getting Started: Serving Web Content</title> 
            <meta http-equiv="Content-Type" content="text/html; charset=UTF-8" />
        </head>
        <body>
            <p th:text="|Hello, ${name}!|" />
        </body>
        </html>
        ```

        Re-run the application and test. This time, use this instead (http://localhost:8080/greeting)
