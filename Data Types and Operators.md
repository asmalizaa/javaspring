# Data Types and Operators

- Java is strongly types language.
- Every variable, expression has a type, and every type is strictly defined.
- All assignments, whether expliciti or via parameter passing in method calls, are checked for type compatibility.
- No automatic coercions or conversions of conflicting types as in some languages.
- The Java compiler checks all expressions and parameters to ensure that the types are compatible.
- Any type mismatches are errors that must be corrected before the compiler will finish compiling the class.
  
## Data Types

Java defines eight primitive data types: byte, short, int, long, char, float, double, and boolean.

<table>
  <tr><th>Group</th><th>Description</th></tr>
  <tr><td>Integers</td><td>This group includes byte, short, int, and long, which are for whole-valued signed numbers.</td></tr>
  <tr><td>Float-point</td><td>This group includes float and double, which represent numbers with fractional precision.</td></tr>
  <tr><td>Characters</td><td>This group includes char, which represents symbols in a character set, like letters and numbers.</td></tr>
  <tr><td>Boolean</td><td>This group includes boolean, which is a special type for representing true/false values.</td></tr>
</table>

### Integers

Java defines four integer types: byte, short, int, and long. All of these are signed, positive, and negative values. Java does not support unsigned, positive-only integers.

<table>
  <tr><th>Name</th><th>Width</th><th>Range</th></tr>
  <tr><td>long</td><td>64</td><td>–9,223,372,036,854,775,808 to 9,223,372,036,854,775,807</td></tr>
  <tr><td>int</td><td>32<td>–2,147,483,648 to 2,147,483,647</td></tr>
  <tr><td>short</td><td>16<td>–32,768 to 32,767</td></tr>
  <tr><td>byte</td><td>8<td>–128 to 127</td></tr>
</table>

### Floating points

Floating-point numbers, also known as real numbers, are used when evaluating expressions that require fractional precision. For example, calculations such as square root, or transcendentals such as sine and cosine, result in a value whose precision requires a floating-point type.

<table>
  <tr><th>Name</th><th>Width</th><th>Range</th></tr>
  <tr><td>double</td><td>64</td><td>4.9e–324 to 1.8e+308</td></tr>
  <tr><td>float</td><td>32<td>1.4e–045 to 3.4e+038</td></tr>
</table>

### Characters

In Java, the data type used to store characters is char. At the time of Java's creation, Unicode required 16 bits. Thus, in Java char is a 16-bit type. The range of a char is 0 to 65,536. There are no negative chars. The standard set of characters known as ASCII still ranges from 0 to 127 as always, and the extended 8-bit character set, ISO-Latin-1, ranges from 0 to 255.

### Boolean

Java has a primitive type, called boolean, for logical values. It can have only one of two possible values, true or false.

## Identifier

  - All Java variables must be identified with unique names.
  - These unique names are called identifiers.
  - Identifiers can be short names (like x and y) or more descriptive names (age, sum, totalVolume).

The general rules for naming variables are:

  - Names can contain letters, digits, underscores, and dollar signs.
  - Names must begin with a letter.
  - Names should start with a lowercase letter, and cannot contain whitespace.
  - Names can also begin with $ and _ (but we will not use it in this tutorial).
  - Names are case-sensitive ("myVar" and "myvar" are different variables).
  - Reserved words (like Java keywords, such as int or boolean) cannot be used as names.

## Strings

  - Java’s string type, called String, is not a primitive type.
  - It is in fact a class.
  - When you declare a variable of type String, you basically creating an object.
  - String class is immutable.
  - When you create a String object, you are creating a string that cannot be changed. That is, once a String object has been created, you cannot change the characters that comprise that string.
  - Each time you need an altered version of an existing string, a new String object is created that contains the modifications. The original string is left unchanged.

There are two ways to declare a string variables.

```java
// literals
String name = "John Smith";

// constructor
String email = new String("john@example.com");
```

The length of a string is the number of characters that it contains. To obtain this value, call the length( ) method.

```java
char chars[] = { 'a', 'b', 'c' };
String s = new String(chars);
System.out.println(s.length());
```

### String concatenation.

  - In general, Java does not allow operators to be applied to String objects.
  - The one exception to this rule is the + operator, which concatenates two strings, producing a String object as the result.

```java
String age = "9";
String s = "He is " + age + " years old.";
System.out.println(s);
```
## Arrays

  - An array is a group of like-typed variables that are referred to by a common name.
  - Array of any type (primitive or class) can be created and may have one or more dimensions.
  - A specific element in an array is accessed by its index.
  - Arrays offer a convenient means of grouping related information.
  - In Java, an array is an object.
  - Array is a fixed size list of values.
  - When declaring an array, the size must be supplied.

### One-Dimensional Array

  - A one-dimensional array is, essentially, a list of like-typed variables.
  - Syntax to declare a one-dimensional array.

    ***type array-var = new type [size];***

    ```java
    int month_days = new int[12];
    ```
  - To access and display array element, use the index.

    ```java
    System.out.println(month_days[3]);
    ```

### Multidimensional Array

  - In Java, multidimensional arrays are actually arrays of arrays.
  - To declare a multidimensional array variable, specify each additional index using another set of square brackets.

    ```java
    int twoD[][] = new int[4][5];
    ```
  - This allocates a 4 by 5 array and assigns it to twoD.
  - Internally, this matrix is implemented as an array of arrays of int.

    ![image](https://github.com/asmalizaa/javaspring/assets/23090837/8e432d02-b76d-4400-b84a-1dee80d1865c)

### Jagged Array

  - When you allocate memory for a multidimensional array, you need only specify the memory for the first (leftmost) dimension.
  - You can allocate the remaining dimensions separately.

    ```java
    int twoD[][] = new int[4][];
    twoD[0] = new int[1];
    twoD[1] = new int[2];
    twoD[2] = new int[3];
    twoD[3] = new int[4];
    ```
    The array created by this program looks like this:

    ![image](https://github.com/asmalizaa/javaspring/assets/23090837/3233df0c-3218-41c4-b325-bc2ccba4eeef)

### Using the length member

  - All array indices in Java begin at 0.
  - The number of elements in an array is stored as part of the array object in the length attribute.
  - If an out-of-bounds runtime access occurs, then a runtime exception is thrown.

    ```java
    int[] arr = new int[5];  
    int arrayLength = arr.length; 
    ```

    ![image](https://github.com/asmalizaa/javaspring/assets/23090837/5fd3ea97-0d5f-4a05-9e66-7b6711843802)

## Operator

## Assignment Operator

## Arithmetic Operators

## String Concatenation Operator

## Relational Operators

## Boolean Operators
