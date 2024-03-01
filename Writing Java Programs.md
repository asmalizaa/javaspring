# Writing Java Programs

## Programming Paradigms

Programming paradigms refer to various ways or styles in which programs or programming languages can be organized. Each paradigm embodies specific structures, features, and opinions on how to tackle common programming problems. Let’s explore some of the most popular paradigms:

1. Imperative Programming:

   - **Description**: Imperative programming focuses on how to achieve a task by specifying a sequence of steps or commands.
   - **Example**: Traditional procedural languages like C or Pascal follow this paradigm.
   - **Key Characteristics**: Mutable state, explicit control flow, and step-by-step instructions.

3. Procedural Programming:
   
   - **Description**: Procedural programming is an extension of imperative programming. It organizes code into reusable procedures or functions.
   - **Example**: Languages like Fortran, COBOL, and early versions of BASIC.
   - **Key Characteristics**: Functions, procedures, and modular design.

4. Functional Programming:
   
   - **Description**: Functional programming treats computation as the evaluation of mathematical functions. It emphasizes immutability and avoids side effects.
   - **Example**: Languages like Haskell, Lisp, and Scala.
   - **Key Characteristics**: Pure functions, higher-order functions, and recursion.

5. Declarative Programming:
   
   - **Description**: Declarative programming focuses on what needs to be achieved rather than specifying how to achieve it. It describes the desired outcome.
   - **Example**: SQL for database queries, HTML for web page structure.
   - **Key Characteristics**: Expressive, concise, and declarative statements.

6. Object-Oriented Programming (OOP):
   
   - **Description**: OOP organizes code around objects, which encapsulate data and behavior. It promotes modularity and reusability.
   - **Example**: Java, C++, Python, and Ruby.
   - **Key Characteristics**: Classes, inheritance, encapsulation, and polymorphism.

Remember that programming paradigms are not mutually exclusive, and some languages support multiple paradigms. Choosing the right paradigm depends on the specific needs of your project and your personal preferences.

## What is Java?

Java is a versatile programming language and computing platform that has left an indelible mark on the digital landscape. Here’s what you need to know:

1. Origin and Evolution:
   - Java was first released by Sun Microsystems in 1995.
   - Over time, it has evolved into a powerful platform that underpins a significant portion of today’s digital world.
   - Many services, applications, and innovative products rely on Java’s reliable foundation.

2. Why Do You Need Java?:
   - Desktop Applications: While most modern Java applications combine the Java runtime and the application itself, some older applications and websites     still require desktop Java.
   - Java.com: This website caters to consumers who need Java for their desktop applications, specifically targeting Java 8.
   - Free to Download: Java is free for personal use, and developers can find development kits and other useful tools on Oracle’s Java download page.

3. Java Components:
   - Java Runtime Environment (JRE): When you download Java software from java.com, you get the JRE version 8. It includes:
     - Java Virtual Machine (JVM): Executes Java applications.
     - Core Java classes.
     - Supporting libraries.
   - Java Development Kit (JDK): For developers, the JDK provides additional tools beyond the JRE.

4. Java Plug-in:
   - The Java Plug-in is part of the JRE and allows certain Java applications to launch via web browsers.
   - It’s not a standalone program and cannot be installed separately.

5. Java Virtual Machine (JVM):
   - The JVM is a crucial part of Java software.
   - It helps run Java applications by interpreting bytecode.
   - When you download Java, the JVM is already included.

In summary, Java is a versatile language that runs on millions of devices and applications, including Android apps, web servers, and games. Whether you’re a developer or a user, understanding Java’s role is essential in today’s digital age!

## The Object-Oriented Paradigm and Java

Let’s delve into the Object-Oriented Paradigm and its relationship with Java.

1. What is Object-Oriented Paradigm?
   - The object-oriented programming (OOP) paradigm takes a unique approach to problem-solving. Instead of focusing directly on the problem at hand, it centers around the objects that constitute a system, server, or application.
   - These objects can be likened to real-world entities—think of a car or a dog. Each object has a state (attributes like name, color, brand) and behavior (actions like moving, slowing down, changing gears).
   - The primary goal of OOP is to represent the real world while writing code.

