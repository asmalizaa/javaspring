# Wrapper Classes

- A Wrapper class in Java is a class whose object wraps or contains primitive data types.
- When we create an object to a wrapper class, it contains a field and in this field, we can store primitive data types.
- In other words, we can wrap a primitive value into a wrapper class object. 

## Need of Wrapper Classes

There are certain needs for using the Wrapper class in Java as mentioned below:

1. They convert primitive data types into objects. Objects are needed if we wish to modify the arguments passed into a method (because primitive types are passed by value).
2. The classes in java.util package handles only objects and hence wrapper classes help in this case also.
3. Data structures in the Collection framework, such as ArrayList and Vector, store only objects (reference types) and not primitive types.
4. An object is needed to support synchronization in multithreading.

## Advantages of Wrapper Classes

1. Collections allowed only object data.
2. On object data we can call multiple methods compareTo(), equals(), toString()
3. Cloning process only objects.
4. Object data allowed null values.
5. Serialization can allow only object data.

## Primitive Data Types and their Correspondinng Wrapper Classes

<table>
  <tr><th>Primitive Data Type</th><th>Wrapper Class</th></tr>
  <tr><td>char</td><td>Character</td></tr>
  <tr><td>byte</td><td>Byte</td></tr>
  <tr><td>short</td><td>Short</td></tr>
  <tr><td>int</td><td>Integer</td></tr>
  <tr><td>long</td><td>Long</td></tr>
  <tr><td>float</td><td>Float</td></tr>
  <tr><td>double</td><td>Double</td></tr>
  <tr><td>boolean</td><td>Boolean</td></tr>
</table>

## Autoboxing and Autounboxinng

The automatic conversion of primitive types to the object of their corresponding wrapper classes is known as autoboxing. For example – conversion of int to Integer, long to Long, double to Double, etc. 

```java
// Java program to demonstrate Autoboxing

import java.util.ArrayList;

class Autoboxing {
	public static void main(String[] args) {
		char ch = 'a';

		// Autoboxing- primitive to Character object conversion
		Character a = ch;

		ArrayList<Integer> arrayList = new ArrayList<Integer>();

		// Autoboxing because ArrayList stores only objects
		arrayList.add(25);

		// printing the values from object
		System.out.println(arrayList.get(0));
	}
}
```

It is just the reverse process of autoboxing. Automatically converting an object of a wrapper class to its corresponding primitive type is known as unboxing. For example – conversion of Integer to int, Long to long, Double to double, etc. 

```java
// Java program to demonstrate Unboxing
import java.util.ArrayList;

class Unboxing {
	public static void main(String[] args) {
		Character ch = 'a';

		// unboxing - Character object to primitive conversion 
		char a = ch;

		ArrayList<Integer> arrayList = new ArrayList<Integer>();
		arrayList.add(24);

		// unboxing because get method returns an Integer object
		int num = arrayList.get(0);

		// printing the values from primitive data types
		System.out.println(num);
	}
}
```

## Dates and Times

Java does not have a built-in Date class, but we can import the java.time package to work with the date and time API. The package includes many date and time classes. For example:

<table>
	<tr><th>Class</th><th>Description</th></tr>
	<tr><td>LocalDate</td><td>Represents a date (year, month, day (yyyy-MM-dd))</td></tr>
	<tr><td>LocalTime</td><td>Represents a time (hour, minute, second and nanoseconds (HH-mm-ss-ns))</td></tr>
	<tr><td>LocalDateTime</td><td>Represents both a date and a time (yyyy-MM-dd-HH-mm-ss-ns)</td></tr>
	<tr><td>DateTimeFormatter</td><td>Formatter for displaying and parsing date-time objects</td></tr>
</table>

### Display Current Date

To display the current date, import the java.time.LocalDate class, and use its now() method:

```java
import java.time.LocalDate; // import the LocalDate class

public class Main {
	public static void main(String[] args) {
		LocalDate myObj = LocalDate.now(); // Create a date object
		System.out.println(myObj); // Display the current date
	}
}
```
### Display Current Time

