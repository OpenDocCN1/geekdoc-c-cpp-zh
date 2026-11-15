
The statements that specify the operations to be performed in the example program are the following:

```
// Compute sides of a right triangle
side1 = x2 - x1;
side2 = y2 - y1;
distance = sqrt(side1*side1 + side2*side2);

// Print distance
cout << "The distance between the two points is "
     << distance << endl;
```

These statements compute the lengths of the two sides of the right triangle formed by two points (see Figure 1.5, page 28) and then compute the length of the hypotenuse of the right triangle. The details of the syntax of these assignment statements are discussed later in the chapter. After the distance is computed, it is printed with the cout statement. This output statement is too long for a single line, so we separate the statement into two lines; the indenting of the second line again indicates that it is a continuation of the previous line. A semicolon ends the output statement. Additional comments are used to explain the computations and the output statement. Note that all C++ statements are required to end with a semicolon.

To end execution of the program and return control to the operating system, we use a return (0); statement.

```
// Exit program
return (0);
```

This statement returns a value of zero to the operating system. A value of zero indicates a successful end of execution.

The body of the main function then ends with the right brace on a line by itself, and another comment line to delineate the end of the main function.

```
}/*---------------------------------------------------*/
```

Note that we have included blank lines (also called whitespace) in the program to separate different components. These blank lines make a program more readable and easier to modify. The statements within the main function were indented in order to show the structure of the program. This spacing provides a consistent style, and makes our programs easier to read.

Now that we have closely examined the C++ program from Chapter 1, we can compare its structure to the general form of a C++ program:

```
preprocessing directives

int main()
{
    declarations;
    statements;
}
```

This structure is evident in the programs developed in this chapter and in the chapters that follow.

## Modify 2.1

- 1. Create a file containing the sample program discussed in this section using either an editor that is part of your C++ compiler or using a word processor. Then compile and execute the program. You should get this output:
- The distance between the two points is: 3.61
- 
- 2. Change the values given to the two points to the coordinates (-1, 6) and (2, 4). Run the program with these new values. Did the distance change? Explain.
- 
- 3. Change the values given to the two points so that they represent the coordinates (1, 0) and (5, 7). Check the program's answer with your calculator.
- 
- 4. Change the values given to the two points so that they represent the same coordinates (2, 4) and (2, 4). Does the program give the correct answer?

### 2.2 Constants and Variables

- constants
- variables
- identifier

Constants and variables represent objects that we use in our programs. Literal **constants** are specific values such as 2, 3.1416, -1.5, 'a', or "hello" that we use to form C++ statements. The value of these objects cannot be changed. **Variables** are memory locations that are assigned a name or **identifier**. The identifier is used to reference the value stored in the memory location. A useful analogy for a memory location and its corresponding identifier is a mailbox that is associated with the name of an individual; the memory location (or mailbox) may contain an object. The following shows the variables, their identifiers, and their initial values after the following declaration statement from program Chapter1_1:

```
double x1(1), y1(5), x2(4), y2(7),
side1, side2, distance;
```

| double x1 | 1.0 | double y1 | 5.0 |
| --- | --- | --- | --- |
| double x2 | 4.0 | double y2 | 7.0 |
| double side1 | ? | double side2 | ? |
| double distance | ? | | |

- garbage
- memory snapshot

The values of variables that were not given initial values are unspecified, and thus indicated with a question mark; sometimes these values are called **garbage** values because their values are unpredictable. A diagram such as this that shows an object along with its identifier, its value, and its data type is called a **memory snapshot**. A memory snapshot shows the contents of a memory location at a specified point in the execution of the program. The preceding memory snapshot shows the objects and their contents after execution of the declaration statement. The objects are declared to be of type **double** and will be represented in memory using the standard IEEE format. For simplicity we show only the value of the variable and its data type, but it is important to remember that the value of a floating point variable, even when initialized with an integer constant, will be represented in memory using the IEEE floating point representation of the integer value.

*If you use a word processor to generate a source file, be sure to save it as a text file.*

