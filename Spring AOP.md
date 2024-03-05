# Spring AOP

Reference: (https://docs.spring.io/spring-framework/reference/core/aop.html)

Aspect-oriented Programming (AOP) complements Object-oriented Programming (OOP) by providing another way of thinking about program structure. The key unit of modularity in OOP is the class, whereas in AOP the unit of modularity is the aspect. Aspects enable the modularization of concerns (such as transaction management) that cut across multiple types and objects. (Such concerns are often termed "crosscutting" concerns in AOP literature.)

One of the key components of Spring is the AOP framework. While the Spring IoC container does not depend on AOP (meaning you do not need to use AOP if you don’t want to), AOP complements Spring IoC to provide a very capable middleware solution.

AOP is used in the Spring Framework to:
- Provide declarative enterprise services. The most important such service is declarative transaction management.
- Let users implement custom aspects, complementing their use of OOP with AOP.

## AOP Concepts

- Aspect: A modularization of a concern that cuts across multiple classes. Transaction management is a good example of a crosscutting concern in enterprise Java applications. In Spring AOP, aspects are implemented by using regular classes (the schema-based approach) or regular classes annotated with the @Aspect annotation (the @AspectJ style).
- Join point: A point during the execution of a program, such as the execution of a method or the handling of an exception. In Spring AOP, a join point always represents a method execution.
- Advice: Action taken by an aspect at a particular join point. Different types of advice include "around", "before", and "after" advice. (Advice types are discussed later.) Many AOP frameworks, including Spring, model an advice as an interceptor and maintain a chain of interceptors around the join point.
- Pointcut: A predicate that matches join points. Advice is associated with a pointcut expression and runs at any join point matched by the pointcut (for example, the execution of a method with a certain name). The concept of join points as matched by pointcut expressions is central to AOP, and Spring uses the AspectJ pointcut expression language by default.
- Introduction: Declaring additional methods or fields on behalf of a type. Spring AOP lets you introduce new interfaces (and a corresponding implementation) to any advised object. For example, you could use an introduction to make a bean implement an IsModified interface, to simplify caching. (An introduction is known as an inter-type declaration in the AspectJ community.)
- Target object: An object being advised by one or more aspects. Also referred to as the "advised object". Since Spring AOP is implemented by using runtime proxies, this object is always a proxied object.
- AOP proxy: An object created by the AOP framework in order to implement the aspect contracts (advice method executions and so on). In the Spring Framework, an AOP proxy is a JDK dynamic proxy or a CGLIB proxy.
- Weaving: linking aspects with other application types or objects to create an advised object. This can be done at compile time (using the AspectJ compiler, for example), load time, or at runtime. Spring AOP, like other pure Java AOP frameworks, performs weaving at runtime.

Spring AOP includes the following types of advice:

- Before advice: Advice that runs before a join point but that does not have the ability to prevent execution flow proceeding to the join point (unless it throws an exception).
- After returning advice: Advice to be run after a join point completes normally (for example, if a method returns without throwing an exception).
- After throwing advice: Advice to be run if a method exits by throwing an exception.
- After (finally) advice: Advice to be run regardless of the means by which a join point exits (normal or exceptional return).
- Around advice: Advice that surrounds a join point such as a method invocation. This is the most powerful kind of advice. Around advice can perform custom behavior before and after the method invocation. It is also responsible for choosing whether to proceed to the join point or to shortcut the advised method execution by returning its own return value or throwing an exception.

## An AOP Example

Reference: (https://docs.spring.io/spring-framework/reference/core/aop/ataspectj/example.html)

Now that you have seen how all the constituent parts work, we can put them together to do something useful.

The execution of business services can sometimes fail due to concurrency issues (for example, a deadlock loser). If the operation is retried, it is likely to succeed on the next try. For business services where it is appropriate to retry in such conditions (idempotent operations that do not need to go back to the user for conflict resolution), we want to transparently retry the operation to avoid the client seeing a PessimisticLockingFailureException. This is a requirement that clearly cuts across multiple services in the service layer and, hence, is ideal for implementing through an aspect.

Because we want to retry the operation, we need to use around advice so that we can call proceed multiple times. The following listing shows the basic aspect implementation:

```java
@Aspect
public class ConcurrentOperationExecutor implements Ordered {

	private static final int DEFAULT_MAX_RETRIES = 2;

	private int maxRetries = DEFAULT_MAX_RETRIES;
	private int order = 1;

	public void setMaxRetries(int maxRetries) {
		this.maxRetries = maxRetries;
	}

	public int getOrder() {
		return this.order;
	}

	public void setOrder(int order) {
		this.order = order;
	}

	@Around("com.xyz.CommonPointcuts.businessService()")
	public Object doConcurrentOperation(ProceedingJoinPoint pjp) throws Throwable {
		int numAttempts = 0;
		PessimisticLockingFailureException lockFailureException;
		do {
			numAttempts++;
			try {
				return pjp.proceed();
			}
			catch(PessimisticLockingFailureException ex) {
				lockFailureException = ex;
			}
		} while(numAttempts <= this.maxRetries);
		throw lockFailureException;
	}
}
```

Note that the aspect implements the Ordered interface so that we can set the precedence of the aspect higher than the transaction advice (we want a fresh transaction each time we retry). The maxRetries and order properties are both configured by Spring. The main action happens in the doConcurrentOperation around advice. Notice that, for the moment, we apply the retry logic to each businessService. We try to proceed, and if we fail with a PessimisticLockingFailureException, we try again, unless we have exhausted all of our retry attempts.

The corresponding Spring configuration follows:

```java
<aop:aspectj-autoproxy/>

<bean id="concurrentOperationExecutor"
		class="com.xyz.service.impl.ConcurrentOperationExecutor">
	<property name="maxRetries" value="3"/>
	<property name="order" value="100"/>
</bean>
```

To refine the aspect so that it retries only idempotent operations, we might define the following Idempotent annotation:

```java
@Retention(RetentionPolicy.RUNTIME)
// marker annotation
public @interface Idempotent {
}
```

We can then use the annotation to annotate the implementation of service operations. The change to the aspect to retry only idempotent operations involves refining the pointcut expression so that only @Idempotent operations match, as follows:

```java
@Around("execution(* com.xyz..service.*.*(..)) && " +
		"@annotation(com.xyz.service.Idempotent)")
public Object doConcurrentOperation(ProceedingJoinPoint pjp) throws Throwable {
	// ...
}
```
