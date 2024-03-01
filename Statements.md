# Statements

In Java, each statement is a complete unit of execution.

```java
int score = 9*5;
```

Here, we have a statement. The complete execution of this statement involves multiplying integers 9 and 5 and then assigning the result to the variable score.

## A Block Statement

A block is a group of statements (zero or more) that is enclosed in curly braces { }.

```java
class Main {
    public static void main(String[] args) {
    	
        String band = "Beatles";
    	
        if (band == "Beatles") { // start of block
            System.out.print("Hey ");
            System.out.print("Jude!");
        } // end of block
    }
}
```

## The if-else Statement

The if statement is Java’s conditional branch statement. It can be used to route program execution through two different paths. Here is the general form of the if statement:

  ***if (condition) statement1;***<br/>
  ***else statement2;***

Here, each statement may be a single statement, or a compound statement enclosed in curly braces (that is, a block). The condition is any expression that returns a boolean value. The else clause is optional. 

The if works like this: If the condition is true, then statement1 is executed. Otherwise, statement2 (if it exists) is executed.

```java
int a, b;
//...
if(a < b) a = 0;
else b = 0;
```

## The switch Statement

The switch statement is Java’s multiway branch statement. It provides an easy way to dispatch execution to different parts of your code based on the value of an expression. As such, it often provides a better alternative than a large series of if-else-if statements. Here is the general form of a switch statement:

***switch (expression) {***<br/>
***case value1:***<br/>
***// statement sequence***<br/>
***break;***<br/>
***case value2:***<br/>
***// statement sequence***<br/>
***break;***<br/>
***.***<br/>
***.***<br/>
***.***<br/>
***case valueN :***<br/>
***// statement sequence***<br/>
***break;***<br/>
***default:***<br/>
***// default statement sequence***<br/>
***}***

## The for Statement

Beginning with JDK 5, there are two forms of the for loop. The first is the traditional form that has been in use since the original version of Java. The second is the newer “for-each” form.

Both types of for loops are discussed here, beginning with the traditional form. Here is the general form of the traditional for statement:

  ***for (initialization; condition; iteration) {***<br/>
  ***// body***<br/>
  ***}***

### foreach

Unlike some languages, such as C#, that implement a for-each loop by using the keyword foreach, Java adds the for-each capability by enhancing the for statement. The advantage of this approach is that no new keyword is required, and no preexisting code is broken. The for-each style of for is also referred to as the enhanced for loop.

The general form of the for-each version of the for is shown here:

***for(type itr-var : collection) statement-block***

## The while Statement

The while loop is Java’s most fundamental loop statement. It repeats a statement or block while its controlling expression is true. Here is its general form:

***while(condition) {***<br/>
***// body of loop***<br/>
***}***

The condition can be any Boolean expression. The body of the loop will be executed if the conditional expression is true. When condition becomes false, control passes to the next line of code immediately following the loop. The curly braces are unnecessary if only a single statement is being repeated.

## The do-while Statement

The do-while loop always executes its body at least once, because its conditional expression is at the bottom of the loop. Its general form is:

***do {***<br/>
***// body of loop***<br/>
***} while (condition);***

## The break Statement

By using break, you can force immediate termination of a loop, bypassing the conditional expression and any remaining code in the body of the loop. When a break statement is encountered inside a loop, the loop is terminated, and program control resumes at the next statement following the loop. Here is a simple example:

```java
// Using break to exit a loop.
class BreakLoop {
    public static void main(String args[]) {
        for(int i=0; i<100; i++) {
            if(i == 10) break; // terminate loop if i is 10
            System.out.println("i: " + i);
        }
        System.out.println("Loop complete.");
    }
}
```

### Use break as a form of goto

Java does not have a goto statement because it provides a way to branch in an arbitrary and unstructured manner. This usually makes goto-ridden code hard to understand and hard to maintain. There are, however, a few places where the goto is a valuable and legitimate construct for flow control. For example, the goto can be useful when you are exiting from a deeply nested set of loops.

```java
// Using break as a civilized form of goto.
class Break {
    public static void main(String args[]) {
        boolean t = true;
        first: {
            second: {
                third: {
                    System.out.println("Before the break.");
                    if(t) break second; // break out of second block
                    System.out.println("This won't execute");
                }
                System.out.println("This won't execute");
            }
            System.out.println("This is after second block.");
        }
    }
}
```

## The continue Statement

Sometimes it is useful to force an early iteration of a loop. The continue statement performs such an action.

In while and do-while loops, a continue statement causes control to be transferred directly to the conditional expression that controls the loop.

In a for loop, control goes first to the iteration portion of the for statement and then to the conditional expression. For all three loops, any intermediate code is bypassed.

```java
// Demonstrate continue.
class Continue {
    public static void main(String args[]) {
        for(int i=0; i<10; i++) {
            System.out.print(i + " ");
            if (i%2 == 0) continue;
            System.out.println("");
        }
    }
}
```
