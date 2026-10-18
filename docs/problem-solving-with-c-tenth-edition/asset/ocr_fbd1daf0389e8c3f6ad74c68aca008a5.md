Display 2.6 illustrates how / and % work with values of type int.

# DISPLAY 2.6 Integer Division

When used with negative values of type int, the result of the operators / and % can be different for different implementations of C++. Thus, you should use / and % with int values only when you know that both values are non-negative.

Any reasonable spacing will do in arithmetic expressions. You can insert spaces before and after operations and parentheses, or you can omit them. Do whatever produces a result that is easy to read.

You can specify the order of operations by inserting parentheses, as illustrated in the following two expressions:

```
(x + y) * z
x + (y * z)
```

To evaluate the first expression, the computer first adds x and y and then multiplies the result by z. To evaluate the second expression, it multiplies y and z and then adds the result to x. Although you may be used to using mathematical formulas that contain square brackets and various other forms of parentheses, that is not allowed in C++. C++ allows only one kind of parentheses in arithmetic expressions. The other varieties are reserved for other purposes.

If you omit parentheses, the computer will follow rules called precedence rules that determine the order in which the operators, such as + and *, are performed. These precedence rules are similar to rules used in algebra and other mathematics classes. For example,

```
x + y * z
```

is evaluated by first doing the multiplication and then the addition. Except in some standard cases, such as a string of additions or a simple multiplication embedded inside an addition, it is usually best to include the parentheses, even if the intended order of operations is the one dictated by the precedence rules. The parentheses make the expression easier to read and less prone to programmer error. A complete set of C++ precedence rules is given in Appendix 2.

Display 2.7 shows some examples of common kinds of arithmetic expressions and how they are expressed in C++.