To display the current time (hour, minute, second, and nanoseconds), import the java.time.LocalTime class, and use its now() method:

```java
import java.time.LocalTime; // import the LocalTime class

public class Main {
	public static void main(String[] args) {
		LocalTime myObj = LocalTime.now();
		System.out.println(myObj);
  	}
}
```

### Display Current Date and Time

To display the current date and time, import the java.time.LocalDateTime class, and use its now() method:

```java
import java.time.LocalDateTime; // import the LocalDateTime class

public class Main {
  	public static void main(String[] args) {
    	LocalDateTime myObj = LocalDateTime.now();
    	System.out.println(myObj);
  	}
}
```

### Formatting Date and Time

The "T" in the example above is used to separate the date from the time. You can use the DateTimeFormatter class with the ofPattern() method in the same package to format or parse date-time objects. The following example will remove both the "T" and nanoseconds from the date-time:

```java
import java.time.LocalDateTime; // Import the LocalDateTime class
import java.time.format.DateTimeFormatter; // Import the DateTimeFormatter class

public class Main {
  	public static void main(String[] args) {
    	LocalDateTime myDateObj = LocalDateTime.now();
    	System.out.println("Before formatting: " + myDateObj);
    	DateTimeFormatter myFormatObj = DateTimeFormatter.ofPattern("dd-MM-yyyy HH:mm:ss");

    	String formattedDate = myDateObj.format(myFormatObj);
    	System.out.println("After formatting: " + formattedDate);
  	}
}
```

## Collections

The Java platform includes a collections framework. A collection is an object that represents a group of objects. A collection framework is a unified architecture for representing and manipulating collections, enabling collections to be manipulated independently of implementation details.

