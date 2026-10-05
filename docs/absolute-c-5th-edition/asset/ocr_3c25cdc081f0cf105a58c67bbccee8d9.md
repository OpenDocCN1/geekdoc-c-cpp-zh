# Self-Test Exercises (continued)

+   6. What is the output of the following program lines when they are embedded in a correct program that declares number to be of type int?

number = (1/3) * 3;
cout << "1/3" * 3 is equal to " << number;

+   7. Write a C++ program that reads two numbers into two variables of type int and outputs both the whole number and the remainder when the first number is divided by the second. This can be done using the operators / %.

+   8. Given the following fragment that programs to convert from degrees Celsius to degrees Fahrenheit, answer the following questions:

double c = 20;
double f;
f = (9/5) * c + 32.0;

a. What value is assigned to f?
b. Explain what is actually happening, and what the programmer likely wanted.
c. Rewrite the code as the programmer intended.

# Type Casting

A type cast is a way of changing a value of one type to a value of another type. A type cast is a kind of function that takes a value of one type and produces a value of another type. C++ has four to six kinds of casts, depending on how you count them. There is an older form of type cast that has two notations for expressing it, and there are four new kinds of type casts introduced with the latest standard. The new kinds of type casts were designed as replacements for the older form; in this book, we will use the newer ones. However, C++ retains the older kind() along with the newer kinds, so we will describe the older kind as well.

Let's start with the newer kind of type casts. Consider the expression 9/2 when operands are an integer type, C++ performs integer division. In some situations, you might want the answer to be the double value 4.5. You can get a result of 4.5 by using the "equivalent" floating-point value 2.0 in place of the integer value 2, as in 9/2.0, which evaluates to 4.5. But what if the 9 and the 2 are variables of type int n and m? Then n/m yields 4. If you want floating-point division in this case, you must do a type cast from int to double (or another floating-point type), as in the following:

```
ans = n/static_cast<double>(m);
```