# FIGURE A-2 Fundamental data types

| Category | | | |
|---|---|---|---|
| Boolean | bool | | |
| Character | char | signed char | unsigned char |
| Signed integer | short | int | long |
| Unsigned integer | unsigned short | unsigned int | unsigned long |
| Floating point | float | double | long double |

A boolean value can be either true or false. Characters are represented by their ASCII integer values, which are listed in Appendix J. Integer values are either signed, such as –5 and +98, or unsigned, such as 5 and 98. The floating-point types are used for real numbers that have both an integer portion and a fractional portion. Boolean, character, and integer types are called integral types. Integral and floating-point types are called arithmetic types.

Most of the data types are available in several forms and sizes. Although you will probably not need more than the four types given previously, Figure A-2 lists the available fundamental data types for your reference.

The size of a data type affects the range of its values. For example, a long integer can have a larger magnitude than a short integer. The sizes of—and therefore the specific ranges for—a data type depend on the particular computer and version of C++ that you use. C++, however, provides a way to determine these ranges, as you will see later in Section A.1.6.

# A.1.4 Variables

A variable, whose name is a C++ identifier, represents a memory location that contains a value of a particular data type. You declare a variable's data type by preceding the variable name with the data type, as in

```
double radius; // Radius of a sphere
```

Note that you can write a comment on the same line to describe the purpose of the variable.

This declaration is also a definition in that it assigns memory for the variable radius. The memory, however, has no particular initial value and so is said to be uninitialized. The program in Figure A-1 declares radius without an initial value and later reads its value by using cin >> radius.

When possible, avoid uninitialized variables

When possible, you should avoid uninitialized variables. That is, you should initialize a variable when you first declare its data type or, alternately, declare a variable data type when you first assign it a value. For example, volume appears for the first time in line 10 of Figure A-1 in the statement

```
double volume = 4 * PI * radius * radius * radius / 3;
```

Because we did not declare volume's data type earlier in the program—thus avoiding an uninitialized value—we declare its data type and assign it a value in the same statement.

# A.1.5 Literal Constants

You use literal constants to indicate particular values within a program. The 4 and 3 in line 10 of Figure A-1 are examples of literal constants that are used within a computation. You can also use a literal constant to initialize the value of a variable. For example, you use true and false as the values of a boolean variable, as mentioned previously.