- Objects in a collection are called elements.
- The Collections API relies heavily on generics for its implementation.
- The Collections classes are all stored in the java.util package.

  ![image](https://github.com/asmalizaa/javaspring/assets/23090837/3ceced38-596a-418a-8a54-968879a38ec9)

The diagram in the slide shows the Collection framework. The framework is made up of a set of interfaces for working with a group (collection) of objects. 

### Collection Interfaces and Implementation

<table>
	<tr><th>Interface</th><th>Implementation</th></tr>
	<tr><td>List</td><td>ArrayList, LinkedList</td></tr>
	<tr><td>Set</td><td>TreeSet, HashSet, LinkedHashSet</td></tr>
	<tr><td>Map</td><td>HashMap, HashTable, TreeMap</td></tr>
	<tr><td>Deque</td><td>ArrayDeque</td></tr>
</table>

### List Interface

- List defines generic list behaviour.
  - Is an ordered collection of elements.
- List behaviours include
  - Adding elements at a specific index.
  - Getting an element based on an index.
  - Removing an element based on an index.
  - Overwriting an element based on an index.
  - Getting the size of the list.
- List allows duplicate elements.


### ArrayList

- Is an implementation of the List interface.
  - The list automatically grows if elements exceed initial size.
- Has numeric index.
  - Elements are accessed by index.
  - Elements can be inserted based on index.
  - Elements can be overwritten.
- Allows duplicate items.

```java
import java.util.ArrayList;
import java.util.List;

public class ListExample {

	public static void main(String[] args) {

		// create the list (empty)
		List<Integer> list = new ArrayList<>();

		// add elements into list
		list.add(1);
		list.add(200);
		list.add(78);
		list.add(45);
		list.add(55);
		System.out.println("List: " + list);

		// get the size
		System.out.println("Size: " + list.size());

		// retrieve element
		System.out.println("First: " + list.get(0));

		// loop and get total
		int total = 0;
		for (int i : list) {
			total += i;
		}
		System.out.println("Total: " + total);

		// add by index
		list.add(0, 999);
		System.out.println("List: " + list);
		System.out.println("Size: " + list.size());

		// add duplicate
		list.add(999);
		System.out.println("List: " + list);
		System.out.println("Size: " + list.size());
		
		// overwrite element
		list.set(0, 45);
		System.out.println("List: " + list);
		System.out.println("Size: " + list.size());
		
		// delete element
		list.remove(0);
		System.out.println("List: " + list);
		System.out.println("Size: " + list.size());
	}

}
```

### Set Interface

- A Set in an interface that contains only unique elements.
- A Set has no index.
- Duplicate elements are not allowed.
- You can iterate through elements to access them.
- TreeSet provides sorted implementation.

```java
import java.util.HashSet;
import java.util.Set;
import java.util.TreeSet;

public class SetExample {

	public static void main(String[] args) {

		// create a treeset object (sorted)
		Set<String> set = new TreeSet<>();

		// add elements to set
		set.add("john");
		set.add("bob");
		set.add("sarah");
		set.add("wanda");
		System.out.println("TreeSet: " + set);

		// create a hashset object (not sorted)
		set = new HashSet<>();

		// add elements to set
		set.add("john");
		set.add("bob");
		set.add("sarah");
		set.add("wanda");
		System.out.println("HashSet: " + set);
		
		// add duplicate
		set.add("john");
		System.out.println("HashSet: " + set);
		
		// delete element
		set.remove("john");
		System.out.println("HashSet: " + set);
	}

}
```

### Map Interface

- A collection that stores multiple key-value pairs.
  - Key: unique identifier for each element in a collection.
  - Value: a value stored in the element associated with the key.
- Called “associative arrays” in other language.

  ![image](https://github.com/asmalizaa/javaspring/assets/23090837/f54c4e15-5fe9-4870-8052-72dc15cc2ba8)

The Map interface does not extend the Collection interface because it represents mappings and not a collection of objects. Some of the key implementation classes includes:
- TreeMap: a map where keys are automatically sorted.
- Hashtable: a classic associative array implementation with keys and values. Hashtable is synchronized.
- HashMap: an implementation just like Hashtable except that it accepts null keys and values. Also, it is not synchronized.

```java
import java.util.Collection;
import java.util.HashMap;
import java.util.Map;
import java.util.Set;
import java.util.TreeMap;

public class MapExample {

	public static void main(String[] args) {

		// use treemap (sorted)
		Map<String, String> map = new TreeMap<>();

		// add elements to map
		map.put("S001", "Blue Polo Shirt");
		map.put("S002", "Black Polo Shirt");
		map.put("H001", "Duke Hat");
		System.out.println("TreeMap: " + map);

		// use hashmap(not sorted)
		map = new HashMap<>();

		// add elements to map
		map.put("S001", "Blue Polo Shirt");
		map.put("S002", "Black Polo Shirt");
		map.put("H001", "Duke Hat");
		System.out.println("HashMap: " + map);

		// key must be unique - this will overwrite existing value
		map.put("S002", "Black T-Shirt");
		System.out.println("HashMap: " + map);

		map.replace("S002", "Blue T-Shirt"); // overwrite existing value
		System.out.println("HashMap: " + map);

		map.replace("H002", "Blue Hat"); // nothing happened
		System.out.println("HashMap: " + map);

		map.put("H002", "Blue Hat"); // added
		System.out.println("HashMap: " + map);

		// retrieve 1 value
		System.out.println("Value: " + map.get("H002"));

		// delete value by key
		map.remove("H002");
		System.out.println("HashMap: " + map);

		// get all keys
		Set<String> keys = map.keySet();
		System.out.println("Keys: " + keys);

		// get all values
		Collection<String> values = map.values();
		System.out.println("Values: " + values);

		// get all pairs
		Set<Map.Entry<String, String>> entries = map.entrySet();
		System.out.println("Entries: " + entries);

		// iterate map
		System.out.println("===Entries===");
		for (String key : keys) {
			System.out.println(key + " => " + map.get(key));
		}

	}

}
```
