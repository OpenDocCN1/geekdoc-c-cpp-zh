# 5.2. BOOLEAN EXPRESSIONS

| Operator | Meaning |
|---|---|
| == | Equal to |
| < | Less than |
| > | Greater than |
| <= | Less than or equal to |
| >= | Greater than or equal to |
| != | Not equal to |

Table 5.1: C++ Relational operators

```
cout << "a = " << a << " b = " << b << endl;
// Assign Boolean value to an integer
int x = a, y = true;
cout << "a = " << a << " b = " << b << endl;
cout << "x = " << x << " y = " << y << endl;
// More mixing
a = 1725; // Warning issued
b = -19; // Warning issued
cout << "a = " << a << " b = " << b << endl;
```

As you can see from line 5.1 (boolvars.cpp), the values **false** and **true** are represented as 0 and 1. More precisely, the result of bool variable of other than 0 or any non-zero integer (positive or negative) means **true**. The direct assignment to a **bool** variable of integer truncation of 'int' to 'bool', the variable is still interpreted as **true**. The data type **bool** is a convenience for programmers; any C++ program can use bool variables to achieve the same results. Boolean values and variables are freely implicit and interchangeable with integers, the **bool** type is convenient and should be used when the context involves true values instead of numbers.

It is important to note that Visual C++ issues warnings for the last assignment statements in Listing 5.1 (boolvars.cpp). Even though any non-zero value is considered **true**, the preferred integer equivalent is **true** (as you can see when you print the literal value **true**). Since the need to assign to a Boolean variable other than **true** or **false** the integer 1 or 0 is extremely rare, the compiler's message alerts the programmer to check sure that the assignment is not a mistake.

# 5.2 Boolean Expressions

The simplest Boolean expressions are **false** and **true**, the bool literals. A Boolean variable is also a Boolean expression. An expression comparing numeric for equality or inequality is also a Boolean expression. The simplest kinds of Boolean expressions use **relational operators** to compare two values. Table 5.1 lists the relational operators available in C++.

Table 5.2 shows some boolean expressions with their associated values. An expression like **10 < 20** is legal but bit of little use, since the expression **true** is equivalent, simpler, and less likely to confuse readers. Boolean expressions are extremely useful when their true depends on the values of one or more variables.

The relational operators are binary and all associative. They all have a lower precedence