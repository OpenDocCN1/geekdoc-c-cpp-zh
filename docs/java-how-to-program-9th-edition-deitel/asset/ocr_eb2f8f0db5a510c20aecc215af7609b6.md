total. The last three statements in the block would fall outside the loop body, causing the computer to interpret the code incorrectly as follows:

```
while ( grade != -1 )
    total = total + grade; // add grade to total
    gradeCounter = gradeCounter + 1; // increment counter
    // prompt for input and read next grade from user
    System.out.print( "Enter grade or -1 to quit: " );
    grade = input.nextInt();
```

The preceding code would cause an infinite loop in the program if the user did not input the sentinel -1 at line 54 (before the while statement).

# Common Programming Error 4.5

> Omitting the braces that delimit a block can lead to logic errors, such as infinite loops. To prevent this problem, some programmers enclose the body of every control statement in braces, even if the body contains only a single statement.

# Explicitly and Implicitly Converting Between Primitive Types

If at least one grade was entered, line 72 of Fig. 4.9 calculates the average of the grades. Recall from Fig. 4.6 that integer division yields an integer result. Even though variable average is declared as a double (line 45), the calculation

```
average = total / gradeCounter;
```

loses the fractional part of the quotient before the result of the division is assigned to average. This occurs because total and gradeCounter are both integers, and integer division yields an integer result. To perform a floating-point calculation with integer values, we must temporarily treat these values as floating-point numbers for use in the calculation. Java provides the unary cast operator to accomplish this task. Line 72 uses the (double) cast operator—a unary operator—to create a temporary floating-point copy of its operand total (which appears to the right of the operator). Using a cast operator in this manner is called explicit conversion or type casting. The value stored in total is still an integer.

The calculation now consists of a floating-point value (the temporary double version of total) divided by the integer gradeCounter. Java knows how to evaluate only arithmetic expressions in which the operands’ types are identical. To ensure that the operands are of the same type, Java performs an operation called promotion (or implicit conversion) on selected operands. For example, in an expression containing values of the types int and double, the int values are promoted to double values for use in the expression. In this example, the value of gradeCounter is promoted to type double, then the floating-point division is performed and the result of the calculation is assigned to average. As long as the (double) cast operator is applied to any variable in the calculation, the calculation will yield a double result. Later in this chapter, we discuss all the primitive types. You’ll learn more about the promotion rules in Section 6.7.

# Common Programming Error 4.6

> A cast operator can be used to convert between primitive numeric types, such as int and double, and between related reference types (as we discuss in Chapter 10, Object-Oriented Programming: Polymorphism). Casting to the wrong type may cause compilation errors or runtime errors.