# Java Elements Quick Reference

## Table of Contents
- [Variables and Data Types](#variables-and-data-types)
- [Operators](#operators)
- [Control Structures](#control-structures)
- [Arrays](#arrays)
- [Methods](#methods)
- [String Operations](#string-operations)

## Variables and Data Types
```java
// Primitive Data Types
int number = 42;                  // Integer values
double decimal = 3.14;            // Decimal numbers
boolean flag = true;              // true or false
char letter = 'A';                // Single character
byte smallNumber = 127;           // 8-bit integer
short mediumNumber = 32767;       // 16-bit integer
long bigNumber = 123456789L;      // 64-bit integer
float floatNumber = 3.14f;        // 32-bit floating point

// Reference Data Types
String text = "Hello Java!";      // String object
Integer wrappedInt = 42;          // Integer wrapper class
Double wrappedDouble = 3.14;      // Double wrapper class

// Constants
final double PI = 3.14159;        // Constant value
final String COMPANY = "Tech";    // Constant string

// Variable declaration patterns
int a, b, c;                      // Multiple declarations
int x = 1, y = 2;                // Multiple initializations
```

## Operators
```java
// Arithmetic Operators
int sum = 5 + 3;                 // Addition
int difference = 10 - 4;         // Subtraction
int product = 4 * 2;             // Multiplication
int quotient = 15 / 3;           // Division
int remainder = 7 % 3;           // Modulus

// Compound Assignment
int number = 10;
number += 5;                     // Add and assign
number -= 3;                     // Subtract and assign
number *= 2;                     // Multiply and assign
number /= 4;                     // Divide and assign

// Comparison Operators
boolean isEqual = (5 == 5);      // Equal to
boolean notEqual = (5 != 3);     // Not equal to
boolean greater = (7 > 3);       // Greater than
boolean less = (4 < 8);          // Less than
boolean greaterEqual = (5 >= 5); // Greater than or equal
boolean lessEqual = (4 <= 4);    // Less than or equal

// Logical Operators
boolean and = true && false;     // Logical AND
boolean or = true || false;      // Logical OR
boolean not = !true;             // Logical NOT

// Increment/Decrement
int count = 0;
count++;                         // Post-increment
++count;                         // Pre-increment
count--;                         // Post-decrement
--count;                         // Pre-decrement
```

## Control Structures
```java
// If-Else Statements
if (score >= 90) {
    System.out.println("A grade");
} else if (score >= 80) {
    System.out.println("B grade");
} else {
    System.out.println("Below B");
}

// Switch Statement
switch (day) {
    case 1:                      // Case with break
        System.out.println("Monday");
        break;
    case 2:                      // Fall-through case
        System.out.println("Tuesday");
        // falls through
    default:
        System.out.println("Other day");
}

// While Loop
int i = 0;
while (i < 5) {                 // Loop with condition
    System.out.println(i);
    i++;
}

// Do-While Loop
do {                           // Executes at least once
    System.out.println(i);
    i--;
} while (i > 0);

// For Loop
for (int j = 0; j < 5; j++) {  // Standard for loop
    System.out.println(j);
}

// Enhanced For Loop
int[] numbers = {1, 2, 3, 4, 5};
for (int num : numbers) {       // For-each loop
    System.out.println(num);
}
```

## Arrays
```java
// Array Declaration and Initialization
int[] numbers = new int[5];     // Fixed-size array
int[] values = {1, 2, 3, 4, 5}; // Array literal
String[] names = new String[3];  // Array of strings

// Multi-dimensional Arrays
int[][] matrix = new int[3][3];  // 2D array
int[][] grid = {                 // 2D array literal
    {1, 2, 3},
    {4, 5, 6},
    {7, 8, 9}
};

// Array Operations
numbers[0] = 10;                // Setting element
int value = numbers[0];         // Getting element
int length = numbers.length;    // Array length

// Array Copying
int[] copy = numbers.clone();   // Full array copy
int[] partial = Arrays.copyOf(numbers, 3);  // Partial copy
```

## Methods
```java
// Basic Method
public void printMessage() {
    System.out.println("Hello!");
}

// Method with Parameters
public int add(int a, int b) {
    return a + b;
}

// Method with Multiple Returns
public String getGrade(int score) {
    if (score >= 90) return "A";
    if (score >= 80) return "B";
    return "C";
}

// Method Overloading
public void display(int number) {
    System.out.println("Number: " + number);
}

public void display(String text) {
    System.out.println("Text: " + text);
}

// Varargs Method
public int sum(int... numbers) {
    int total = 0;
    for (int num : numbers) {
        total += num;
    }
    return total;
}
```

## String Operations
```java
// String Creation
String str1 = "Hello";          // String literal
String str2 = new String("Hi"); // String object

// String Methods
String text = "Hello World";
int length = text.length();     // String length
char first = text.charAt(0);    // Get character
String sub = text.substring(0, 5); // Substring
String upper = text.toUpperCase(); // Convert case
String lower = text.toLowerCase(); // Convert case

// String Comparison
boolean equals = str1.equals(str2);     // Content comparison
boolean ignoreCase = str1.equalsIgnoreCase(str2);
int compare = str1.compareTo(str2);     // Lexicographic comparison

// String Manipulation
String concat = str1 + " " + str2;      // Concatenation
String joined = String.join("-", "a", "b"); // Joining
String replaced = text.replace("l", "L");   // Replace
String[] split = text.split(" ");          // Split

// StringBuilder (Mutable Strings)
StringBuilder builder = new StringBuilder();
builder.append("Hello");        // Add text
builder.append(" World");       // Add more text
String result = builder.toString(); // Convert to String
```
