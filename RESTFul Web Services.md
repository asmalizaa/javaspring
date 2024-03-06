# RESTFul Web Services

## What is JSON, HTTP Method, REST API and Web Server?

JSON
- JSON stands for JavaScript Object Notation
- JSON is a lightweight format for storing and transporting data
- JSON is often used when data is sent from a server to a web page
- JSON is "self-describing" and easy to understand

```json
{
  "employees":[
      {"firstName":"John", "lastName":"Doe"},
      {"firstName":"Anna", "lastName":"Smith"},
      {"firstName":"Peter", "lastName":"Jones"}
  ]
}
```
JSON Syntax Rules
- Data is in name/value pairs
- Data is separated by commas
- Curly braces hold objects
- Square brackets hold arrays

HTTP Method
- The Hypertext Transfer Protocol (HTTP) is designed to enable communications between clients and servers.
- HTTP works as a request-response protocol between a client and server.

![image](https://github.com/asmalizaa/javaspring/assets/23090837/ea2945f5-88a5-410d-a28c-596512262235)

**Example**

A client (browser) sends an HTTP request to the server; then the server returns a response to the client. The response contains status information about the request and may also contain the requested content.

<table>
  <tr><th>HTTP Method</th><th>Description</th></tr>
  <tr><td>GET</td><td>Used to request data from a specified resource.</td></tr>
  <tr><td>POST</td><td>Used to send data to a server to create/update a resource.</td></tr>
  <tr><td>PUT</td><td>Used to send data to a server to create/update a resource.</td></tr>
  <tr><td>DELETE</td><td>Deletes the specified resource.</td></tr>
  <tr><td>HEAD</td><td>Almost identical to GET, but without the response body.</td></tr>
  <tr><td>TRACE</td><td>Describes the communication options for the target resource.</td></tr>
</table>

Web Service

![image](https://github.com/asmalizaa/javaspring/assets/23090837/7a839ba9-87b8-4208-92a1-f3d0a7974bbf)

- A web service is a collection of open protocols and standards used for exchanging data between applications or systems.
- Software applications written in various programming languages and running on various platforms can use web services to exchange data over computer networks like the Internet in a manner like inter-process communication on a single computer.
- This interoperability (e.g., between Java and Python, or Windows and Linux applications) is due to the use of open standards.

REST API
- An API is an application programming interface. It is a set of rules that allow programs to talk to each other. The developer creates the API on the server and allows the client to talk to it.
- REST determines how the API looks like. It stands for “Representational State Transfer”. It is a set of rules that developers follow when they create their API. One of these rules states that you should be able to get a piece of data (called a resource) when you link to a specific URL.
- Each URL is called a request while the data sent back to you is called a response.

Web Server
- The term web server can refer to hardware or software, or both working together.
- On the hardware side, a web server is a computer that stores web server software and a website's component files. (For example, HTML documents, images, CSS stylesheets, and JavaScript files) A web server connects to the Internet and supports physical data interchange with other devices connected to the web.
- On the software side, a web server includes several parts that control how web users access hosted files. At a minimum, this is an HTTP server. An HTTP server is software that understands URLs (web addresses) and HTTP (the protocol your browser uses to view webpages). An HTTP server can be accessed through the domain names of the websites it stores, and it delivers the content of these hosted websites to the end user's device.

## How does REST API works 

<table>
  <tr><th>Terminology</th><th>Description</th></tr>
  <tr><td>Client</td><td>The person or program using the API. 
The client makes requests to the API to retrieve some information or change something within the application.
Your browser is a client – it interacts with APIs for different websites to get page content. The requested info is sent back to your browser and displayed.
</td></tr>
  <tr><td>Resource</td><td>Any piece of information that the API can provide the client.
For instance, a resource in Facebook’s API could be a user, a page, a photo, or a post. Each resource has a unique name, called the resource identifier.
</td></tr>
  <tr><td>Server</td><td>Used by the application that receives client request i.e., service, and contains resources that the client wants. The server has an API to interact with clients without giving them direct access to content stored in its database.</td></tr>
</table>

![image](https://github.com/asmalizaa/javaspring/assets/23090837/6f1a656b-4d9e-42ae-bc80-47713e119da6)

- To get access to a resource, the client sends an HTTP request. In return, the server generates an HTTP response with encoded data on the resource.
- Both types of REST messages are self-descriptive, meaning they contain information on how to interpret and process them.

## REST request structure

Any REST request includes four essential parts: an HTTP method, an endpoint, headers, and a body.

<table>
  <tr><th>Component</th><th>Description</th></tr>
  <tr><td>HTTP Method</td><td>Describes what is to be done with a resource. There are four basic methods also name CRUD operations.</td></tr>
  <tr><td>Endpoint</td><td>Contains a Uniform Resource Identifier (URI) indicating where and how to find the resource on the internet.
The most common type of URI is a Uniform Resource Locater (URL), serving as a complete web address.
</td></tr>
  <tr><td>Headers</td><td>Store information relevant to both the client and server. Mainly, headers provide authentication data – such as an API key, the name or IP address of the computer where the server is installed, and the information about the response format.</td></tr>
  <tr><td>Body</td><td>Used to convey additional information to the server. For instance, it may be a piece of data you want to add or replace.</td></tr>
</table>

![image](https://github.com/asmalizaa/javaspring/assets/23090837/b792c4fe-cd8e-4a6b-af0b-bd38b4750b0e)

## REST response structure

In response, the server sends not the sought-for resource itself, but its representation – a machine-readable description of its current state. The same resource can be represented in different formats, but the most popular ones are XML and JSON.

![image](https://github.com/asmalizaa/javaspring/assets/23090837/d95b62ba-d051-46c0-a4f2-231e77233402)

## Microservices Architecture 

![image](https://github.com/asmalizaa/javaspring/assets/23090837/bf81127c-7365-45dd-9f6b-cc25a03f3b16)

Microservice architecture, aka microservices, are a specific method of designing software systems to structure a single application as a collection of loosely coupled services. 

Applications tend to begin as a monolithic architecture (more on that below), and over time grow into a set of interconnected microservices.

The main idea behind microservices is that some types of applications are easier to build and maintain when they are broken down into many small pieces that work together. 

Each component of a microservice architecture has:
- Its own CPU
- Its own runtime environment
- Often, a dedicated team working in it, ensuring each service is distinct from one another

This architecture means each service can:
- Run its own unique process
- Communicate autonomously without having to rely on the other microservices or the application as a whole

## Activity: Greeting Service

Reference: (https://spring.io/guides/gs/rest-service)

You will build a service that will accept HTTP GET requests at (http://localhost:8080/greeting)

It will respond with a JSON representation of a greeting, as the following listing shows:

![image](https://github.com/asmalizaa/javaspring/assets/23090837/87eed750-d25d-4548-9333-51a95be0871c)

You can customize the greeting with an optional name parameter in the query string, as the following listing shows:

![image](https://github.com/asmalizaa/javaspring/assets/23090837/048d32c5-aebc-4615-b73a-51d2aee227b4)

The name parameter value overrides the default value of World and is reflected in the response, as the following listing shows:

![image](https://github.com/asmalizaa/javaspring/assets/23090837/c5d93dce-3224-4970-ad7b-7dc16f1d7ddf)

### Starting with Spring Initialize

1. Go to https://start.spring.io/
2. Configure the new project.
   - Project: Maven
   - Language: Java
   - Sprint Boot: default selection
   - Project Metadata: default settings
   - Packaging: Jar
   - Java: 21
   - Dependencies: Spring Web
   - Click Generate button.
3. Extract the downloaded zip file.
4. Import Maven project into Eclipse.

### Create a Resource Representation Class

Now that you have set up the project and build system, you can create your web service.

Begin the process by thinking about service interactions.

The service will handle GET requests for /greeting, optionally with a name parameter in the query string. The GET request should return a 200 OK response with JSON in the body that represents a greeting. It should resemble the following output:

![image](https://github.com/asmalizaa/javaspring/assets/23090837/9fd28906-d262-47d9-ad11-74a9ed3620c8)

The id field is a unique identifier for the greeting, and content is the textual representation of the greeting.

To model the greeting representation, create a resource representation class. To do so, provide a plain old Java object with fields, constructors, and accessors for the id and content data, as below.

```java
public class Greeting {
    private final long id;
    private final String content;

    public Greeting(long id, String content) {
        this.id = id;
        this.content = content;
    }

    public long getId() {
        return id;
    }

    public String getContent() {
        return content;
    }
}
```

### Create a Resource Controller

In Spring’s approach to building RESTful web services, HTTP requests are handled by a controller. 

These components are identified by the @RestController annotation, and the GreetingController shown in the following listing, handles GET requests for /greeting by returning a new instance of the Greeting class.

```java
import java.util.concurrent.atomic.AtomicLong;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RequestParam;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class GreetingController {

	private static final String template = "Hello, %s!";
	private final AtomicLong counter = new AtomicLong();

	@GetMapping("/greeting")
	public Greeting greeting(@RequestParam(value = "name", defaultValue = "World") String name) {
		return new Greeting(counter.incrementAndGet(), String.format(template, name));
	}
}
```

This controller is concise and simple, but there is plenty going on under the hood. We break it down step by step.

- The @GetMapping annotation ensures that HTTP GET requests to /greeting are mapped to the greeting() method.
- @RequestParam binds the value of the query string parameter name into the name parameter of the greeting() method. If the name parameter is absent in the request, the defaultValue of World is used.
- The implementation of the method body creates and returns a new Greeting object with id and content attributes based on the next value from the counter and formats the given name by using the greeting template.
- This code uses Spring @RestController annotation, which marks the class as a controller where every method returns a domain object instead of a view. It is shorthand for including both @Controller and @ResponseBody.

Run the application. Test the service by going to (http://localhost:8080/greeting) where you should see

![image](https://github.com/asmalizaa/javaspring/assets/23090837/83c3bb43-1d7d-4a75-8c77-135dd1f73d13)

Provide a name query string parameter by visiting http://localhost:8080/greeting?name=User. Notice how the value of the content attribute changes from Hello, World! to Hello, User!, as the following listing shows:

![image](https://github.com/asmalizaa/javaspring/assets/23090837/f91e7fa2-7dfe-4c1b-9f60-35d61bb37d80)

This change demonstrates that the @RequestParam arrangement in GreetingController is working as expected. The name parameter has been given a default value of World but can be explicitly overridden through the query string.

Notice also how the id attribute has changed from 1 to 2. This proves that you are working against the same GreetingController instance across multiple requests and that its counter field is being incremented on each call as expected.


