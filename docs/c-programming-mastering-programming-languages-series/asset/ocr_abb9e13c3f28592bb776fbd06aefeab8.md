```
```cpp
int age;        // Integer variable
double salary;   // Double-precision floating-point variable
char grade;      // Character variable
bool isStudent;  // Boolean variable
```
```

Understanding data types is crucial, as it dictates the range and precision of values a variable can hold. This foundational concept lays the groundwork for efficient data representation and manipulation.

# Functions and Modular Programming: Building Blocks of Reusable Code

In C++, functions are the building blocks of modular programming, allowing you to break down a program into manageable and reusable parts. Function declaration and definition in C++ follow a specific syntax.

```
```cpp
// Function declaration
int add(int a, int b);

// Function definition
int add(int a, int b) {
    return a + b;
}
```
```

Here, the add function takes two integer parameters (a and b) and returns their sum. Understanding functions facilitates code organization, enhances reusability, and promotes a modular programming approach.

# Conditional Statements: Controlling Program Flow

Conditional statements are essential for introducing decision-making capabilities to your programs. The if, else if, and else constructs control the flow of execution based on specified conditions.

```
```cpp
int num = 10;

if (num > 0) {
    // Code block executed if num is greater than 0
} else if (num < 0) {
    // Code block executed if num is less than 0
} else {
    // Code block executed if num is equal to 0
}
```
```