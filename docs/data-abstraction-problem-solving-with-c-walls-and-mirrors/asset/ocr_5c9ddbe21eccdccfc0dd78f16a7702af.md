# 688 APPENDIX A Review of C++ Fundamentals

# ### FIGURE A-2 Fundamental data types

| Category | Available Data Types by Category |
|---|---||
| Boolean | bool | |
| Character | char signed char unsigned char |
| Signed integer | short int long |
| Unsigned integer | unsigned short unsigned unsigned long |
| Floating point | float double long double |

A boolean value can be either true or false. Characters are represented by the ASCII value, which are listed in Appendix A. Integer values are either signed, such as -5 and +98, or unsigned, as 5 and 98. The **floating-point types** are used for numbers that have both an integer and a fractional part. Boolean, character, and integer are called **integral types**. Integral and floating-point types are called **arithmetic types**.

Most of the types are available in several forms and sizes. Although you will not need more than the four given previously, Figure A-2 lists the fundamental data types for your reference.

The size of a data type affects the range of its values. For example, a long can have a larger magnitude than a short integer. The sizes of—and the specific ranges for—a data type depend on the particular computer and version of C++ that you use. C++, however, provides a way to determine these ranges, as you will see later in Section A.6.

# ### A.1.4 Variables

A variable, whose is a C++ identifier, represents a memory location that contains a value of a particular data type. You declare a variable's data type by preceding the variable name with the data type, as

```
double radius; // Radius of a sphere
```

Note that you can write a comment on the line to describe the purpose of the variable. The memory, however, has no initial value and is said to be uninitialized. In Figure A-1 declares radius without an initial value and later reads its value using cin >> radius;

When, you should avoid uninitialized variables. That is, you should initialize a variable when you first declare its data type or, declare a variable's data type when you first assign it a value. For example, volume appears in the first line of 10 of Figure A-1 in the statement

```
double volume = 4 * PI * radius * radius / 3;
```

Because we did not declare volume's data type in the program—avoiding an uninitialized variable—we declare its data type and assign it value in the same statement.

# ### A.1.5 Literal Constants

You use literal constants to indicate particular values within a program. The 4 and 3 in line 10 of Figure A-1 are examples of literal constants that are used in a computation. You can also use a literal to initialize the value of a variable. For example, you use true and false as the values of a boolean variable, as mentioned previously.