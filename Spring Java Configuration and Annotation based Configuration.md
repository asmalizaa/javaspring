# Spring Java Configuration and Annotation based Configuration

Starting from Spring 2.5 it became possible to configure the dependency injection using annotations. So instead of using XML to describe a bean wiring, you can move the bean configuration into the component class itself by using annotations on the relevant class, method, or field declaration.

Annotation injection is performed before XML injection. Thus, the latter configuration will override the former for properties wired through both approaches.

## Coupling in Java

In object oriented design, Coupling refers to the degree of direct knowledge that one element has of another. In other words, how often do changes in class A force related changes in class B. There are two types of coupling.

1. Tight coupling.

   - In general, Tight coupling means the two classes often change together. In other words, if A knows more than it should about the way in which B was implemented, then A and B are tightly coupled.
   - Example : If you want to change the skin, you would also have to change the design of your body as well because the two are joined together – they are tightly coupled. The best example of tight coupling is RMI (Remote Method Invocation).

   ```java
   // Java program to illustrate tight coupling concept
   class Subject {
       Topic t = new Topic();

       public void startReading() {
           t.understand();
       }
   } 
   class Topic {
       public void understand() {
           System.out.println("Tight coupling concept");
       }
   } 
   ```

   In the above program the Subject class is dependents on Topic class. In the above program Subject class is tightly coupled with Topic class it means if any change in the Topic class requires Subject class to change. For example, if Topic class understand() method change to gotit() method then you have to change the startReading() method will call gotit() method instead of calling understand() method.
   
3. Loose coupling.

   - In simple words, loose coupling means they are mostly independent.
   - If the only knowledge that class A has about class B, is what class B has exposed through its interface, then class A and class B are said to be loosely coupled.
   - In order to over come from the problems of tight coupling between objects, spring framework uses dependency injection mechanism with the help of POJO/POJI model and through dependency injection its possible to achieve loose coupling.
   - Example : If you change your shirt, then you are not forced to change your body – when you can do that, then you have loose coupling. When you can’t do that, then you have tight coupling. The examples of Loose coupling are Interface, JMS.

   ```java
   // Java program to illustrate loose coupling concept 
   public interface Topic {
       void understand();
   }
   class Topic1 implements Topic {
       public void understand() {
           System.out.println("Got it");
       }
   }
   class Topic2 implements Topic {
       public void understand() {
           System.out.println("understand");
       }
   }
   public class Subject {
       public static void main(String[] args) {
           Topic t = new Topic1();
           t.understand();
       }
   } 
   ```

   In the above example, Topic1 and Topic2 objects are loosely coupled. It means Topic is an interface and we can inject any of the implemented classes at run time and we can provide service to the end user.

### Which is better tight coupling or loose coupling?

In general, Tight Coupling is bad in but most of the time, because it reduces flexibility and re-usability of code, it makes changes much more difficult, it impedes test ability etc. loose coupling is a better choice because A loosely coupled will help you when your application need to change or grow. If you design with loosely coupled architecture, only a few parts of the application should be affected when requirements change. 

![image](https://github.com/asmalizaa/javaspring/assets/23090837/2f564ca6-3d17-45f8-9a5a-ba81da45d33a)

- Tight coupling is not good at the test-ability. But loose coupling improves the test ability.
- Tight coupling does not provide the concept of interface. But loose coupling helps us follow the GOF principle of program to interfaces, not implementations.
- In Tight coupling, it is not easy to swap the codes between two classes. But it’s much easier to swap other pieces of code/modules/objects/components in loose coupling.
- Tight coupling does not have the changing capability. But loose coupling is highly changeable.

## The IoC Container

Spring Official Reference: (https://docs.spring.io/spring-framework/reference/core/beans.html)

### What Is Inversion of Control?

Inversion of Control is a principle in software engineering which transfers the control of objects or portions of a program to a container or framework. We most often use it in the context of object-oriented programming.

In contrast with traditional programming, in which our custom code makes calls to a library, IoC enables a framework to take control of the flow of a program and make calls to our custom code. To enable this, frameworks use abstractions with additional behavior built in. If we want to add our own behavior, we need to extend the classes of the framework or plugin our own classes.

The advantages of this architecture are:
- decoupling the execution of a task from its implementation
- making it easier to switch between different implementations
- greater modularity of a program
- greater ease in testing a program by isolating a component or mocking its dependencies, and allowing components to communicate through contracts

We can achieve Inversion of Control through various mechanisms such as: Strategy design pattern, Service Locator pattern, Factory pattern, and Dependency Injection (DI).

### The Spring IoC Container

An IoC container is a common characteristic of frameworks that implement IoC.

In the Spring framework, the interface ApplicationContext represents the IoC container. The Spring container is responsible for instantiating, configuring and assembling objects known as beans, as well as managing their life cycles.

The Spring framework provides several implementations of the ApplicationContext interface: AnnotationConfigApplicationContext, ClassPathXmlApplicationContext and FileSystemXmlApplicationContext for standalone applications, and WebApplicationContext for web applications.

In order to assemble beans, the container uses configuration metadata, which can be in the form of XML configuration or annotations.

Here’s one way to manually instantiate a container:

```java
ApplicationContext context = new ClassPathXmlApplicationContext("applicationContext.xml");
```

And here’s an example of manually instantiating a container using AnnotationConfigApplicationContext:

```java
AnnotationConfigApplicationContext annotationContext = new AnnotationConfigApplicationContext();
```

When you create an instance of AnnotationConfigApplicationContext and provide it with one or more configuration classes, it scans these classes for the @Bean annotations and other relevant annotations. It then initializes and manages the beans defined in these classes, setting up their dependencies and managing their lifecycle. You can find the detailed example here.

To set the item attribute in the example above, we can use metadata. Then the container will read this metadata and use it to assemble beans at runtime.

