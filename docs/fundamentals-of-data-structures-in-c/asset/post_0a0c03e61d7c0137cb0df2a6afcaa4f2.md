
## Enumerated Data Type

The enumerated data type gives an opportunity to invent your own data type with a set of named integer constants represented by identifiers that specifies all the valid values a variable of that type may have. They can be used in any expression where integer constants are valid.

The general form or the syntax of enumerated data type is,

```
enum identifier { enumeration_list } list_of_variables;
```

where enum is a keyword, which is used to specify the enumerated data type, identifier is an user-defined enumerated data type which can be used to declare the enumeration_list also referred as enumeration constants. Both the identifier and the list_of_variables are optional, but at least one must be present. For example, the enumeration

```
enum month { JANUARY, FEBRUARY, MARCH, APRIL, MAY, JUNE, JULY,
AUGUST, SEPTEMBER, OCTOBER, NOVEMBER, DECEMBER };
```

creates a new type month in which the enumeration_list is JANUARY . . . , DECEMBER.

The values for the enumeration list are set automatically to integers 0 to 11. To number the enumeration_list from 1 to 12 the enum declaration should be

```
enum month { JANUARY = 1, FEBRUARY, MARCH, APRIL, MAY, JUNE, JULY,
AUGUST, SEPTEMBER, OCTOBER, NOVEMBER, DECEMBER };
```

where the first enumeration_list (i.e., JANUARY) is explicitly set to 1 and hence the remaining values are incremented from 1, and result in values of 1 to 12. To define a variable for the new type month, the statement

```
enum month month_start, month_end;
```

declares month_start and month_end as variables for the new type month.

### 1.6.3 Empty Data Type

The keyword void is used to indicate an empty data type. This data type is not used to declare any variables, but used to indicate nothing. When used as a function return type, void means that the function does not return a value. When used in a function parameter list, void means the function does not take any parameters.

## 1.7 Expressions using Operators in C

An operator is a symbol or a special character that tells the computer to perform certain mathematical or logical operations, which is applied to operands to give a result. Operators are used in programs to manipulate data and variables. The data items that operators act upon to evaluate expressions are called as operands. One of the main reasons for the power of C is its wide range of operators. C not only offers the common arithmetic and logical operators, but also offers operators for bit-level manipulations, pointer operations and so on. The operators used in C are

- Arithmetic operators
- Unary operators
- Increment and Decrement operators
- Relational operators
- Equality operators
- Logical operators
- Bitwise operators
- Conditional operator
- Assignment operators
- Special operators.

### 1.7.1 Arithmetic Operators

C language has all the basic arithmetic operators. Table 1.5 shows various arithmetic operators and their meaning.

| Operator | Meaning |
|---|---|
| + | Addition |
| - | Subtraction |
| * | Multiplication |
| / | Division |
| % | Modulo operation (remainder after integer division) |

The operands that act upon arithmetic operators must represent numeric values, thus the operands can be integer quantities or floating-point quantities. Division of one integer quantity by another is referred to as the integer division. Integer division truncates the fractional part (i.e., the decimal portion of the quotient will be dropped). Modulo division produces the remainder of an integer division as the result. Modulo division is only meaningful between integers.

Suppose when operands x and y are integer variables whose values are 9 and -4 respectively. Several arithmetic expressions and their results are

| Expression | Result |
|---|---|
| x + y | 5 |
| x - y | 13 |
| x * y | -36 |
| x / y | -2 |
| x % y | 1 |

When two operands such as x and y are declared as integers, an arithmetic operation performed on these integers are referred as **integer arithmetic**. It always yields an integer value. When two operands such as x and y are declared as real (i.e., `float` or `double` or `long double`) an arithmetic operation performed on these floats are referred to as floating-point arithmetic. It always yields a floating-point value. If either of the operands is real, an arithmetic operation performed on these integers is called as mixed-mode arithmetic. It always yields a real value (float value). For example,

```
125/25.0 = 5.0
```

Since 25.0 is real constant, 125 is converted to a real (i.e., 125.0) and the result is also a real.

### 1.7.2 Unary Operators

The operators that act upon a single operand to produce a new value are called as unary operators. Unary operators usually precede its operands, though some unary operators are written after their operands. Table 1.6 shows various unary operators and their meaning.

