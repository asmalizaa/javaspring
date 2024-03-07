# Thymeleaf

[Thymeleaf](http://www.thymeleaf.org/) is a Java template engine for processing and creating HTML, XML, JavaScript, CSS and text.

Thymeleaf's main goal is to bring elegant natural templates to your development workflow — HTML that can be correctly displayed in browsers and also work as static prototypes, allowing for stronger collaboration in development teams.

The library is extremely extensible, and its natural templating capability ensures we can prototype templates without a back end. This makes development very fast when compared with other popular template engines such as JSP.

## Natural Templates

HTML templates written in Thymeleaf still look and work like HTML, letting the actual templates that are run in your application keep working as useful design artifacts.

```html
<table>
<thead>
    <tr>
      <th th:text="#{msgs.headers.name}">Name</th>
      <th th:text="#{msgs.headers.price}">Price</th>
    </tr>
  </thead>
  <tbody>
    <tr th:each="prod: ${allProducts}">
      <td th:text="${prod.name}">Oranges</td>
      <td th:text="${#numbers.formatDecimal(prod.price, 1, 2)}">0.99</td>
    </tr>
  </tbody>
</table>
```

## Spring MVC and Thymeleaf: how to access data from templates

Reference: (https://www.thymeleaf.org/doc/articles/springmvcaccessdata.html)

In a typical Spring MVC application, @Controller classes are responsible for preparing a model map with data and selecting a view to be rendered. This model map allows for the complete abstraction of the view technology and, in the case of Thymeleaf, it is transformed into a Thymeleaf context object (part of the Thymeleaf template execution context) that makes all the defined variables available to expressions executed in templates.

## Spring model attributes

Spring MVC calls the pieces of data that can be accessed during the execution of views model attributes. The equivalent term in Thymeleaf language is context variables.

There are several ways of adding model attributes to a view in Spring MVC. Below you will find some common cases.

Add attribute to Model via its addAttribute method.

```java
@RequestMapping(value = "message", method = RequestMethod.GET)
public String messages(Model model) {
    model.addAttribute("messages", messageRepository.findAll());
    return "message/list";
}
```

Return ModelAndView with model attributes included.

```java
@RequestMapping(value = "message", method = RequestMethod.GET)
public ModelAndView messages() {
    ModelAndView mav = new ModelAndView("message/list");
    mav.addObject("messages", messageRepository.findAll());
    return mav;
}
```

Expose common attributes via methods annotated with @ModelAttribute

```java
@ModelAttribute("messages")
public List<Message> messages() {
    return messageRepository.findAll();
}
```

As you may have noticed, in all the above cases the messages attribute is added to the model and it will be available in Thymeleaf views.

In Thymeleaf, these model attributes (or context variables in Thymeleaf jargon) can be accessed with the following syntax: ${attributeName}, where attributeName in our case is messages. This is a Spring EL expression. In short, Spring EL (Spring Expression Language) is a language that supports querying and manipulating an object graph at runtime.

You can access model attributes in views with Thymeleaf as follows.

```html
 <tr th:each="message : ${messages}">
    <td th:text="${message.id}">1</td>
    <td><a href="#" th:text="${message.title}">Title ...</a></td>
    <td th:text="${message.text}">Text ...</td>
</tr>
```

## Activity: Display List of Records

In this activity, we are going to create a page to display list of records.

1. Update index.html to include link to call the list page.

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
       <p>View list of tutorials click <a href="/all">here</a></p>
   </body>
   </html>
   ```

2. Update the TutorialService.java to include a new method to display list of records page.

   ```java
   import org.springframework.beans.factory.annotation.Autowired;
   import org.springframework.stereotype.Controller;
   import org.springframework.ui.Model;
   import org.springframework.web.bind.annotation.GetMapping;
   import org.springframework.web.bind.annotation.ModelAttribute;
   import org.springframework.web.bind.annotation.PostMapping;

   @Controller
   public class TutorialService {
       @Autowired
       TutorialRepository tutorialRepository;

       @GetMapping("/addnew")
       public String addNewForm(Model model) {
           model.addAttribute("tutorial", new Tutorial());
           return "addnew";
       }

       @PostMapping("/addnew")
       public String addNewSubmit(@ModelAttribute Tutorial tutorial, Model model) {
           Tutorial _tutorial = tutorialRepository
                       .save(new Tutorial(tutorial.getTitle(), tutorial.getDescription(), tutorial.isPublished()));
           model.addAttribute("tutorial", _tutorial);
           return "result";
       }

       @GetMapping("/all")
       public String showAll(Model model) {
           model.addAttribute("tutorials", tutorialRepository.findAll());
           return "alltutorials";
       }
   }
   ```

3. Create a new page all alltutorials.html in src/main/resources/templates

   ```html
   <!DOCTYPE html>
   <html xmlns:th="https://www.thymeleaf.org">
   <head>
       <meta charset="UTF-8">
       <title>List of Tutorials</title>
   </head>
   <body>
       <h1>List of Tutorials</h1>
       <table>
       <thead>
           <tr>
               <th>ID</th>
               <th>Title</th>
               <th>Description</th>
               <th>Published</th>
           </tr>
       </thead>
       <tbody>
           <tr th:if="${tutorials.empty}">
               <td colspan="2">No Records Found</td>
           </tr>
           <tr th:each="tutorial : ${tutorials}">
               <td><span th:text="${tutorial.id}"> ID </span></td>
               <td><span th:text="${tutorial.title}"> Title </span></td>
               <td><span th:text="${tutorial.description}"> Description </span></td>
               <td><span th:text="${tutorial.published}"> Published </span></td>
           </tr>
       </tbody>
       </table>
   </body>
   </html>
   ```
   
4. Run and test. You should see a page that looks like below.

   <img width="154" alt="image" src="https://github.com/asmalizaa/javaspring/assets/23090837/61e70394-c698-4635-b608-da32d07f0deb">

The end.
