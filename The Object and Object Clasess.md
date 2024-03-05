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

Constructors are used for initializing new objects. Fields are variables that provide the state of the class and its objects, and methods are used to implement the behavior of the class and its objects.

```java
public class Rectangle {

	private int width;
	private int height;

	public Rectangle() {
		System.out.println("Default rectangle created: width = 25, height = 10");
		width = 25;
		height = 10;
	}

	public Rectangle(int w, int h) {
		if (w > 0 && w < 30 && h > 0 && h < 30) {
			width = w;
			height = h;
			System.out.println("A rectangle is created: width = " + width + ", height = " + height);
		} else {
			System.out.println("Out of range. Width and height must be between 0 and 30.");
		}
	}

	public int getArea() {
		return height * width;
	}

	public void draw() {
		for (int i = 0; i < height; i++) {
			for (int j = 0; j < width; j++) {
				System.out.print("*");
			}
			System.out.println();
		}
	}
}
```

## Computing Hash Code of an Object

The hash code value is an integer value associated with each object. It is used to identify the location of objects in the hash table.

```java
class Main {
  public static void main(String[] args) {

    // hashCode() with Object
    Object obj1 = new Object();
    System.out.println(obj1.hashCode());  // 1785210046

    Object obj2 = new Object();
    System.out.println(obj2.hashCode());  // 1552787810

    Object obj3 = new Object();
    System.out.println(obj3.hashCode());  // 1361960727
  }
}
```

## Comparing Objects for Equality

You can use equals() method from Object class to compare objects. Although equals() method can be used to compare the values of two strings, it is not really useful by default to compare two objects without overriding it.

```java
// Java Program to Compare Two Objects

import java.io.*;

class Pet {
	String name;
	int age;
	String breed;

	Pet(String name, int age, String breed)
	{
		this.name = name;
		this.age = age;
		this.breed = breed;
	}
	@Override public boolean equals(Object obj)
	{

		// checking if the two objects
		// pointing to same object
		if (this == obj)
			return true;

		// checking for two condition:
		// 1) object is pointing to null
		// 2) if the objects belong to
		// same class or not
		if (obj == null
			|| this.getClass() != obj.getClass())
			return false;

		Pet p1 = (Pet)obj; // type casting object to the
						// intended class type

		// checking if the two 
		// objects share all the same values
		return this.name.equals(p1.name)
			&& this.age == p1.age
			&& this.breed.equals(p1.breed);
	}
}

public class GFG {
	public static void main(String args[])
	{

		Pet dog1 = new Pet("Snow", 3, "German Shepherd");
		Pet cat = new Pet("Jack", 2, "Tabby");
		Pet dog2 = new Pet("Snow", 3, "German Shepherd");
		System.out.println(dog1.equals(dog2));
	}
}
```

## String Representation of an Object

Now we will be dealing with one of its methods known as toString() method. We typically generally do use the toString() method to get the string representation of an object. It is very important and readers should be aware that whenever we try to print the object reference then internally toString() method is invoked. If we did not define the toString() method in your class then the Object class toString() method is invoked otherwise our implemented or overridden toString() method will be called.

```java
// Java Program to print string representation of object
public class Box {

	// instance variables
	// default access modifier - accessible within the package only
	private double width;
	private double height;
	private double depth;
	private String name;

	public Box() {
		System.out.println("Box constructor executed...");
		width = 10;
		height = 10;
		depth = 10;
		name = "box";
		updateCounter();
	}

	public double calculateVolume() {
		// calculate volume for box
		return width * height * depth;
	}

	@Override
	public String toString() {
		return "== Box Details ==\n" + "Name = " + name + "\n" + "Width = " + width + "\n" + "Height = " + height + "\n"
				+ "Depth = " + depth + "\n" + "Volume = " + calculateVolume() + "\n";
	}
}
```

## Cloning an Object

Object cloning refers to the creation of an exact copy of an object. It creates a new instance of the class of the current object and initializes all its fields with exactly the contents of the corresponding fields of this object.

There are 3 methods for creating Object Cloning in Java that are mentioned below:

