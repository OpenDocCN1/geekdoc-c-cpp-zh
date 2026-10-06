# 784 APPENDIX K C++ for Java Programmers

Consider the following Java if-else statement that compares the integer x to 6 and increments y by 10 if x is 6, and by 20 otherwise:

```
if (x == 6)
y += 10;
else
y += 20;
```

Because the syntax for an if-else statement is the same in C++, we could place this statement in a C++ program and the variable x is equal to 6 and false otherwise. The test x==6 is a predicate expression that returns true if it returns a value of type boolean. A Java flow-control statement requires its test expression to have a boolean value, so you must use a predicate expression as the test expression.

A C++ control statement does not restrict the data type of its test expression. Flow-control decisions are made based on whether the expression returns zero or nonzero. If the test returns zero, any nonzero value is considered true. The equality operator in the example returns true, which is 1, if x has the value of 6, it returns false, which is 0. The if-else statement determines its choice of action based on these.

This behavior of the C++ if-else statement gives you great flexibility in constructing tests for flow-control statements. It can also create confusion and subtle logic errors. For example, consider the following if-else statement:

```
if (x = 6)
y += 10;
else
y += 20;
```

At first, this might be the same as the earlier example, but by closer inspection you can see that the test expression is the assignment statement x = 6. The Java compiler will reject this as an error, since it is not a predicate expression. The C++ compiler will accept this statement, and when the program runs, the if-else statement will be evaluated as follows:

```
if (x = 6) // The variable x is assigned the value of 6.
y += 10; // it is non-zero, so it is "true"; increment y by 10.
```

Every time this code executes, x will be assigned the value 6, and y will be incremented by 10. The original value of x is overwritten by the if's test expression and is never used! Tracking down subtle errors, such as this, has cost this author many sleepless nights. When performing tests in C++ flow-control statements, always check that the test uses == and !=.

**Functions.** As mentioned, C++ functions do not need to be part of a class. You do not need to precede C++ functions with access modifiers, as you would for Java methods. The syntax for declaration and invocation of a C++ function is similar to that of a Java method. Functions can be defined anywhere in a C++ file, except inside another function.

Here is an example of a C++ function, realCube, that has a parameter of type double and returns the cube of a number:

```
double realCube(double x)
{
  return x * x * x;
} // defined after realCube
```

Any function defined after realCube can invoke realCube. But if a function is defined before realCube and needs to call it? In this case, the compiler would issue an error stating that