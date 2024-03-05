# Other Metadata Configurations

## Spring @Required Annotation

Spring Annotations allow us to configure dependencies and implement dependency injection through java programs. Those are a form of metadata that provides data about a program. The @Required annotation in spring is a method-level annotation used in the setter method of a bean property and therefore making the setter-injection compulsory. This annotation suggests that the required bean property must be injected with a value at the configuration time which we will show and explain in the following example.  

1. First, let’s create a simple Spring Application and inject the literal values by setter injection. So, create a simple class Student having three attributes rollNo, name, and age. Create setter methods for these two attributes and a simple method to print the details of the student.
2. Let’s create a properties file in your classpath and name the file as student-info.properties (for this example we name it like this, you can name it according to your need). And in this file, we are going to write something like this.
3.  Let’s set the values from the properties file by using the @Value Annotation. So, we can modify our Student.java file something like this.
4.  Now let’s create a Student Bean in the beans.xml file. Below is the complete code for the beans.xml file.
5.  So now our bean is ready. Now let’s create a class and define the main() method inside that class. Suppose we have created a class named Main and we have defined the main() method inside this class. Below is the code for the Main.java class. Comments are added inside the code for better understanding.
6.  Now run your main() method and the output will be like this.
7.  So our application is working fine. Now let’s come again to the Student.java file and remove the @Value(“${student.rollNo}”) before the setRollNo() method. So now our modified Student.java file is something like this as follows:
8.  Now again run your main() method and the output will be like this.
9.  So the Student class object is created but the Roll no value has not been assigned. But we want the Roll No value must be filled before creating the Student class object. You can consider like Roll no is a primary key and we don’t want this value as null. So here @Required Annotation comes into the picture. So if we modify our Student.java file as the following them we are going to get exceptions in our program.
10.  So in this scenario, the exception console is trying to tell us that it’s mandatory to provide the value to the Roll no to create the Student class object. So if you want some field value must be filled with some value then you should use the @Required Annotation. So we can modify our Student.java file something like this as follows:
11.  Return the program again and you are going to get the output as below as shown:

## Injection with @Resource

Reference: (https://docs.spring.io/spring-framework/reference/core/beans/annotation-config/resource.html)

Spring also supports injection by using the JSR-250 @Resource annotation (jakarta.annotation.Resource) on fields or bean property setter methods. This is a common pattern in Jakarta EE: for example, in JSF-managed beans and JAX-WS endpoints. Spring supports this pattern for Spring-managed objects as well.

@Resource takes a name attribute. By default, Spring interprets that value as the bean name to be injected. In other words, it follows by-name semantics, as demonstrated in the following example:

```java
public class SimpleMovieLister {

	private MovieFinder movieFinder;

	@Resource(name="myMovieFinder")
	public void setMovieFinder(MovieFinder movieFinder) {
		this.movieFinder = movieFinder;
	}
}
```

If no name is explicitly specified, the default name is derived from the field name or setter method. In case of a field, it takes the field name. In case of a setter method, it takes the bean property name. The following example is going to have the bean named movieFinder injected into its setter method:

```java
public class SimpleMovieLister {

	private MovieFinder movieFinder;

	@Resource
	public void setMovieFinder(MovieFinder movieFinder) {
		this.movieFinder = movieFinder;
	}
}
```

In the exclusive case of @Resource usage with no explicit name specified, and similar to @Autowired, @Resource finds a primary type match instead of a specific named bean and resolves well known resolvable dependencies: the BeanFactory, ApplicationContext, ResourceLoader, ApplicationEventPublisher, and MessageSource interfaces.

Thus, in the following example, the customerPreferenceDao field first looks for a bean named "customerPreferenceDao" and then falls back to a primary type match for the type CustomerPreferenceDao:

```java
public class MovieRecommender {

	@Resource
	private CustomerPreferenceDao customerPreferenceDao;

	@Resource
	private ApplicationContext context;

	public MovieRecommender() {
	}

	// ...
}
```
