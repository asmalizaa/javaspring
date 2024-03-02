# Java Package

- Packages are containers for classes.
- Packages are used to keep the class name space compartmentalized.
- Packages are stored in a hierarchical manner and are explicitly imported into new class definitions.
- The package is both a naming and a visibility control mechanism.
- Define classes inside a package that are not accessible by code outside that package.
- Define class members that are exposed only to other members of the same package.

## The Purpose of Package

- Preventing naming conflicts. For example there can be two classes with name Employee in two packages, college.staff.cse.Employee and college.staff.ee.Employee
- Making searching/locating and usage of classes, interfaces, enumerations and annotations easier.
- Providing controlled access: protected and default have package level access control. A protected member is accessible by classes in the same package and its subclasses. A default member (without any access specifier) is accessible by classes in the same package only.
- Packages can be considered as data encapsulation (or data-hiding).

## Package Declaration

- Every file can only have 1 package statement.
- Package declaration must always be the first line in the file.
- The package declaration syntax:
      ***package <top_package_name>.<sub_package_name>;***
  
## Sub-Packages in Java

Packages that are inside another package are the subpackages. These are not imported by default, they have to imported explicitly. Also, members of a subpackage have no access privileges, i.e., they are considered as different package for protected and default access specifiers.

```java
import java.util.*;
```

util is a subpackage created inside java package.  

## Naming Convention

- Package names are written in all lower case to avoid conflict with the names of classes or interfaces.
- Companies use their reversed Internet domain name to begin their package names—for example, com.example.mypackage for a package named mypackage created by a programmer at example.com.
- Name collisions that occur within a single company need to be handled by convention within that company, perhaps by including the region or the project name after the company name (for example, com.example.region.mypackage).
- Packages in the Java language itself begin with java. or javax.
- In some cases, the internet domain name may not be a valid package name. This can occur if the domain name contains a hyphen or other special character, if the package name begins with a digit or other character that is illegal to use as the beginning of a Java name, or if the package name contains a reserved Java keyword, such as "int". In this event, the suggested convention is to add an underscore. For example;

<table>
    <tr><th>Domain Name</th><th>Package Name Prefix</th></tr>
    <tr><td>hyphenated-name.example.org</td><td>org.example.hyphenated_name</td></tr>
    <tr><td>example.int</td><td>int_.example</td></tr>
    <tr><td>123name.example.com</td><td>com.example._123name</td></tr>
</table>

## Importing Java Package

Java has an import statement that allows you to import an entire package (as in earlier examples), or use only certain classes and interfaces defined in the package.

The general form of import statement is:

```java
import package.name.ClassName;   // To import a certain class only
import package.name.*   // To import the whole package
```

For example;

```java
import java.util.Date; // imports only Date class
import java.io.*;      // imports everything inside java.io package
```

The import statement is optional in Java.

If you want to use class/interface from a certain package, you can also use its fully qualified name, which includes its full package hierarchy.

Here is an example to import a package using the import statement.

```java
import java.util.Date;

class MyClass implements Date {
    // body
}
```

## Java Archive (JAR) Files

A JAR (Java Archive) is a package file format typically used to aggregate many Java class files and associated metadata and resources (text, images, etc.) into one file to distribute application software or libraries on the Java platform. 

In simple words, a JAR file is a file that contains a compressed version of .class files, audio files, image files, or directories. We can imagine a .jar file as a zipped file(.zip) that is created by using WinZip software. Even, WinZip software can be used to extract the contents of a .jar . So you can use them for tasks such as lossless data compression, archiving, decompression, and archive unpacking. 