1. Using Assignment Operator to create a copy of the reference variable.
2. Creating a copy using the clone() method.
3. Usage of clone() method – Deep Copy.

### Example 1: Using Assignment Operator to create a copy of the reference variable

In Java, there is no operator to create a copy of an object. Unlike C++, in Java, if we use the assignment operator then it will create a copy of the reference variable and not the object. This can be explained by taking an example. The following program demonstrates the same.

```java
// Java program to demonstrate that assignment operator 
// only creates a new reference to same object 
import java.io.*; 

// A test class whose objects are cloned 
class Test { 
	int x, y; 
	Test() 
	{ 
		x = 10; 
		y = 20; 
	} 
} 

// Driver Class 
class Main { 
	public static void main(String[] args) { 
		Test ob1 = new Test(); 
		System.out.println(ob1.x + " " + ob1.y); 

		// Creating a new reference variable ob2  pointing to same address as ob1 
		Test ob2 = ob1; 

		// Any change made in ob2 will be reflected in ob1 
		ob2.x = 100; 

		System.out.println(ob1.x + " " + ob1.y); 
		System.out.println(ob2.x + " " + ob2.y); 
	} 
}
```

### Example 2: Creating a copy using the clone() method - Shallow Copy

The class whose object’s copy is to be made must have a public clone method in it or in one of its parent classes.  

- Every class that implements clone() should call super.clone() to obtain the cloned object reference.
- The class must also implement java.lang.Cloneable interface whose object clone we want to create otherwise it will throw CloneNotSupportedException when the clone method is called on that class’s object.

In the below code example the clone() method does create a completely new object with a different hashCode value, which means its in a separate memory location. But due to the Test object c being inside Test2, the primitive types have achieved deep copy but this Test object c is still shared between t1 and t2. To overcome that we explicitly do a deep copy for object variable c, which is discussed later. 

```java
// A Java program to demonstrate 
// shallow copy using clone() 
import java.util.ArrayList; 

// An object reference of this class is 
// contained by Test2 
class Test { 
	int x, y; 
} 

// Contains a reference of Test and 
// implements clone with shallow copy. 
class Test2 implements Cloneable { 
	int a; 
	int b; 
	Test c = new Test(); 
	public Object clone() throws CloneNotSupportedException 
	{ 
		return super.clone(); 
	} 
} 

// Driver class 
public class Main { 
	public static void main(String args[]) throws CloneNotSupportedException { 
		Test2 t1 = new Test2(); 
		t1.a = 10; 
		t1.b = 20; 
		t1.c.x = 30; 
		t1.c.y = 40; 

		Test2 t2 = (Test2)t1.clone(); 

		// Creating a copy of object t1 and passing it to t2 
		t2.a = 100; 

		// Change in primitive type of t2 will not be reflected in t1 field 
		t2.c.x = 300; 

		// Change in object type field will be reflected in both t2 and t1(shallow copy) 
		System.out.println(t1.a + " " + t1.b + " " + t1.c.x + " " + t1.c.y); 
		System.out.println(t2.a + " " + t2.b + " " + t2.c.x + " " + t2.c.y); 
	} 
}
```

### Example 3: Creating a copy using the clone() method - Deep Copy

- If we want to create a deep copy of object X and place it in a new object Y then a new copy of any referenced objects fields are created and these references are placed in object Y. This means any changes made in referenced object fields in object X or Y will be reflected only in that object and not in the other. In the below example, we create a deep copy of the object.
- A deep copy copies all fields and makes copies of dynamically allocated memory pointed to by the fields. A deep copy occurs when an object is copied along with the objects to which it refers.

