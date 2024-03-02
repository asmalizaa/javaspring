# The Object and Object Class

Java is an object-oriented programming language. The core concept of the object-oriented approach is to break complex problems into smaller objects.

An object is any entity that has a state and behavior. For example, a bicycle is an object. It has

- **States**: idle, first gear, etc
- **Behaviors**: braking, accelerating, etc.

## The Object Class

- Object class is present in java.lang package.
- Every class in Java is directly or indirectly derived from the Object class.
- If a class does not extend any other class then it is a direct child class of Object and if extends another class then it is indirectly derived.
- Therefore the Object class methods are available to all Java classes. Hence Object class acts as a root of the inheritance hierarchy in any Java Program.

The Object class provides multiple methods which are as follows:

- tostring() method
- hashCode() method
- equals(Object obj) method
- finalize() method
- getClass() method
- clone() method
- wait(), notify() notifyAll() methods

## What is the Class of an Object

In Java, classes and objects are basic concepts of Object Oriented Programming (OOPs) that are used to represent real-world concepts and entities. The class represents a group of objects having similar properties and behavior.

A class in Java is a set of objects which shares common characteristics/ behavior and common properties/ attributes. It is a user-defined blueprint or prototype from which objects are created.

For example, the animal type Dog is a class while a particular dog named Tommy is an object of the Dog class.

### Properties of Java Classes

1. Class is not a real-world entity. It is just a template or blueprint or prototype from which objects are created.
2. Class does not occupy memory.
3. Class is a group of variables of different data types and a group of methods.
4. A Class in Java can contain:
   - Data member
   - Method
   - Constructor
   - Nested Class
   - Interface

```java
package com.example.domain;

public class Rectangle {
	private double width;
	private double height;

	public Rectangle() {
		this.width = 5;
		this.height = 5;
	}

	public double getArea() {
		return this.width * this.height;
	}

	public double getPerimeter() {
		return (2 * this.height) + (2 * this.width);
	}

	@Override
	public String toString() {
		return "Rectangle of width=" + this.width + " and height=" + this.height + " has an area=" + this.getArea()
				+ " and perimeter=" + this.getPerimeter();
	}
}
```

## Computing Hash Code of an Object

## Comparing Objects for Equality

## String Representation of an Object

## Cloning an Object

## Finalizing an Object

## Immutable Object
