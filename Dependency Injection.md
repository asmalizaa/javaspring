# Dependency Injection

Reference: (https://docs.spring.io/spring-framework/reference/core/beans/dependencies/factory-collaborators.html)

### What Is Dependency Injection?

Dependency injection is a pattern we can use to implement IoC, where the control being inverted is setting an object’s dependencies.

Connecting objects with other objects, or “injecting” objects into other objects, is done by an assembler rather than by the objects themselves.

Here’s how we would create an object dependency in traditional programming:

```java
public class Store {
    private Item item;
 
    public Store() {
        item = new ItemImpl1();    
    }
}
```

In the example above, we need to instantiate an implementation of the Item interface within the Store class itself.

By using DI, we can rewrite the example without specifying the implementation of the Item that we want:

```java
public class Store {
    private Item item;
    public Store(Item item) {
        this.item = item;
    }
}
```

Dependency Injection in Spring can be done through constructors, setters or fields.

### Constructor-Based Dependency Injection

In the case of constructor-based dependency injection, the container will invoke a constructor with arguments each representing a dependency we want to set.

Spring resolves each argument primarily by type, followed by name of the attribute, and index for disambiguation. Let’s see the configuration of a bean and its dependencies using annotations:

```java
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.ComponentScan;
import org.springframework.context.annotation.Configuration;

@Configuration
@ComponentScan("com.example.di")
public class Config {

	@Bean
	public Engine engine() {
		return new Engine("v8", 5);
	}

	@Bean
	public Transmission transmission() {
		return new Transmission("sliding");
	}
}
```

Here we’re using annotations to notify Spring runtime that this class provides bean definitions (@Bean annotation), and that the package com.example.di needs to perform a context scan for additional beans.

- The @Configuration annotation indicates that the class is a source of bean definitions. We can also add it to multiple configuration classes.
- We use the @Bean annotation on a method to define a bean. If we don’t specify a custom name, then the bean name will default to the method name.
- For a bean with the default singleton scope, Spring first checks if a cached instance of the bean already exists, and only creates a new one if it doesn’t. If we’re using the prototype scope, the container returns a new bean instance for each method call.

Next, we define a Car class.

```java
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Component;

@Component
public class Car {
	private final Engine engine;
	private final Transmission transmission;

	@Autowired
	public Car(Engine engine, Transmission transmission) {
		this.engine = engine;
		this.transmission = transmission;
	}

	@Override
	public String toString() {
		return String.format("Engine: %s Transmission: %s", engine, transmission);
	}
}
```

Here are the definitions of Engine and Transmission.

```java
public class Engine {
	private final String type;
	private final int volume;

	public Engine(String type, int volume) {
		this.type = type;
		this.volume = volume;
		System.out.println("Engine constructor");
	}

	@Override
	public String toString() {
		return String.format("%s %d", type, volume);
	}
}
```

```java
public class Transmission {
	private final String type;

	public Transmission(String type) {
		this.type = type;
		System.out.println("Transmission constructor");
	}

	@Override
	public String toString() {
		return String.format("%s", type);
	}
}
```

Finally, we need to bootstrap an ApplicationContext using our POJO configuration.

```java
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.context.ApplicationContext;
import org.springframework.context.annotation.AnnotationConfigApplicationContext;

@SpringBootApplication
public class AppRunner {

	public static void main(String[] args) {
		ApplicationContext context = new AnnotationConfigApplicationContext(Config.class);

		Car car = context.getBean(Car.class);
		System.out.println(car);
	}
}
```

Run the application, verify that the output similar to below.

```java
Engine constructor
Transmission constructor
Engine: v8 5 Transmission: sliding
```

### Setter-Based Dependency Injection

For setter-based DI, the container will call setter methods of our class after invoking a no-argument constructor or no-argument static factory method to instantiate the bean. Let’s create this configuration using annotations:

```java
@Bean
public Store store() {
    Store store = new Store();
    store.setItem(item1());
    return store;
}
```

We can also use XML for the same configuration of beans:

```java
<bean id="store" class="org.baeldung.store.Store">
    <property name="item" ref="item1" />
</bean>
```

We can combine constructor-based and setter-based types of injection for the same bean. The Spring documentation recommends using constructor-based injection for mandatory dependencies, and setter-based injection for optional ones.

### Field-Based Dependency Injection

In case of Field-Based DI, we can inject the dependencies by marking them with an @Autowired annotation:

```java
public class Store {
    @Autowired
    private Item item; 
}
```

While constructing the Store object, if there’s no constructor or setter method to inject the Item bean, the container will use reflection to inject Item into Store.

We can also achieve this using XML configuration.

## Bean Scopes

Reference: (https://docs.spring.io/spring-framework/reference/core/beans/factory-scopes.html)

When you create a bean definition, you create a recipe for creating actual instances of the class defined by that bean definition. The idea that a bean definition is a recipe is important, because it means that, as with a class, you can create many object instances from a single recipe.

You can control not only the various dependencies and configuration values that are to be plugged into an object that is created from a particular bean definition but also control the scope of the objects created from a particular bean definition. This approach is powerful and flexible, because you can choose the scope of the objects you create through configuration instead of having to bake in the scope of an object at the Java class level. Beans can be defined to be deployed in one of a number of scopes. The Spring Framework supports six scopes, four of which are available only if you use a web-aware ApplicationContext. You can also create a custom scope.

<table>
    <tr><th>Scope</th><th>Description</th></tr>
    <tr><td>singleton</td><td>(Default) Scopes a single bean definition to a single object instance for each Spring IoC container.</td></tr>
    <tr><td>prototype</td><td>Scopes a single bean definition to any number of object instances.</td></tr>
    <tr><td>request</td><td>Scopes a single bean definition to the lifecycle of a single HTTP request. That is, each HTTP request has its own instance of a bean created off the back of a single bean definition. Only valid in the context of a web-aware Spring ApplicationContext.</td></tr>
    <tr><td>session</td><td>Scopes a single bean definition to the lifecycle of an HTTP Session. Only valid in the context of a web-aware Spring ApplicationContext.</td></tr>
    <tr><td>application</td><td>Scopes a single bean definition to the lifecycle of a ServletContext. Only valid in the context of a web-aware Spring ApplicationContext.</td></tr>
    <tr><td>websocket</td><td>Scopes a single bean definition to the lifecycle of a WebSocket. Only valid in the context of a web-aware Spring ApplicationContext.</td></tr>
</table>

## Using @Autowired

Reference: (https://docs.spring.io/spring-framework/reference/core/beans/annotation-config/autowired.html)

You can apply the @Autowired annotation to constructors, as the following example shows:

```java
public class MovieRecommender {

	private final CustomerPreferenceDao customerPreferenceDao;

	@Autowired
	public MovieRecommender(CustomerPreferenceDao customerPreferenceDao) {
		this.customerPreferenceDao = customerPreferenceDao;
	}

	// ...
}
```

You can also apply the @Autowired annotation to traditional setter methods, as the following example shows:

```java
public class SimpleMovieLister {

	private MovieFinder movieFinder;

	@Autowired
	public void setMovieFinder(MovieFinder movieFinder) {
		this.movieFinder = movieFinder;
	}

	// ...
}
```

You can also apply the annotation to methods with arbitrary names and multiple arguments, as the following example shows:

```java
public class MovieRecommender {

	private MovieCatalog movieCatalog;

	private CustomerPreferenceDao customerPreferenceDao;

	@Autowired
	public void prepare(MovieCatalog movieCatalog,
			CustomerPreferenceDao customerPreferenceDao) {
		this.movieCatalog = movieCatalog;
		this.customerPreferenceDao = customerPreferenceDao;
	}

	// ...
}
```

You can apply @Autowired to fields as well and even mix it with constructors, as the following example shows:

```java
public class MovieRecommender {

	private final CustomerPreferenceDao customerPreferenceDao;

	@Autowired
	private MovieCatalog movieCatalog;

	@Autowired
	public MovieRecommender(CustomerPreferenceDao customerPreferenceDao) {
		this.customerPreferenceDao = customerPreferenceDao;
	}

	// ...
}
```

By default, autowiring fails when no matching candidate beans are available for a given injection point. In the case of a declared array, collection, or map, at least one matching element is expected.

## Using @PostConstruct and @PreDestroy

Reference: (https://docs.spring.io/spring-framework/reference/core/beans/annotation-config/postconstruct-and-predestroy-annotations.html)

Introduced in Spring 2.5, the support for these annotations offers an alternative to the lifecycle callback mechanism described in initialization callbacks and destruction callbacks. Provided that the CommonAnnotationBeanPostProcessor is registered within the Spring ApplicationContext, a method carrying one of these annotations is invoked at the same point in the lifecycle as the corresponding Spring lifecycle interface method or explicitly declared callback method. In the following example, the cache is pre-populated upon initialization and cleared upon destruction:

```java
public class CachingMovieLister {

	@PostConstruct
	public void populateMovieCache() {
		// populates the movie cache upon initialization...
	}

	@PreDestroy
	public void clearMovieCache() {
		// clears the movie cache upon destruction...
	}
}
```
