# 5.9  SPECIAL OPERATORS

![](bbox=[0.768, 0.136, 0.885, 0.181])

C supports some special operators of interest such as comma operator, sizeof operator, pointer operators (& and *) and member selection operators (. and ->). The comma and sizeof operators are discussed in this section while the pointer operators are discussed in Chapter 13. Member selection operators which are used to select members of a structure are discussed in Chapters 12 and 13. ANSI committee has introduced two preprocessor operators known as “string-izing” and “token-pasting” operators (# and ##).

# 5.9.1  The Comma Operator

The comma operator can be used to link the related expressions together. A comma-linked list of expressions are evaluated left to right and the value of right-most expression is the value of the combined expression. For example, the statement

```
value = (x = 10, y = 5, x+y);
```

first assigns the value 10 to x, then assigns 5 to y, and finally assigns 15 (i.e. 10 + 5) to value. Since comma operator has the lowest precedence of all operators, the parentheses are necessary. Some applications of comma operator are:

```
In for loops:

    for ( n = 1, m = 10, n <=m; n++, m++)

In while loops:

    while (c = getchar(), c != '10')

Exchanging values:

    t = x, x = y, y = t;
```

# 5.9.2  The sizeof Operator

The sizeof is a compile time operator and, when used with an operand, it returns the number of bytes the operand occupies. The operand may be a variable, a constant or a data type qualifier. Examples:

```
m = sizeof (sum);
n = sizeof (long int);
k = sizeof (235L);
```

The sizeof operator is normally used to determine the lengths of arrays and structures when their sizes are not known to the programmer. It is also used to allocate memory space dynamically to variables during execution of a program.

# WORKED-OUT PROBLEM 5.3

In Fig. 5.3, the program employs different kinds of operators. The results of their evaluation are also shown for comparison.

Notice the way the increment operator ++ works when used in an expression. In the statement

```
c = ++a - b;
```

new value of a (= 16) is used thus giving the value 6 to c. That is, a is incremented by 1 before it is used in the expression. However, in the statement

```
d = b++ + a;
```