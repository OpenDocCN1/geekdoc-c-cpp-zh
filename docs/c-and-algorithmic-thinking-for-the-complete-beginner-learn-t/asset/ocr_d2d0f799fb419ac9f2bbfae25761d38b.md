The modulus operator (%) returns the remainder of an integer division, which means that

```
`a = 13 % 3`
```

assigns a value of 1 to variable a.

> > **Notice:** In C++, the modulus operator (%) cannot be used with floating-point numbers. For example, the operation 13.4 % 4 cannot be performed.

> > **Notice:** Please keep in mind that flowcharts are a loose method used to represent an algorithm. Although the use of the modulus (%) operator is allowed in flowcharts, this book uses the commonly accepted MOD operator instead! For example, the C++ statement `b = 13 % 3` is represented in a flowchart as

![](bbox=[0.049, 0.305, 0.989, 0.427])

In mathematics, as you already know, you are allowed to use parentheses as well as braces and brackets.

$$y = \frac{5}{2}\left\{3 + 2\left[4 + 7\left(7 - \frac{4}{3}\right)\right]\right\}$$

However, in C++ there is no such thing as braces and brackets. Parentheses are all we have; therefore, the same expression should be written using parentheses instead of braces or brackets.

```
`y = 5 / 2 * (3 + 2 * (4 + 7 * (7 - 4 / 3)));`
```

One other thing that is legal in mathematics but not in C++ is that you can skip the multiplication operator and write 3x, meaning “3 times x.” In C++, however, you must always use an asterisk anywhere a multiplication operation exists. This is one of the most common mistakes novice programmers make when they write mathematical expressions in C++.

# 7.3 What is the Precedence of Arithmetic Operators?

Arithmetic operators follow the same precedence rules as in mathematics, and these are: multiplication and division are performed first, addition and subtraction are performed afterwards.

| Precedence | Arithmetic Operators |
|---|---|
| Higher precedence ↑ Lower precedence | *, /, % (higher); +, - (lower) |