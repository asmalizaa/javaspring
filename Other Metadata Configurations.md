# Other Metadata Configurations

## Spring @Required Annotation

Spring Annotations allow us to configure dependencies and implement dependency injection through java programs. Those are a form of metadata that provides data about a program. The @Required annotation in spring is a method-level annotation used in the setter method of a bean property and therefore making the setter-injection compulsory. This annotation suggests that the required bean property must be injected with a value at the configuration time which we will show and explain in the following example.  

```java
import org.springframework.beans.factory.annotation.Required;
import org.springframework.beans.factory.annotation.Value;

public class Student {

	private int rollNo;
	private String name;
	private int age;

	@Required
	public void setRollNo(int rollNo) {
		this.rollNo = rollNo;
	}

	@Value("${student.name}")
	public void setName(String name) {
		this.name = name;
	}

	@Value("${student.age}")
	public void setAge(int age) {
		this.age = age;
	}

	public void display(){
		System.out.println("Roll No: " + rollNo);
		System.out.println("Name: " + name);
		System.out.println("Age: " + age);
	}
}
```

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

## Using @Value

Reference: (https://docs.spring.io/spring-framework/reference/core/beans/annotation-config/value-annotations.html)

@Value is typically used to inject externalized properties:

```java
@Component
public class MovieRecommender {

    private final String catalog;

    public MovieRecommender(@Value("${catalog.name}") String catalog) {
        this.catalog = catalog;
    }
}
```

With the following configuration:

```java
@Configuration
@PropertySource("classpath:application.properties")
public class AppConfig { }
```

And the following application.properties file:

```java
catalog.name=MovieCatalog
```

In that case, the catalog parameter and field will be equal to the MovieCatalog value.

## The Spring @Qualifier Annotation

The @Autowired annotation is a great way of making the need to inject a dependency in Spring explicit. Although it’s useful, there are use cases for which this annotation alone isn’t enough for Spring to understand which bean to inject.

By default, Spring resolves autowired entries by type.

If more than one bean of the same type is available in the container, the framework will throw NoUniqueBeanDefinitionException, indicating that more than one bean is available for autowiring.

Let’s imagine a situation in which two possible candidates exist for Spring to inject as bean collaborators in a given instance:

```java
@Component("fooFormatter")
public class FooFormatter implements Formatter {
 
    public String format() {
        return "foo";
    }
}

@Component("barFormatter")
public class BarFormatter implements Formatter {
 
    public String format() {
        return "bar";
    }
}

@Component
public class FooService {
     
    @Autowired
    private Formatter formatter;
}
```

If we try to load FooService into our context, the Spring framework will throw a NoUniqueBeanDefinitionException. This is because Spring doesn’t know which bean to inject. To avoid this problem, there are several solutions; the @Qualifier annotation is one of them.

By using the @Qualifier annotation, we can eliminate the issue of which bean needs to be injected.

Let’s revisit our previous example to see how we solve the problem by including the @Qualifier annotation to indicate which bean we want to use:

```java
public class FooService {
     
    @Autowired
    @Qualifier("fooFormatter")
    private Formatter formatter;
}
```

By including the @Qualifier annotation, together with the name of the specific implementation we want to use, in this example Foo, we can avoid ambiguity when Spring finds multiple beans of the same type.
