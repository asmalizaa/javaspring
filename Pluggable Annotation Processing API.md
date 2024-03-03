#  Pluggable Annotation Processing API

## Annotations in Java

Annotations are used to provide supplemental information about a program. 

- Annotations start with ‘@’.
- Annotations do not change the action of a compiled program.
- Annotations help to associate metadata (information) to the program elements i.e. instance variables, constructors, methods, classes, etc.
- Annotations are not pure comments as they can change the way a program is treated by the compiler. See below code for example.
- Annotations basically are used to provide additional information, so could be an alternative to XML and Java marker interfaces.

***Note: This program throws compiler error because we have mentioned override, but not overridden, we have overloaded display.***

```java
// Java Program to Demonstrate that Annotations are Not Barely Comments

// Class 1
class Base {

	// Method
	public void display() {
		System.out.println("Base display()");
	}
}

// Class 2
// Main class
class Derived extends Base {

	// Overriding method as already up in above class
	@Override public void display(int x) {
		// Print statement when this method is called
		System.out.println("Derived display(int )");
	}

	// Method 2
	// Main driver method
	public static void main(String args[]) {
		// Creating object of this class inside main()
		Derived obj = new Derived();

		// Calling display() method inside main()
		obj.display();
	}
}
```

## @Generated

The Generated annotation is used to mark source code that has been generated. It can also be used to differentiate user written code from generated code in a single file. When used, the value element must have the name of the code generator. The recommended convention is to use the fully qualified name of the code generator in the value field .

For example: com.company.package.classname. The date element is used to indicate the date the source was generated. The date element must follow the ISO 8601 standard. For example the date element would have the following value 2001-07-04T12:08:56.235-0700 which represents 2001-07-04 12:08:56 local time in the U.S. Pacific Time time zone.

```java
@Generated("com.example.Generator")
 
@Generated(value="com.example.Generator", date= "2017-07-04T12:08:56.235-0700")
 
@Generated(value="com.example.Generator", date= "2017-07-04T12:08:56.235-0700", comments= "comment 1")
```

## @Resource

The Resource annotation marks a resource that is needed by the application. This annotation may be applied to an application component class, or to fields or methods of the component class. When the annotation is applied to a field or method, the container will inject an instance of the requested resource into the application component when the component is initialized. If the annotation is applied to the component class, the annotation declares a resource that the application will look up at runtime.

Even though this annotation is not marked Inherited, deployment tools are required to examine all superclasses of any component class to discover all uses of this annotation in all superclasses. All such annotation instances specify resources that are needed by the application component. Note that this annotation may appear on private fields and methods of superclasses; the container is required to perform injection in these cases as well.

## @PostConstruct

The PostConstruct annotation is used on a method that needs to be executed after dependency injection is done to perform any initialization. This method MUST be invoked before the class is put into service. This annotation MUST be supported on all classes that support dependency injection. The method annotated with PostConstruct MUST be invoked even if the class does not request any resources to be injected. Only one method can be annotated with this annotation. The method on which the PostConstruct annotation is applied MUST fulfill all of the following criteria:

- The method MUST NOT have any parameters except in the case of interceptors in which case it takes an InvocationContext object as defined by the Interceptors specification.
- The method defined on an interceptor class MUST HAVE one of the following signatures:

  void MethodName (InvocationContext)

  Object MethodName (InvocationContext) throws Exception

  Note: A PostConstruct interceptor method must not throw application exceptions, but it may be declared to throw checked exceptions including the java.lang.Exception if the same interceptor method interposes on business or timeout methods in addition to lifecycle events. If a PostConstruct interceptor method returns a value, it is ignored by the container.

- The method defined on a non-interceptor class MUST HAVE the following signature:

  void MethodName ()

- The method on which PostConstruct is applied MAY be public, protected, package private or private.
- The method MUST NOT be static except for the application client.
- The method MAY be final.
- If the method throws an unchecked exception the class MUST NOT be put into service except in the case of EJBs where the EJB can handle exceptions and even recover from them.

## @PreDestroy

