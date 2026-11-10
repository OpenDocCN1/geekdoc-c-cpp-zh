the extent possible using such declarations and other methods. The VAX computer uses two bytes to store short ints, which is half the amount it uses for ints; but for present-day PCs, with cheap and plentiful memory, most compiler writers make no distinction between int and short int.

**unsigned short** For the unsigned short int variable, the range of values does not exceed that of the unsigned int; it may be shorter.

**unsigned long** The unsigned long variable declaration transforms the range of long int to the set of 4-byte non-negative integers with values ranging from 0 to 4294967295.

**long** On most computers, long int variables are 4-byte integers with values ranging over the interval [-2147483648 to 2147483647].

**float** Integer and character data types are incapable of storing numbers with fractional parts. Depending on the precision required, C provides two variable types for computation with floating-point numbers, i.e., numbers with a decimal (internally a binary) point. floats are stored in four bytes and are accurate to about seven significant digits.

# Note

+   - It must be remembered that the floating point numbers held in a computer's memory are at best approximations to real numbers. The finite extent of the word size of any computer forces a truncation or round-off of the value to be stored; whether a storage location is two bytes wide, or four, or even eight, the value stored therein can be precise only to so many binary digits. In any computation with floating point numbers, errors of round-off or truncation are necessarily introduced. Therefore, any number with a long string of digits after the decimal point, given by a computer as the result of a computation, may not be quite as accurate as it seems.

**double** Because the words of memory can store values that are precise only to a fixed number of figures, any calculation involving floating-point numbers almost invariably introduces round-off errors. At the same time, scientific computations often demand a far greater accuracy than that provided by single precision arithmetic, i.e., arithmetic with the four-byte float variables. Thus, where large-scale scientific or engineering computations are involved, the double declaration becomes the natural choice for program variables. The double specification allows the storage of double precision floating-point numbers (in eight consecutive bytes) that are held correct to 15 digits and have a much greater range of definition than floats.

**Boolean data type _Bool** A _Bool variable is defined in the language to be large enough to store just the values 0 and 1. The precise amount of memory that is used is unspecified. _Bool variables are used in programs that need to indicate a

Boolean condition. For example, a variable of this type might be used to indicate whether all data has been read from a file. By convention, 0 is used to indicate a false value and 1 indicates a true value. When assigning a value to a _Bool variable, a value of 0 is stored as 0 inside the variable, whereas any nonzero value is stored as 1. To make it easier to work with _Bool variables in a program, the standard header file stdbool.h defines the values for bool, as true, and false.

# 8.9 PROGRAM STATEMENT

A statement is a syntactic construction that performs an action when a program is executed. All C program statements are terminated with a semicolon (;). A program statement in C can be classified as shown in Fig. 8.9.

**Declaration** is a program statement that serves to communicate to the language translator information about the name and type of the data objects needed during program execution.

![](bbox=[0.55, 0.34, 0.9, 0.5])

Fig.8.9 Different types of program statements available in C

**Expression statement** is the simplest kind of statement which is no more than an expression followed by a semicolon. An expression is a sequence of operators and operands that specifies computation of a value.

```
x = 4
```

is just an expression (which could be part of a larger expression), but

```
x = 4;
```

is a statement.

**Compound statement** is a sequence of statements that may be treated as a single statement in the construction of larger statements.

**Labeled statements** can be used to mark any statement so that control may be transferred to the statement by switch statement.

**Control statement** is a statement whose execution results in a choice being made as to which of two or more paths should be followed. In other words, the control statements determine the 'flow of execution' in a program.