# Develop Web Applications using the Spring Framework - Spring MVC

Reference: (https://docs.spring.io/spring-framework/reference/web/webmvc.html)

Spring Web MVC is the original web framework built on the Servlet API and has been included in the Spring Framework from the very beginning. The formal name, "Spring Web MVC," comes from the name of its source module (spring-webmvc), but it is more commonly known as "Spring MVC".

## What is Spring MVC?

Spring MVC is a Java-based framework that is mostly used for developing web applications. It follows the MVC (Model-View-Controller) Design Pattern. This design pattern specifies that an application consists of a data model, presentation information, and control information.

This framework is developed around a DispatcherServlet which dispatches requests to handlers. In the current industry, many of them are using Spring Boot Microservices, but there are many projects still running in Spring MVC. So it is worth learning Spring MVC in the recent era. That’s why we are going to cover all the things which are part of the Spring MVC framework one by one in an organized manner.

## Spring – MVC Framework

Spring MVC Framework follows the Model-View-Controller architectural design pattern which works around the Front Controller i.e. the Dispatcher Servlet. The Dispatcher Servlet handles and dispatches all the incoming HTTP requests to the appropriate controller. It uses @Controller and @RequestMapping as default request handlers. The @Controller annotation defines that a particular class is a controller. @RequestMapping annotation maps web requests to Spring Controller methods. The terms model, view, and controller are as follows:

- Model: The Model encapsulates the application data.
- View: View renders the model data and generates HTML output that the client’s browser can interpret.
- Controller: The Controller processes the user requests and passes them to the view for rendering.

## DispatcherServlet

Dispatcher Servlet is the front controller that manages the entire HTTP request and response handling process. 

Now, the question is What is Front Controller? It is quite simple, as the name suggests, when any web requests are made, the requests will come first to the front Controller which is nothing but the Dispatcher Servlet. The Front Controller stands first that is why it’s name is like this. After the requests comes into this, the dispatcher servlet accepts the requests and decides which controller will be suitable to handle these requests. Then it dispatches the HTTP requests to specific controller.

![image](https://github.com/asmalizaa/javaspring/assets/23090837/1bae210f-cfab-4f89-8487-34b56ccc6306)

1. All the incoming requests are intercepted by the DispatcherServlet that works as the front controller.
2. The DispatcherServlet then gets an entry of handler mapping from the XML file and forwards the request to the controller.
3. The object of ModelAndView is returned by the controller.
4. The DispatcherServlet checks the entry of the view resolver in the XML file and invokes the appropriate view component.

![image](https://github.com/asmalizaa/javaspring/assets/23090837/c8cc88ad-6406-4ff8-9e5d-eb2cd11c5f54)

## Activity: Spring Web MVC

In this activity, we are going to add a form to add a new tutorial.

**Steps**

1. Add dependencies to your existing project.

   - Thymeleaf dependency to your project (if needed).

     ```xml
     <dependency>
         <groupId>org.springframework.boot</groupId>
         <artifactId>spring-boot-starter-thymeleaf</artifactId>
     </dependency>
     ```

   - Spring Boot Devtools (if needed).
     ```xml
     <dependency>
     	<groupId>org.springframework.boot</groupId>
     	<artifactId>spring-boot-devtools</artifactId>
     	<scope>runtime</scope>
     	<optional>true</optional>
     </dependency>
     ```

2. Add a welcome page in this location src/main/resources/static

   ```html
   <!DOCTYPE html>
   <html>
       <head>
           <meta charset="UTF-8">
           <title>Welcome Page</title>
       </head>
   <body>
       <h1>Welcome Page</h1>
       <p>Add new tutorial click <a href="/addnew">here</a></p>
   </body>
   </html>
   ```
   
3. Create a TutorialService class that will act as the Controller.

   ```java
   import org.springframework.stereotype.Controller;
   import org.springframework.ui.Model;
   import org.springframework.web.bind.annotation.GetMapping;
   import org.springframework.web.bind.annotation.ModelAttribute;
   import org.springframework.web.bind.annotation.PostMapping;

   @Controller
   public class TutorialService {
       @GetMapping("/addnew")
       public String addNewForm(Model model) {
           model.addAttribute("tutorial", new Tutorial());
           return "addnew";
       }

       @PostMapping("/addnew")
       public String addNewSubmit(@ModelAttribute Tutorial tutorial, Model model) {
           model.addAttribute("tutorial", tutorial);
           return "result";
       }
   }
   ```

   This controller is concise and simple, but a lot is going on. The rest of this section analyzes it step by step.
   - The mapping annotations let you map HTTP requests to specific controller methods. The two methods in this controller are both mapped to /addnew.
   - You can use @RequestMapping (which, by default, maps all HTTP operations, such as GET, POST, and so forth).
   - However, in this case, the addNewForm() method is specifically mapped to GET by using @GetMapping, while addNewSubmit() is mapped to POST with @PostMapping.
   - This mapping lets the controller differentiate the requests to the /addnew endpoint.
   - The addNewForm() method uses a Model object to expose a new Tutorial to the view template.
   - The implementation of the method body relies on a view technology to perform server-side rendering of the HTML by converting the view name (addnew) into a template to render.
   - In this case, we use Thymeleaf, which parses the addnew.html template and evaluates the various template expressions to render the form.
   - The following listing (from src/main/resources/templates/addnew.html) shows the addnew template.

5. Create the 'Add New Tutorial' form page in this location src/main/resources/templates

   ```html
   <!DOCTYPE HTML>
   <html xmlns:th="https://www.thymeleaf.org">
   <head>
      <title>Add New Tutorial</title>
      <meta http-equiv="Content-Type" content="text/html; charset=UTF-8" />
   </head>
   <body>
      <h1>Add New Tutorial</h1>
      <form action="#" th:action="@{/addnew}" th:object="${tutorial}" method="post">
         <p>Title: <input type="text" th:field="*{title}" /></p>
         <p>Description: <input type="text" th:field="*{description}" /></p>
         <p><input type="submit" value="Submit" /> <input type="reset" value="Reset" /></p>
      </form>
   </body>
   </html>
   ```

   - The th:action="@{/addnew}" expression directs the form to POST to the /addnew endpoint, while the th:object="${tutorial}" expression declares the model object to use for collecting the form data.
   - The three form fields, expressed with th:field="{id}", th:field="{title}" and th:field="{description}", correspond to the fields in the Tutorial object.
   - That covers the controller, model, and view for presenting the form. Now we can review the process of submitting the form.
   - As noted earlier, the form submits to the /addnew endpoint by using a POST call.
   - The addNewSubmit() method receives the Tutorial object that was populated by the form.
   - The Tutorial is a @ModelAttribute, so it is bound to the incoming form content.
   - Also, the submitted data can be rendered in the result view by referring to it by name (by default, the name of the method parameter, so tutorial in this case).
   - The id is rendered in the ```<p th:text="'id: ' + ${tutorial.id}" />``` expression.
   - Likewise, the title is rendered in the ```<p th:text="'title: ' + ${tutorial.title}" />``` expression.
   - The following listing (from src/main/resources/templates/result.html) shows the result template.

4. Create the 'Result' page in this location src/main/resources/templates

   ```html
   <!DOCTYPE HTML>
   <html xmlns:th="https://www.thymeleaf.org">
   <head>
      <title>Result</title>
      <meta http-equiv="Content-Type" content="text/html; charset=UTF-8" />
   </head>
   <body>
      <h1>Result</h1>
      <p th:text="'Id: ' + ${tutorial.id}" />
      <p th:text="'Title: ' + ${tutorial.title}" />
      <p th:text="'Description: ' + ${tutorial.description}" />
      <p th:text="'Published: ' + ${tutorial.published}" />
      <a href="/addnew">Add another</a>
   </body>
   </html>
   ```

   For clarity, this example uses two separate view templates for rendering the form and displaying the submitted data. However, you can use a single view for both purposes.

5. Test the service.

   Now that the web site is running, visit http://localhost:8080/addnew, where you see the following form.

   <img width="171" alt="image" src="https://github.com/asmalizaa/javaspring/assets/23090837/cefbb518-6015-4f3d-a60e-1f282def3460">

   Submit an ID, Title and Description to see the results.

   <img width="119" alt="image" src="https://github.com/asmalizaa/javaspring/assets/23090837/4164c91b-0d90-40bb-bf81-6c58305eac98">

   Congratulations! You have just used Spring to create and submit a form.
