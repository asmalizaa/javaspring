# Spring Security

Reference: (https://spring.io/projects/spring-security)

Spring Security is a powerful and highly customizable authentication and access-control framework. It is the de-facto standard for securing Spring-based applications.

Spring Security is a framework that focuses on providing both authentication and authorization to Java applications. Like all Spring projects, the real power of Spring Security is found in how easily it can be extended to meet custom requirements

Spring Security framework adds two important capabilities to web applications.
1. Authentication
2. Authorization

This framework provides protection against popular security issues like SCRF attacks, or Fixation attacks. It provides a secure and standard way to set up user login functionality in web applications and thus provides quick user authentication and access control.

![image](https://github.com/asmalizaa/javaspring/assets/23090837/df6e3118-7667-4e58-b2a9-3b134a32994f)

## Authentication

Authentication is the process of verifying the identity of the computer user. It is the process of verifying the user and devices before allowing them to access the resources. The main strategy interface for authentication is AuthenticationManager, which has only one method.

```java
public interface AuthenticationManager {
    Authentication authenticate(Authentication authentication) throws AuthenticationException;
}
```

An AuthenticationManager can do one of 3 things in its authenticate() method:
- Return an Authentication (normally with authenticated=true) if it can verify that the input represents a valid principal.
- Throw an AuthenticationException if it believes that the input represents an invalid principal.
- Return null if it cannot decide.

AuthenticationException is a runtime exception. It is usually handled by an application in a generic way, depending on the style or purpose of the application. In other words, user code is not normally expected to catch and handle it. For example, a web UI might render a page that says that the authentication failed, and a backend HTTP service might send a 401 response, with or without a WWW-Authenticate header depending on the context.

## Authorization

When a user or a device is authenticated, the next step is authorization which is the process of allowing the authority to perform certain tasks or operations. In Java, AccessDecisionManager and AccessDecsionVoter classes help in the authorization process. 

## Activity: Securing a Web Application

Reference: (https://spring.io/guides/gs/securing-web)