| alignas | alignof | and | and_eq | asm |
| :--- | :--- | :--- | :--- | :--- |
| auto | bitand | bitor | bool | break |
| case | catch | char | char16_t | char32_t |
| class | compl | const | constexpr | const_cast |
| continue | decltype | default | delete | do |
| double | dynamic_cast | else | enum | explicit |
| extern | false | float | for | friend |
| goto | if | inline | int | long |
| mutable | namespace | new | noexcept | not |
| not_eq | nullptr | operator | or | or_eq |
| private | protected | public | register | reinterpret_cast |
| return | short | signed | sizeof | static |
| static_assert | static_cast | struct | switch | template |
| this | thread_local | throw | true | try |
| typedef | typedef | typename | union | unsigned |
| using | virtual | void | volatile | wchar_t |
| while | xor | xor_eq | | |

We frequently use memory snapshots to show the contents of objects both before and after a statement is executed in order to show its effect. The rules for selecting a valid identifier are as follows:

- an identifier must begin with an alphabetic character or the underscore character
- alphabetic characters in an identifier can be lowercase or uppercase letters
- an identifier can contain digits, but not as the first character
- an identifier can be of any length, but the first 31 characters of the identifier must be unique

C++ is case-sensitive, which means uppercase letters are distinguished from lowercase letters; thus Side1, SIDE1 and side1 represent three different objects. C++ also includes keywords with special meaning to the C++ compiler that cannot be used for identifiers; a complete list of keywords is given in Table 2.1.

Examples of valid identifiers are distance, x1, xSum, averageMeasurement, and initialTime. Examples of invalid identifiers are 1x (begins with a digit), switch (a keyword), $sum (contains an invalid character $), and rate% (contains an invalid character %).

An identifier name should be carefully selected so that it reflects the contents of the object, if possible, the name should also indicate the units of measurement. For example, if an object represents a temperature measurement in degrees Fahrenheit, use an identifier such as tempF or degreesF. If an object represents an angle, name it thetaRad to indicate that the angle is measured in radians or thetaDeg to indicate that the angle is measured in degrees.

![](img/0235a4ea835dc4575bd036e024a533b3_60_0.png)

Declarations statements included in any block of code must include not only the identifiers of the objects that we plan to use in our program, but they must also specify the data type of the object. C++ is a strongly typed programming language. This means that every identifier must be declared before it can be used in a statement. Data types are presented after a discussion on scientific notation.

### Practice 2.1

Determine which of the following names are valid identifiers. If a name is not a valid identifier, give the reason that it is not acceptable, and suggest a valid replacement.

- 1. density
- 2. area
- 3. Time
- 4. xsum
- 5. x_sum
- 6. tax-rate
- 7. perimeter
- 8. sec**2
- 9. degrees_C
- 10. break
- 11. #123
- 12. x$y
- 13. count
- 14. void
- 15. f(x)
- 16. f2
- 17. Final_Value
- 18. w1.1
- 19. reference1
- 20. reference_1
- 21. m/s

### Scientific Notation

A floating-point value is one that can represent both integer and non-integer values, such as 2.5, -0.004, and 15.0. A floating-point value expressed in scientific notation is rewritten as a mantissa times a power of 10, where the mantissa has an absolute value greater than or equal to 1.0 and less than 10.0. For example, in scientific notation, 25.6 is written as 2.56 x 10^1, -0.004 is written as -4.0 x 10^-3, and 1.5 is written as 1.5 x 10^0. In exponential notation, the letter e is used to separate the mantissa from the exponent of the power of 10. Thus, in exponential notation, 25.6 is written as 2.56e1, -0.004 is written as -4.0e-3, and 1.5 is written as 1.5e0.

The number of digits allowed by the computer for the decimal portion of the mantissa determines the precision, and the number of digits allowed for the exponent determines the range. Thus, values with two digits of precision and an exponent range of -8 to 7 could include values such as 2.3 x 10^2 (230,000) and 5.9 x 10^-8 (0.000000059). This precision and exponent range would not be sufficient for many of the types of values that we use in engineering problem solutions. For example, the distance in miles from Mars to the Sun, with seven digits of precision, is 141,517,510, or 1.4151751 x 10^8; to represent this value, we would need at least seven digits of precision and an exponent range that included the integer 8.

### Practice 2.2

In Problems 1 through 6, express the value in scientific notation. Specify the number of digits of precision needed to represent each value.

- 1. 35.004
- 2. 0.00042
- 3. -50,000
- 4. 3.15723
- 5. -0.09997
- 6. 10,000.028
