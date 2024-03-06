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
The term web server can refer to hardware or software, or both working together.

- On the hardware side, a web server is a computer that stores web server software and a website's component files. (For example, HTML documents, images, CSS stylesheets, and JavaScript files) A web server connects to the Internet and supports physical data interchange with other devices connected to the web.
- On the software side, a web server includes several parts that control how web users access hosted files. At a minimum, this is an HTTP server. An HTTP server is software that understands URLs (web addresses) and HTTP (the protocol your browser uses to view webpages). An HTTP server can be accessed through the domain names of the websites it stores, and it delivers the content of these hosted websites to the end user's device.

