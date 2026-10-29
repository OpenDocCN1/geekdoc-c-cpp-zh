
## Initializing Variables in Declarations

You can initialize a variable (that is, give it a value) at the time that you declare the variable.

### SYNTAX

```
Type_Name Variable_Name_1 = Expression_for_Value_1,
    Variable_Name_2 = Expression_for_Value_2, ...;
```

### EXAMPLES

```
int count = 0, limit = 10, fudgeFactor = 2;
double distance = 999.99;
```

### SYNTAX

Alternative syntax for initializing in declarations:

```
Type_Name Variable_Name_1 (Expression_for_Value_1),
    Variable_Name_2 (Expression_for_Value_2), ...;
```

### EXAMPLES

```
int count(0), limit(10), fudgeFactor(2);
double distance(999.99);
```

### TIP: Use Meaningful Names

Variable names and other names in a program should at least hint at the meaning or use of the thing they are naming. It is much easier to understand a program if the variables have meaningful names. Contrast

```
x = y * z;
```

with the more suggestive

```
distance = speed * time;
```

The two statements accomplish the same thing, but the second is easier to understand.

### More Assignment Statements

A shorthand notation exists that combines the assignment operator (=) and an arithmetic operator so that a given variable can have its value changed by adding, subtracting, multiplying by, or dividing by a specified value. The general form is

```
Variable Operator = Expression
```

which is equivalent to

```
Variable = Variable Operator (Expression)
```

The Expression can be another variable, a constant, or a more complicated arithmetic expression. The following list gives examples.

| EXAMPLE | EQUIVALENT TO |
| --- | --- |
| count += 2; | count = count + 2; |
| total -= discount; | total = total - discount; |
| bonus *= 2; | bonus = bonus * 2; |
| time /= rushFactor; | time = time / rushFactor; |
| change %= 100; | change = change % 100; |
| amount *= cnt1 + cnt2; | amount = amount * (cnt1 + cnt2); |

### Self-Test Exercises

- 1. Give the declaration for two variables called feet and inches. Both variables are of type int and both are to be initialized to zero in the declaration. Give both initialization alternatives.
- 2. Give the declaration for two variables called count and distance. count is of type int and is initialized to zero. distance is of type double and is initialized to 1.5. Give both initialization alternatives.
- 3. Write a program that contains statements that output the values of five or six variables that have been defined, but not initialized. Compile and run the program. What is the output? Explain.

### Assignment Compatibility

As a general rule, you cannot store a value of one type in a variable of another type. For example, most compilers will object to the following:

```
int intVariable;
intVariable = 2.99;
```

The problem is a type mismatch. The constant 2.99 is of type double, and the variable intVariable is of type int. Unfortunately, not all compilers will react the same way to the previous assignment statement. Some will issue an error message, some will give only a warning message, and some compilers will not object at all. Even if the compiler does allow you to use the previous assignment statement, it will give intVariable the int value 2, not the value 3. Since you cannot count on your compiler accepting the previous assignment, you should not assign a double value to a variable of type int.

There are some special cases in which it is permitted to assign a value of one type to a variable of another type. It is acceptable to assign a value of an integer type, such as `int`, to a variable of a floating-point type, such as type `double`. For example, the following is a valid and acceptable style:

```
double doubleVariable;
doubleVariable = 2;
```

The style shown will set the value of the variable named `doubleVariable` equal to 2.0.

Although it is usually a bad idea to do so, you can store an int value such as 65 in a variable of type char and you can store a letter such as 'z' in a variable of type int. For many purposes, the C language considers characters to be small integers, and perhaps unfortunately, C++ inherited this from C. The reason for allowing this is that variables of type char consume less memory than variables of type int; thus, doing arithmetic with variables of type char can save some memory. However, it is clearer to use the type int when you are dealing with integers and to use the type char when you are dealing with characters.

The general rule is that you cannot place a value of one type in a variable of another type—though it may seem that there are more exceptions to the rule than there are cases that follow the rule. Even if the compiler does not enforce this rule strictly, it is a good rule to follow. Placing data of one type in a variable of another type can cause problems because the value must be changed to a value of the appropriate type and that value may not be what you would expect.

Values of type `bool` can be assigned to variables of an integer type (`short`, `int`, `long`), and integers can be assigned to variables of type `bool`. However, it is poor style to do this. For completeness and to help you read other people’s code, here are the details: When assigned to a variable of type `bool`, any nonzero integer will be stored as the value true. Zero will be stored as the value false. When assigning a bool value to an integer variable, true will be stored as 1, and false will be stored as 0.

### Literals

A literal is a name for one specific value. Literals are often called constants in contrast to variables. Literals or constants do not change value; variables can change their values. Integer constants are written in the way you are used to writing numbers. Constants of type `int` (or any other integer type) must not contain a decimal point. Constants of type `double` may be written in either of two forms. The simple form for double constants is like the everyday way of writing decimal fractions. When written in this form a double constant must contain a decimal point. No number constant (either integer or floating-point) in C++ may contain a comma.

A more compact notation for constants of type double is called **scientific notation** or **floating-point notation** and is particularly handy for writing very large numbers and very small fractions. For instance, 3.67 × 10^17, which is the same as `367000000000000000.0` is best expressed in C++ by the constant `3.67e17`. The number 5.89 × 10^-6, which is the same as `0.00000589`, is best expressed in C++ by the constant `5.89e-6`. The e stands for exponent and means "multiply by 10 to the power that follows." The e may be either uppercase or lowercase.

Think of the number after the e as telling you the direction and number of digits to move the decimal point. For example, to change 3.49e+4 to a numeral without an e, you move the decimal point four places to the right to obtain 34900.0, which is another way of writing the same number. If the number after the e is negative, you move the decimal point the indicated number of spaces to the left, inserting extra zeros if need be. So, 3.49e-2 is the same as 0.0349.

The number before the e may contain a decimal point, although it is not required. However, the exponent after the e definitely must not contain a decimal point.

### What Is Doubled?

Why is the type for numbers with a fractional part called double? Is there a type called "single" that is half as big? No, but something like that is true. Many programming languages traditionally used two types for numbers with a fractional part. One type used less storage and was very imprecise (that is, it did not allow very many significant digits). The second type used double the amount of storage and so was much more precise; it also allowed numbers that were larger (although programmers tend to care more about precision than about size). The kinds of numbers that used twice as much storage were called double-precision numbers; those that used less storage were called single precision. Following this tradition, the type that (more or less) corresponds to this double-precision type was named double in C++. The type that corresponds to single precision in C++ was called float. C++ also has a third type for numbers with a fractional part, which is called long double.

Constants of type char are expressed by placing the character in single quotes, as illustrated in what follows:

```
char symbol = 'Z';
```

Note that the left and right single quote symbols are the same symbol.

Constants for strings of characters are given in double quotes, as illustrated by the following line taken from Display 1.1:

```
cout << "How many programming languages have you used? ";
```

Be sure to notice that string constants are placed inside double quotes, while constants of type char are placed inside single quotes. The two kinds of quotes mean different things. In particular, 'A' and "A" mean different things. 'A' is a value of type char and can be stored in a variable of type char. "A" is a string of characters. The fact that the string happens to contain only one character does not make "A" a value of type char. Also notice that for both strings and characters, the left and right quotes are the same.

quotes

Strings in double quotes, like "Hello", are often called C-strings. A C-string is not the same as the string class introduced earlier although both are used to store sequences of text and we sometimes use the two interchangeably. The difference is explained in detail in Chapter 9. Experts recommend you use the string class when possible instead of a C-string for purposes of security and flexibility.

C-string
