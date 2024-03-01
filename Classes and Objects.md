# Classes and Objects

## What is a Class

- Class defines a new data type.
- Once defined, this new type can be used to create objects of that type.
- Thus, a class is a template for an object, and an object is an instance of a class.
- A class is declared by use of the class keyword.
- The data, or variables, defined within a class are called instance variables.
- The code is contained within methods.
- Collectively, the methods and variables defined within a class are called members of the class.

  ![image](https://github.com/asmalizaa/javaspring/assets/23090837/6fb0f89c-867a-473f-97d5-39e452aaf630)

## Declaring Fields in a Class

Fields in a class also known as attributes of properties that describes the object of the class.

Here is a class called Box that defines three instance variables: width, height, and depth. Currently, Box does not contain any methods.

```java
class Box {
    double width;
    double height;
    double depth;
}
```

## Creating Instances of a Class

Object is an instance of a class. To create instance(s) of a class, just use the **new** keyword and call the constructor.

```java
// This program declares two Box objects.
class BoxDemo2 {
    public static void main(String args[]) {
        Box mybox1 = new Box();
        Box mybox2 = new Box();
        double vol;

        // assign values to mybox1's instance variables
        mybox1.width = 10;
        mybox1.height = 20;
        mybox1.depth = 15;

        /* assign different values to mybox2's instance variables */
        mybox2.width = 3;
        mybox2.height = 6;
        mybox2.depth = 9;

        // compute volume of first box
        vol = mybox1.width * mybox1.height * mybox1.depth;
        System.out.println("Volume is " + vol);

        // compute volume of second box
        vol = mybox2.width * mybox2.height * mybox2.depth;
        System.out.println("Volume is " + vol);
    }
}
```

## The null Reference Type

In Java, this word is a reserved word for literal values. It seems like a keyword, but actually, it is a literal similar to true and false.

This word is used as a default value for the uninitialized variable of reference types like Object or user-defined class. It will not be used as a default variable for any variable of primitive types, like, int and float.

Typecasting null to any reference type is fine at both compile-time and runtime. It will not throw any error or exception. The same is shown in the code snippet below.

```java
public class CastingNull {
    public static void main(String[] args) {
        String myStr = (String) null; // null can be type cast to String
        Integer myItr = (Integer) null; // it can also be type casted to Integer
        Double myDbl = (Double) null; // yes it's possible, no error
        System.out.println("Printing null casted to String");
        System.out.println(myStr);
        System.out.println("Printing null casted to Integer");
        System.out.println(myItr);
        System.out.println("Printing null casted to Double");
        System.out.println(myDbl);
    }
}
```

## Using Dot Notation to Access Fields of a Class

In Java language, the dot operator (.) symbolizes the element or operator that works over the syntax. It is often known as a separator, dot, and period.

Simply, the dot operator acts as an access provider for objects and classes. The usage of the above operator is as below.

```java
System.out.println("Width of rectOne: "  + rectOne.width);
System.out.println("Height of rectOne: " + rectOne.height);
```

##  Default Initialization of Fields

All fields of a class, static as well as non-static, are initialized to a default value.

The default value of a field depends on its data type.

  - A numeric field ( byte, short, char, int, long, float, and double) is initialized to zero.
  - A boolean field is initialized to false.
  - A reference type field is initialized to null.

## Access Level Modifiers for a Class

- Access level modifiers determine whether other classes can use a particular field or invoke a particular method.
- There are two levels of access control:
  - At the top level - public, or package-private (no explicit modifier).
  - At the member level - public, private, protected, or package-private (no explicit modifier).
- A class may be declared with the modifier public, in which case that class is visible to all classes everywhere.
- If a class has no modifier (the default, also known as package-private), it is visible only within its own package.
- At the member level, you can also use the public modifier or no modifier (package-private) just as with top-level classes, and with the same meaning.
- For members, there are two additional access modifiers: private and protected.
- The private modifier specifies that the member can only be accessed in its own class.
- The protected modifier specifies that the member can only be accessed within its own package (as with package-private) and, in addition, by a subclass of its class in another package.

<table>
  <tr><th>Modifier</th><th>Class</th><th>Package</th><th>Subclass</th><th>World</th></tr>
  <tr><td>public</td><td>Y</td><td>Y</td><td>Y</td><td>Y</td></tr>
  <tr><td>protected</td><td>Y</td><td>Y</td><td>Y</td><td>N</td></tr>
  <tr><td>default</td><td>Y</td><td>Y</td><td>N</td><td>N</td></tr>
  <tr><td>private</td><td>Y</td><td>N</td><td>N</td><td>N</td></tr>
</table>

### Tips on Choosing an Access Level

- If other programmers use your class, you want to ensure that errors from misuse cannot happen.
- Access levels can help you do this.
  - Use the most restrictive access level that makes sense for a particular member. Use private unless you have a good reason not to.
  - Avoid public fields except for constants.

## Import Declaration

## Declaring Methods of a Class

## Local Variables

## Instance Methods

## Class Methods

## Invoking a Method

## Access Level for Class Member