| Operator | Meaning |
|---|---|
| - | Unary minus |
| ++ | Increment by 1 |
| -- | Decrement by 1 |
| sizeof | Returns the size of the operand. |

When the operator is used before the variable, the operation is applied to the variable first, and then the result is used in the expression. This type of notation is referred as prefix notation. When the operator is used after the variable, the value of the variable is used first, and then the operation is applied to the variable. This type of notation is referred as postfix notation. If the value of the operand x is 3 then the various expressions and their results are

| Expression | Execution |
|---|---|
| ++x | x <- 3 + 1 |
| x++ | x <- 3 ; x <- 3 + 1 |
| --x | x <- 3 - 1 |
| x-- | x <- 3 ; x <- 3 - 1 |

The pre-increment operation (++x) increments x by 1 and then assigns the value to x. The post-increment operation (x++) assigns the value to x and then increments 1. The pre-decrement operation (--x) decrements 1 and then assigns to x. The post-decrement operation (x--) assigns the value to x and then decrements 1. These operators are usually very efficient, but causes confusion if you try to use too many evaluations in a single statement.

### The sizeof Operator

The sizeof operator is not a library function but a keyword, which returns the size of the operand in bytes. The sizeof operator always precedes its operand. This operator can be used for dynamic memory allocation. Various expressions and results of sizeof operator are

| Expression | Result |
|---|---|
| sizeof(char) | 1 |
| sizeof(int) | 2 |
| sizeof(float) | 4 |
| sizeof(double) | 8 |

### 1.7.3 Relational Operators

Relational operators are symbols that are used to test the relationship between two variables or between a variable and a constant. These operators are used for checking conditions in control statements. Table 1.7 shows various relational operators and their meaning.

Table 1.7 : Relational Operators and its Meaning

| Operator | Meaning |
|---|---|
| < | less than |
| > | greater than |
| <= | less than or equal to |
| >= | greater than or equal to |

An expression containing a relational operator is called as an relational expression. The value of the relational expression is either one or zero. If the expression is true, it is represented by an integer value 1. If the expression is false, it is represented by an integer value 0. These operators have left to right associativity.

If the values of x, y, z are 1, 2, 3 respectively then the results and the values returned by the expressions are

| Expression | Result | Value |
|---|---|---|
| x < y | True | 1 |
| (x + y) >= z | True | 1 |
| (y + z) > (x + z) | False | 0 |
| y >= 10*(x + z) | False | 0 |

### 1.7.4 Equality Operators

Closely associated with relational operators are two equality operators. Table 1.8 shows various equality operators and their meaning.

Table 1.8 : Equality Operators and its Meaning

| Operator | Meaning |
|---|---|
| == | equal to |
| != | not equal to |

The value of the expression is either one or zero. If the expression is true then the result will be one, if the expression is false then the result will be zero. If the values of x and y are 1 and 2 respectively, then the various expressions and their results are

| Expression | Result | Value |
|---|---|---|
| y != 2 | False | 0 |
| x == 2 | False | 0 |
| x == 1 | True | 1 |
| y != 3 | True | 1 |

### 1.7.5 Logical Operators

Operators, which are used to combine two or more relational expressions, are called as logical operators. These operators are used to test more than one condition at a time.

Table 1.9 shows various logical operators and their meaning.

| Operator | Meaning |
|---|---|
| && | Logical AND |
| \|\| | Logical OR |
| ! | Logical NOT |

### 1.7.6 Bit wise Operators

C has certain operators known as bit wise operators that are used in applications, which require manipulation of individual bits within a word of memory. These operators permit the programmer to access and manipulate individual bits within a piece of data. Bit wise operators can operate only on integers and characters but not on floats and doubles.

Table 1.10 shows the various bit wise operators and their meaning.

| Operator | Meaning |
|---|---|
| ~ | One's complement |
| << | Left shift |
| >> | Right shift |
| & | Bit wise AND |
| \| | Bit wise OR |
| ^ | Bit wise X-OR |

### Masking

Masking is a process in which a given pattern is transformed into another bit pattern by means of bit wise operator. The original bit pattern is one of the operands in the bitwise operation. The second operand called as the mask is a specially selected bit pattern that brings the desired transformation. Usually logical bitwise AND operator (&) is used for masking.
