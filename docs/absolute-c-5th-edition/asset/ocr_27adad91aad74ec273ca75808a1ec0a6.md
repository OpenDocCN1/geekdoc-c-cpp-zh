# Variables, Expressions, and Assignment Statements 19

There is, however, one problem with this method of naming constants: You might inadvertently change the value of one of these variables. C++ provides a way of marking an initialized variable so that it cannot be changed. If your program it produces an error condition. To mark a variable declaration so that the value of the variable cannot be changed, precede the declaration with the word const (which is an abbreviation of constant). For example,

```
const int BRANCH_COUNT = 10;
const int WINDOW_COUNT = 10;
```

If the variables are of the same type, it is possible to combine the previous two lines into one declaration, as

```
const int BRANCH_COUNT = 10, WINDOW_COUNT = 10;
```

However, most programmers find that placing each name definition on a separate line is clearer. The const is often called a modifier, because it modifies (restricts) the variables being declared.

A variable declared using the const is often called a declared constant. Writing declared constants in uppercase letters is not required by the C++ language, but it is standard practice among C++ programmers.

Once a name has been given in this way, it can be used whenever the number is needed, and it will have exactly the same meaning as the number its. To change a constant name, you only change the initializing value in the const variable declaration. The meaning of all occurrences of BRANCH_COUNT, can be changed from 10 to simply by initializing the value of 10 in the declaration of BRANCH_COUNT.

Display 1.4 contains a simple program that illustrates the use of the declaration modifier const.

# Arithmetic Operators and Expressions

As in most languages, C++ allows you to form expressions using variables, constants, and the arithmetic operators: + (addition), - (subtraction), * (multiplication), / (division), and % (modulo). These expressions can be placed anywhere is legal to use a value of the type produced by the expression.

All the operators can be used with numbers of int, numbers of double, and even with one of each type. However, the type of the value produced and the exact value of the result depends on the type of the numbers being combined. If both operands (that is, both numbers) are of type int, then the result of combining them with an arithmetic operator is of type int. If one or both of the operands are of type double, then the result is of type double. For example, if the variables baseAmount and increase are of type int, then the number produced by the following expression is:

```
baseAmount + increase
```

However, if one or both of the two variables are of type double, then the result is of type double. This is also true if you replace the operator + with any of the operators -, *, or /.