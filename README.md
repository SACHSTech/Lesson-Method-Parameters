# Methods with Parameters

So far, the methods we have written always did the same thing every time they were called. If we wanted slightly different behaviour, we would have needed separate methods or repeated code.

To make methods more flexible, we use **parameters**. A parameter allows us to send a **value** into a method so the method can *use* that value when it runs.

For example, we may want to draw a line of stars:

```
*****
```

But how long should the line be? 

3? 10? 50?

Without parameters, we might end up writing many nearly identical methods:

```java
private void drawLine3() {
    System.out.println("***");
}

private void drawLine8() {
    System.out.println("********");
}

private void drawLine12() {
    System.out.println("************");
}
```

This is still repetitive.

Instead, we can write one method using a **parameter**:

```java
private void drawLine(int length) {
    for (int i = 0; i < length; i++) {
        System.out.print("*");
    }
    System.out.println();
}
```

Now we can call the method with any value we choose:

```java
drawLine(5);   // *****
drawLine(10);  // **********
drawLine(3);   // ***
```

## What Is a Parameter?

A **parameter** is a variable listed inside the method parentheses. It receives a value when the method is called.

In the example below:

```java
private void drawLine(int length)
```

- `int` is the **data type** the method expects
- `length` is the **parameter variable** that will store the value passed in

When we call the method with:

```java
drawLine(8);
```

- `8` is the **argument** (the actual value sent into the method)
- and inside the method, `length` becomes `8` for that call

You can think of a parameter as a blank that must be filled in:

```
drawLine( ___ );
```

## Parameter Types Must Match

If a method says it expects an `int`, you must pass an `int`.

```java
drawLine("ten"); // incorrect
```

This results in a compiler error because `"ten"` is a `String`, not an `int`.

```
error: method drawLine in class Main cannot be applied to given types
```

The fix is to pass an `int`:

```java
drawLine(10);
```

## Using Variables as Arguments

We often take user input and pass it into methods as arguments.

For example:

```java
public void run() {
    int width = readInt("How wide should the line be? ");
    drawLine(width);
}
```

If the variable type matches the expected parameter type, the call is valid. Here, `width` is an `int`, which matches the parameter type in `drawLine(int length)`.

However, since user input can be unpredictable, it is good practice to **validate** or **clean up** the input before using it.

### Checking for Edge Cases

When we use parameters, Java expects the value type to match exactly — but the *meaning* of the value is up to us to check.  

For example, a negative width doesn’t make sense for a line.

We can prevent invalid input by adding a simple check:

```java
public void run() {
    int width = readInt("How wide should the line be? ");

    if (width <= 0) {
        System.out.println("Width must be a positive number.");
    } else {
        drawLine(width);
    }
}
```

This ensures the method is only called with valid input.

### Cleaning Up Text Input

When working with `String` parameters, we may want to clean or adjust user input before passing it to a method.  

For example, trimming spaces or converting to a consistent case:

```java
public void run() {
    String name = readLine("Enter your name: ");
    name = name.trim();  // string method that removes extra spaces
    greet(name);
}

private void greet(String person) {
    System.out.println("Hello, " + person + "!");
}
```

This prevents unexpected spacing or formatting issues in output.

### Example: Controlling Repetition

Parameters can also control how many times something happens:

```java
private void printWordNTimes(String word, int count) {
    for (int i = 0; i < count; i++) {
        System.out.println(word);
    }
}
```

And we can combine this with user input and validation:

```java
public void run() {
    String word = readLine("Enter a word: ");
    int times = readInt("How many times? ");

    if (times <= 0) {
        System.out.println("Please enter a positive number.");
    } else {
        printWordNTimes(word, times);
    }
}
```

This not only introduces flexible methods but also models **safe programming habits** — checking values before using them.

## Scaling Up: One Parameter Box

Let us start with a **fixed width** box, but allow the **height** to change.

```
+----------+
|          |
|          |
|          |
+----------+
```

```java
private void drawBox(int height) {
    drawBorder();
    for (int i = 0; i < height - 2; i++) {
        drawSide();
    }
    drawBorder();
}

private void drawBorder() {
    System.out.println("+----------+");
}

private void drawSide() {
    System.out.println("|          |");
}
```

Calling it:

```java
drawBox(4);
drawBox(8);
```

This shows how changing one parameter affects the output.

## Multiple Parameters

Once we are comfortable with one parameter, we can add a second one to generalize width as well:

```
+--------+
|        |
|        |
+--------+
```

```java
private void drawBox(int width, int height) {
    drawBorder(width);
    for (int i = 0; i < height - 2; i++) {
        drawSide(width);
    }
    drawBorder(width);
}

private void drawBorder(int width) {
    System.out.print("+");
    for (int i = 0; i < width - 2; i++) {
        System.out.print("-");
    }
    System.out.println("+");
}

private void drawSide(int width) {
    System.out.print("|");
    for (int i = 0; i < width - 2; i++) {
        System.out.print(" ");
    }
    System.out.println("|");
}
```

Calling it:

```java
drawBox(12, 5);
drawBox(20, 10);
```

This version can now draw boxes of any size.

