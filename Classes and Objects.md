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

## Using Dot Notation to Access Fields of a Class

##  Default Initialization of Fields

## Access Level Modifiers for a Class

## Import Declaration

## Declaring Methods of a Class

## Local Variables

## Instance Methods

## Class Methods

## Invoking a Method

## Access Level for Class Member