```java
// A Java program to demonstrate 
// deep copy using clone() 

// An object reference of this 
// class is contained by Test2 
class Test { 
	int x, y; 
} 

// Contains a reference of Test and 
// implements clone with deep copy. 
class Test2 implements Cloneable { 
	int a, b; 

	Test c = new Test(); 

	public Object clone() throws CloneNotSupportedException 
	{ 
		// Assign the shallow copy to 
		// new reference variable t 
		Test2 t = (Test2)super.clone(); 

		// Creating a deep copy for c 
		t.c = new Test(); 
		t.c.x = c.x; 
		t.c.y = c.y; 

		// Create a new object for the field c 
		// and assign it to shallow copy obtained, 
		// to make it a deep copy 
		return t; 
	} 
} 

public class Main { 
	public static void main(String args[]) throws CloneNotSupportedException { 
		Test2 t1 = new Test2(); 
		t1.a = 10; 
		t1.b = 20; 
		t1.c.x = 30; 
		t1.c.y = 40; 

		Test2 t3 = (Test2)t1.clone(); 
		t3.a = 100; 

		// Change in primitive type of t2 will not be reflected in t1 field 
		t3.c.x = 300; 

		// Change in object type field of t2 will not be reflected in t1(deep copy) 
		System.out.println(t1.a + " " + t1.b + " " + t1.c.x + " " + t1.c.y); 
		System.out.println(t3.a + " " + t3.b + " " + t3.c.x + " " + t3.c.y); 
	} 
}
```

### Deep Copy vs Shallow Copy

There are certain differences between using clone() as a deep copy vs that as a shallow copy as mentioned below:

- Shallow copy is the method of copying an object and is followed by default in cloning. In this method, the fields of an old object X are copied to the new object Y. While copying the object type field the reference is copied to Y i.e object Y will point to the same location as pointed out by X. If the field value is a primitive type it copies the value of the primitive type.
- Therefore, any changes made in referenced objects in object X or Y will be reflected in other objects.
- Shallow copies are cheap and simple to make. In the above example, we created a shallow copy of the object.

## Finalizing an Object

The finalize() method is called the finalizer.

Finalizers get invoked when JVM figures out that this particular instance should be garbage collected. Such a finalizer may perform any operations, including bringing the object back to life.

The main purpose of a finalizer is, however, to release resources used by objects before they’re removed from the memory. A finalizer can work as the primary mechanism for clean-up operations, or as a safety net when other methods fail.

To understand how a finalizer works, let’s take a look at a class declaration:

```java
public class Finalizable {
    private BufferedReader reader;

    public Finalizable() {
        InputStream input = this.getClass()
          .getClassLoader()
          .getResourceAsStream("file.txt");
        this.reader = new BufferedReader(new InputStreamReader(input));
    }

    public String readFirstLine() throws IOException {
        String firstLine = reader.readLine();
        return firstLine;
    }

    // other class members
}
```

The class Finalizable has a field reader, which references a closeable resource. When an object is created from this class, it constructs a new BufferedReader instance reading from a file in the classpath.

Such an instance is used in the readFirstLine method to extract the first line in the given file. Notice that the reader isn’t closed in the given code.

We can do that using a finalizer:

```java
@Override
public void finalize() {
    try {
        reader.close();
        System.out.println("Closed BufferedReader in the finalizer");
    } catch (IOException e) {
        // ...
    }
}
```

It’s easy to see that a finalizer is declared just like any normal instance method.

In reality, **the time at which the garbage collector calls finalizers is dependent on the JVM’s implementation and the system’s conditions, which are out of our control.**

To make garbage collection happen on the spot, we’ll take advantage of the System.gc method. In real-world systems, we should never invoke that explicitly, for a number of reasons:

1. It’s costly.
2. It doesn’t trigger the garbage collection immediately – it’s just a hint for the JVM to start GC.
3. JVM knows better when GC needs to be called.

## Immutable Object

An immutable object is an **object whose internal state remains constant after it has been entirely created.**

This means that the public API of an immutable object guarantees us that it will behave in the same way during its whole lifetime.

If we take a look at the class String, we can see that even when its API seems to provide us a mutable behavior with its replace method, the original String doesn’t change:

```java
String name = "baeldung";
String newName = name.replace("dung", "----");

assertEquals("baeldung", name);
assertEquals("bael----", newName);
```

In Java, variables are mutable by default, meaning we can change the value they hold.

By using the final keyword when declaring a variable, the Java compiler won’t let us change the value of that variable. Instead, it will report a compile-time error:

```java
final String name = "baeldung";
name = "bael...";
```