3. Features of the Object-Oriented Paradigm:
   - Entities (Objects): OOP breaks down a problem into a set of entities called objects. These objects encapsulate both data and functions.
   - Data-Centric Approach: OOP treats data as a critical element in program development. It restricts the flow of data and protects it from accidental modification by external functions.
   - Interaction Between Objects: Objects from different classes can easily interact through functions.
   - Bottom-Up Approach: OOP follows a bottom-up development process, building from individual objects to a complete system.

5. Comparison with Procedure-Oriented Approach:
   - Procedure-Oriented Programming (POP): In POP, the program is divided into small parts based on functions. Functions take precedence over data.
   - Object-Oriented Programming (OOP): In OOP, the program is divided into objects, which are instances of classes. Here, data is a critical element.
   - Security: OOP, due to abstraction and data hiding, is more secure than the procedure-oriented approach.

In summary, Java is an exclusively object-oriented language, and its success lies in embracing the principles of OOP. By modeling real-world concepts as objects, Java simplifies program design and enhances code readability.

## What is a Java Program

A Java program is a set of instructions written in the Java programming language. Let’s explore what makes Java programs unique:

1. Definition:
   - A Java program is a collection of code written in the Java language.
   - It consists of classes, methods, and other components that work together to achieve specific tasks.

3. Key Aspects of Java Programs:
   - Object-Oriented: Java is an object-oriented language, which means it revolves around the concept of objects. Objects represent real-world entities and encapsulate both data (attributes) and behavior (methods).
   - Platform Independence: Java programs can run on various platforms, including Windows, Mac, Linux, and even devices like the Raspberry Pi.
   - Versatility: Java is used for a wide range of applications:
     - Mobile Applications: Especially Android apps.
     - Desktop Applications: Creating software for desktop computers.
     - Web Applications: Building dynamic web pages and services.
     - Web Servers and Application Servers: Handling requests and serving web content.
     - Games: Developing interactive games.
     - Database Connectivity: Interacting with databases.
   - Security and Robustness: Java emphasizes security, and its robust features prevent common programming errors.
   - Community Support: With tens of millions of developers, Java has a huge community that provides assistance and resources.

5. Why Use Java?:
   - Popularity: Java is one of the most popular programming languages globally, running on over 3 billion devices.
   - Job Market Demand: Learning Java opens up numerous job opportunities.
   - Ease of Learning: Java’s syntax is straightforward, making it easy to learn.
   - Open-Source and Free: You can use Java without any licensing costs.
   - Clear Structure: OOP principles give Java programs a clear structure, promoting code reusability and maintainability.

In summary, a Java program combines code, objects, and logic to create powerful and versatile applications.

## Activity: Setup

1. JDK - Java Development Kit

   URL: https://www.oracle.com/java/technologies/downloads/
   
3. IDE - Eclipse

   URL: https://www.eclipse.org/downloads/

## Activity: Your First Java Program

In this activity, you are going to write your first Java program using Eclipse.

1. Launch eclipse.
2. Close the welcome page.
3. Create a new Java project via File > New > Java Project.

   ![image](https://github.com/asmalizaa/javaspring/assets/23090837/dd2a039a-ccca-43cd-b63b-a04c131a4918)

5. In the New Java Project wizard, enter below details.
   - Project name: HelloProject
   - Module: Unchecked
   - Leave everything else to default settings and click Finish to proceed.

     ![image](https://github.com/asmalizaa/javaspring/assets/23090837/004e915c-b5f6-40d3-bf56-d6923b4eb082)

6. Next is to create a new class. Right-click project > New > Class.

   ![image](https://github.com/asmalizaa/javaspring/assets/23090837/40c7c223-76c8-4795-a0a3-ef158ba1cc6a)

   Enter HelloProgram at Name field, then click Finish.

   ![image](https://github.com/asmalizaa/javaspring/assets/23090837/4c7c4451-bc55-4897-b448-1f278715e084)

7. Enter below codes in the HelloProgram class.

   ```java
   public class HelloProgram {
      public static void main(String[] args) {
         System.out.println("Hello World!");
      }
   }
   ```
   
8. To run the program, go to Run > Run.

   ![image](https://github.com/asmalizaa/javaspring/assets/23090837/4adb3f6e-bc05-4d25-8de7-15288b71c545)

9. The string “Hello World!” should be displayed in the console/output.

   ![image](https://github.com/asmalizaa/javaspring/assets/23090837/a42e7d9c-caeb-4f46-a8d3-8d973b24670c)



The end.