## A More Complex Example: Math Operations

Parameters can be used to pass numbers, strings, or other data to methods that perform logic.

```java
private void printSum(int a, int b) {
    int total = a + b;
    System.out.println("The sum is " + total);
}
```

Call it:

```java
printSum(4, 7);
printSum(10, 25);
```

You can also mix parameters of different data types:

```java
private void describePerson(String name, int age) {
    System.out.println(name + " is " + age + " years old.");
}
```

Call it:

```java
describePerson("Alex", 15);
describePerson("Sam", 17);
```

Soon, we will write methods that not only receive values but also **produce and return** values. Before that, we must be confident sending values *into* methods. 

The following practice problems focus only on methods with parameteres.


<br>

## Practice Problems
Each problem increases in difficulty. Try to reason about what the method does and how to use parameters effectively. Be sure to test with different arguments!

<br>

### Problem 1 — Repeat a Word
Write a method that prints the same word a given number of times on separate lines.

```java
public class Problem1 extends ConsoleProgram {
    public void run() {
        echo("Java", 3);
        echo("Code", 2);
    }

    private void echo(String word, int times) {
        // TODO
    }
}
```

**Expected Output:**
```
Java
Java
Java
Code
Code
```

<br>

### Problem 2 — Draw a Line of Characters
Write a method that prints a line made up of a character repeated `n` times.

```java
public class Problem2 extends ConsoleProgram {
    public void run() {
        drawLine('*', 5);
        drawLine('-', 10);
    }

    private void drawLine(char symbol, int length) {
        // TODO
    }
}
```

**Expected Output:**
```
*****
----------
```
<br>

### Problem 3 — Personalized Greeting
Write a method that prints a greeting to a person, repeated as many times as you specify.

```java
public class Problem3 extends ConsoleProgram {
    public void run() {
        greet("Alice", 2);
        greet("Bob", 4);
    }

    private void greet(String name, int times) {
        // TODO
    }
}
```

**Expected Output:**
```
Hello, Alice!
Hello, Alice!
Hello, Bob!
Hello, Bob!
Hello, Bob!
Hello, Bob!
```
<br>

### Problem 4 — Only Evens
Write a method that prints all even numbers up to a given number.

```java
public class Problem4 extends ConsoleProgram {
    public void run() {
        printEvensUpTo(10);
    }

    private void printEvensUpTo(int max) {
        // TODO
    }
}
```

**Expected Output:**
```
2 4 6 8 10
```

<br>

### Problem 5 — Triangle of Symbols
Write a method that prints a right triangle made of any symbol.

```java
public class Problem5 extends ConsoleProgram {
    public void run() {
        drawTriangle('#', 4);
    }

    private void drawTriangle(char symbol, int height) {
        // TODO
    }
}
```

**Expected Output:**
```
#
##
###
####
```
<br>

### Problem 6 — Centered Pyramid
Write a method that prints a centered pyramid of `*` characters.  
The pyramid’s height should come from a parameter.  
Each row should be centered relative to the bottom.

```java
public class Problem6 extends ConsoleProgram {
    public void run() {
        drawPyramid(5);
    }

    private void drawPyramid(int height) {
        // TODO
    }
}
```

**Expected Output:**
```
    *
   ***
  *****
 *******
*********
```

<br>

### Problem 7 — Word Triangle
Write a method that prints a word as a triangle, one more character per line.

```java
public class Problem7 extends ConsoleProgram {
    public void run() {
        wordTriangle("CODE");
    }

    private void wordTriangle(String word) {
        // TODO
    }
}
```

**Expected Output:**
```
C
CO
COD
CODE
```
<br>

### Problem 8 — Safe Divider
Write a method that divides one number by another, but checks for division by zero first.

```java
public class Problem8 extends ConsoleProgram {
    public void run() {
        safeDivide(10, 2);
        safeDivide(10, 0);
    }

    private void safeDivide(int a, int b) {
        // TODO
    }
}
```

**Expected Output:**
```
Result: 5
Error: cannot divide by zero.
```

<br>

### Problem 9 — Number Pattern
Write a method that takes two integers: a **start** and an **end**.  
It prints all numbers from start to end inclusive.  
If `start` is greater than `end`, print them in reverse order.

```java
public class Problem9 extends ConsoleProgram {
    public void run() {
        printRange(3, 7);
        printRange(10, 6);
    }

    private void printRange(int start, int end) {
        // TODO
    }
}
```

**Expected Output:**
```
3 4 5 6 7
10 9 8 7 6
```

<br>

### Problem 10 — Grade Bar Graph (Challenge)
Write a method that prints a small bar graph for scores, right-aligning names and truncating long ones.  
Each bar should be a line of `#` characters equal to the score divided by 10.

```java
public class Problem10 extends ConsoleProgram {
    public void run() {
        drawBar("Alexander", 95);
        drawBar("Bo", 60);
        drawBar("Catherine", 30);
        drawBar("LongNameDude", 50);
    }

    private void drawBar(String name, int score) {
        // TODO
    }
}
```

**Expected Output:**
```
 Alexander: #########
        Bo: ######
 Catherine: ###
LongNameDu: #####
```