The PreDestroy annotation is used on methods as a callback notification to signal that the instance is in the process of being removed by the container. The method annotated with PreDestroy is typically used to release resources that it has been holding. This annotation MUST be supported by all container managed objects that support PostConstruct except the application client container in Java EE 5. The method on which the PreDestroy annotation is applied MUST fulfill all of the following criteria:

- The method MUST NOT have any parameters except in the case of interceptors in which case it takes an InvocationContext object as defined by the Interceptors specification.
- The method defined on an interceptor class MUST HAVE one of the following signatures:

  void MethodName (InvocationContext)

  Object MethodName (InvocationContext) throws Exception

  Note: A PreDestroy interceptor method must not throw application exceptions, but it may be declared to throw checked exceptions including the java.lang.Exception if the same interceptor method interposes on business or timeout methods in addition to lifecycle events. If a PreDestroy interceptor method returns a value, it is ignored by the container.

- The method defined on a non-interceptor class MUST HAVE the following signature:

  void MethodName ()

- The method on which PreDestroy is applied MAY be public, protected, package private or private.
- The method MUST NOT be static.
- The method MAY be final.
- If the method throws an unchecked exception it is ignored except in the case of EJBs where the EJB can handle exceptions.

## @DeclareRoles

This annotation is used to define the security roles that comprise the security model of the application. This annotation is specified on a class, and it typically would be used to define roles that could be tested (for example, by calling isUserInRole) from within the methods of the annotated class.

Following is an example of how this annotation would be used. In this example, BusinessAdmin is the only security role specified, but the value of this parameter can include a list of security roles specified by the application.

```java
@DeclareRoles("BusinessAdmin")
public class CalculatorServlet {
    //...
}
```

Specifying @DeclareRoles("BusinessAdmin") is equivalent to defining the following in web.xml:

```java
<web-app>
    <security-role>
        <role-name>BusinessAdmin</role-name>
    </security-role>
</web-app>
```

The syntax for declaring more than one role is as shown in the following example:

```java
@DeclareRoles({"Administrator", "Manager", "Employee"})
```

## @RolesAllowed

The @RolesAllowed annotation specifies the security roles permitted to access method(s) in an application. This annotation can be specified on a class or on method(s). When specified at the class level, it applies to all methods in the class. When specified on a method, it applies to that method only, and overrides any values specified at the class level.

To specify that no roles are authorized to access method(s) in an application, use the @DenyAll annotation. To specify that a user in any role is authorized to access the application, use the @PermitAll annotation.

When used in conjunction with the @DeclareRoles annotation, the combined set of security roles are used by the application.

Here is some example code that demonstrates the use of the RolesAllowed annotation.

```java
@RolesAllowed("AllUsers")
public class Calculator {
	@RolesAllowed("Administrator")
	public void setNewRate(int rate) {
	//..
}
```

## @PermitAll

The @PermitAll annotation specifies that all security roles are permitted to execute the specified method(s). The user is not checked against a database to ensure that this user is authorized to access this application.

This annotation can be specified on a class or on method(s). Specifying this annotation on the class means that it applies to all methods of the class. Specifying it at the method level means that it applies to only that method.

Here is some example code that demonstrates the use of the PermitAll annotation.

```java
import javax.annotation.security.*;
@RolesAllowed("RestrictedUsers")
public class Calculator {
	@RolesAllowed("Administrator")
	public void setNewRate(int rate) {
		//...
	}
	@PermitAll
	public long convertCurrency(long amount) {
		//...
	}
}
```

## @DenyAll

The @DenyAll annotation specifies that no security roles are permitted to execute the specified method(s). This means that these methods are excluded from execution in the Java EE container.

Here is some example code that demonstrates the use of the DenyAll annotation.

```java
import javax.annotation.security.*;
@RolesAllowed("Users")
public class Calculator {
	@RolesAllowed("Administrator")
	public void setNewRate(int rate) {
		//...
	}
	@DenyAll
	public long convertCurrency(long amount) {
		//...
	}
}
```
