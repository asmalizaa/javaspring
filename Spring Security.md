# Spring Security

Reference: (https://spring.io/projects/spring-security)

Spring Security is a powerful and highly customizable authentication and access-control framework. It is the de-facto standard for securing Spring-based applications.

Spring Security is a framework that focuses on providing both authentication and authorization to Java applications. Like all Spring projects, the real power of Spring Security is found in how easily it can be extended to meet custom requirements

Spring Security framework adds two important capabilities to web applications.
1. Authentication
2. Authorization

This framework provides protection against popular security issues like SCRF attacks, or Fixation attacks. It provides a secure and standard way to set up user login functionality in web applications and thus provides quick user authentication and access control.

![image](https://github.com/asmalizaa/javaspring/assets/23090837/df6e3118-7667-4e58-b2a9-3b134a32994f)

To read more on Spring Security Architecture, go [here](https://spring.io/guides/topicals/spring-security-architecture)

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

## Activity 1: Securing a Web Application

Reference: (https://spring.io/guides/gs/securing-web)

**Thymeleaf 3.1 no longer provides access to HttpServletRequest so HttpServletRequest#getRemoteUser() cannot be used to access the currently authenticated user.**

### Starting with Spring Initializr

Use Spring Initializr to create a new project with below settings.
   - Project: Maven
   - Language: Java
   - Spring Boot: default
   - Group: com.example
   - Artifact: secureweb
   - Name: secureweb
   - Description: Demo project for Spring Data JPA
   - Package name: com.example.secureweb
   - Packaging: Jar
   - Java: 21
   - Dependencies: Spring Web, Thymeleaf, Spring Boot Developers
   
   Generate/download, extract and import project into eclipse.

### Create an Unsecured Web Application

Before you can apply security to a web application, you need a web application to secure. This section walks you through creating a simple web application. Then you will secure it with Spring Security in the next section.

The web application includes two simple views: a home page and a “Hello, World” page. The home page is defined in the following Thymeleaf template (from src/main/resources/templates/home.html)

```html
<!DOCTYPE html>
<html xmlns="http://www.w3.org/1999/xhtml" xmlns:th="https://www.thymeleaf.org">
    <head>
        <title>Spring Security Example</title>
    </head>
    <body>
        <h1>Welcome!</h1>
        <p>Click <a th:href="@{/hello}">here</a> to see a greeting.</p>
    </body>
</html>
```

This simple view includes a link to the /hello page, which is defined in the following Thymeleaf template (from src/main/resources/templates/hello.html)

```html
<!DOCTYPE html>
<html xmlns="http://www.w3.org/1999/xhtml" xmlns:th="https://www.thymeleaf.org">
    <head>
        <title>Hello World!</title>
    </head>
    <body>
        <h1>Hello world!</h1>
    </body>
</html>
```

The web application is based on Spring MVC. As a result, you need to configure Spring MVC and set up view controllers to expose these templates. The following listing (from src/main/java/com/example/securingweb/MvcConfig.java) shows a class that configures Spring MVC in the application.

```java
package com.example.securingweb;

import org.springframework.context.annotation.Configuration;
import org.springframework.web.servlet.config.annotation.ViewControllerRegistry;
import org.springframework.web.servlet.config.annotation.WebMvcConfigurer;

@Configuration
public class MvcConfig implements WebMvcConfigurer {

	public void addViewControllers(ViewControllerRegistry registry) {
		registry.addViewController("/home").setViewName("home");
		registry.addViewController("/").setViewName("home");
		registry.addViewController("/hello").setViewName("hello");
		registry.addViewController("/login").setViewName("login");
	}

}
```

The addViewControllers() method (which overrides the method of the same name in WebMvcConfigurer) adds four view controllers. Two of the view controllers reference the view whose name is home (defined in home.html), and another references the view named hello (defined in hello.html). The fourth view controller references another view named login. You will create that view in the next section.

At this point, you could jump ahead to "Run the Application" and run the application without having to log in to anything.

Now that you have an unsecured web application, you can add security to it.

### Set up Spring Security

Suppose that you want to prevent unauthorized users from viewing the greeting page at /hello. As it is now, if visitors click the link on the home page, they see the greeting with no barriers to stop them. You need to add a barrier that forces the visitor to sign in before they can see that page.

You do that by configuring Spring Security in the application. If Spring Security is on the classpath, Spring Boot automatically secures all HTTP endpoints with "basic" authentication. However, you can further customize the security settings. The first thing you need to do is add Spring Security to the classpath.

With Maven, you need to add two extra entries (one for the application and one for testing) to the <dependencies> element in pom.xml, as the following listing shows.

```xml
<dependency>
	<groupId>org.springframework.boot</groupId>
	<artifactId>spring-boot-starter-security</artifactId>
</dependency>
<dependency>
	<groupId>org.thymeleaf.extras</groupId>
	<artifactId>thymeleaf-extras-springsecurity6</artifactId>
	<!-- Temporary explicit version to fix Thymeleaf bug -->
	<version>3.1.1.RELEASE</version>
</dependency>
<dependency>
	<groupId>org.springframework.security</groupId>
	<artifactId>spring-security-test</artifactId>
	<scope>test</scope>
</dependency>
```

The following security configuration (from src/main/java/com/example/securingweb/WebSecurityConfig.java) ensures that only authenticated users can see the secret greeting.

```java
package com.example.securingweb;

import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.security.config.annotation.web.builders.HttpSecurity;
import org.springframework.security.config.annotation.web.configuration.EnableWebSecurity;
import org.springframework.security.core.userdetails.User;
import org.springframework.security.core.userdetails.UserDetails;
import org.springframework.security.core.userdetails.UserDetailsService;
import org.springframework.security.provisioning.InMemoryUserDetailsManager;
import org.springframework.security.web.SecurityFilterChain;

@Configuration
@EnableWebSecurity
public class WebSecurityConfig {

	@Bean
	public SecurityFilterChain securityFilterChain(HttpSecurity http) throws Exception {
		http
			.authorizeHttpRequests((requests) -> requests
				.requestMatchers("/", "/home").permitAll()
				.anyRequest().authenticated()
			)
			.formLogin((form) -> form
				.loginPage("/login")
				.permitAll()
			)
			.logout((logout) -> logout.permitAll());

		return http.build();
	}

	@Bean
	public UserDetailsService userDetailsService() {
		UserDetails user =
			 User.withDefaultPasswordEncoder()
				.username("user")
				.password("password")
				.roles("USER")
				.build();

		return new InMemoryUserDetailsManager(user);
	}
}
```

The WebSecurityConfig class is annotated with @EnableWebSecurity to enable Spring Security’s web security support and provide the Spring MVC integration. It also exposes two beans to set some specifics for the web security configuration:

The SecurityFilterChain bean defines which URL paths should be secured and which should not. Specifically, the / and /home paths are configured to not require any authentication. All other paths must be authenticated.

When a user successfully logs in, they are redirected to the previously requested page that required authentication. There is a custom /login page (which is specified by loginPage()), and everyone is allowed to view it.

The UserDetailsService bean sets up an in-memory user store with a single user. That user is given a user name of user, a password of password, and a role of USER.

Now you need to create the login page. There is already a view controller for the login view, so you need only to create the login view itself, as the following listing (from src/main/resources/templates/login.html) shows.

```html
<!DOCTYPE html>
<html xmlns="http://www.w3.org/1999/xhtml" xmlns:th="https://www.thymeleaf.org">
    <head>
        <title>Spring Security Example </title>
    </head>
    <body>
        <div th:if="${param.error}">
            Invalid username and password.
        </div>
        <div th:if="${param.logout}">
            You have been logged out.
        </div>
        <form th:action="@{/login}" method="post">
            <div><label> User Name : <input type="text" name="username"/> </label></div>
            <div><label> Password: <input type="password" name="password"/> </label></div>
            <div><input type="submit" value="Sign In"/></div>
        </form>
    </body>
</html>
```

This Thymeleaf template presents a form that captures a username and password and posts them to /login. As configured, Spring Security provides a filter that intercepts that request and authenticates the user. If the user fails to authenticate, the page is redirected to /login?error, and your page displays the appropriate error message. Upon successfully signing out, your application is sent to /login?logout, and your page displays the appropriate success message.

Last, you need to provide the visitor a way to display the current user name and sign out. To do so, update the hello.html to say hello to the current user and contain a Sign Out form, as the following listing (from src/main/resources/templates/hello.html) shows

```html
<!DOCTYPE html>
<html xmlns="http://www.w3.org/1999/xhtml" xmlns:th="https://www.thymeleaf.org"
      xmlns:sec="https://www.thymeleaf.org/thymeleaf-extras-springsecurity6">
    <head>
        <title>Hello World!</title>
    </head>
    <body>
        <h1 th:inline="text">Hello <span th:remove="tag" sec:authentication="name">thymeleaf</span>!</h1>
        <form th:action="@{/logout}" method="post">
            <input type="submit" value="Sign Out"/>
        </form>
    </body>
</html>
```

We display the username by using Thymeleaf’s integration with Spring Security. The “Sign Out” form submits a POST to /logout. Upon successfully logging out, it redirects the user to /login?logout.

### Run the Application

Once the application starts up, point your browser to http://localhost:8080. You should see the home page, as the following image shows.

![image](https://github.com/asmalizaa/javaspring/assets/23090837/ca5061b3-7bcf-4480-bc66-c85c22ac8255)

When you click on the link, it attempts to take you to the greeting page at /hello. However, because that page is secured and you have not yet logged in, it takes you to the login page, as the following image shows.

![image](https://github.com/asmalizaa/javaspring/assets/23090837/97bcdb42-996a-44b0-a836-779dd25b5175)

At the login page, sign in as the test user by entering user and password for the username and password fields, respectively. Once you submit the login form, you are authenticated and then taken to the greeting page, as the following image shows.

![image](https://github.com/asmalizaa/javaspring/assets/23090837/2dfd8d52-8c37-445e-b22a-b292a77bc7d0)

If you click on the Sign Out button, your authentication is revoked, and you are returned to the login page with a message indicating that you are logged out.

Congratulations! You have developed a simple web application that is secured with Spring Security.

Additional reading [How to do user authentication in Spring Boot using PostgreSQL database?](https://fullstackdeveloper.guru/2020/06/05/how-to-do-user-authentication-in-spring-boot-using-postgresql-database/comment-page-1/)
