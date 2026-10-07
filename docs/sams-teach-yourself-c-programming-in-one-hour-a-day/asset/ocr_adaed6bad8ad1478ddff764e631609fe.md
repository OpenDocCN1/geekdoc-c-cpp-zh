The following macro, in which the conditional operator determines the larger of two values, also uses each of its parameters twice. (You learned about the conditional operator in Lesson 4, “The Pieces of a C Program: Statements, Expressions, and Operators.)

```
#define LARGER(x, y) ((x) > (y) ? (x) : (y))
```

A macro can have as many parameters as needed, but all the parameters in the list must be used in the substitution string. For example, the macro definition

```
#define ADD(x, y, z) ((x) + (y))
```

is invalid because the parameter z is not used in the substitution string. Also, when you invoke the macro, you may not count the correct number of arguments.

When you write a macro definition, the opening parenthesis must immediately follow the macro name; there be no whitespace. The opening parenthesis tells the preprocessor that a function is being defined and that this isn't a symbolic constant type substitution. Look at the following definition:

```
#define SUM(x, y, z) ((x)+(y)+(z))
```

Because of the space between SUM and ,, the preprocessor treats this like a substitution. Every occurrence of SUM in the source code is replaced with (x, y, z) ((x)+(y)+(z)), clearly not what you wanted.

Also note that in the substitution string, each parameter is enclosed in parentheses. It is necessary to avoid unintended side effects when passing expressions as arguments to the macro. Look at the following example of a macro defined without parentheses:

```
#define SQUARE(x) x*x
```

If you use this macro with a simple variable as an argument, there’s no problem. But what if you pass an expression as an argument?

```
result = SQUARE(x + y);
```

The resulting macro expansion is as follows, which doesn’t give the proper result:

```
result = x + y * x + y;
```

If you use parentheses, you can avoid the problem, as shown in this example:

```
#define SQUARE(x) (x) * (x)
```

This definition expands to the following line, which gives the proper result:

```
result = (x + y)*(x + y);
```

You can obtain additional flexibility in macro definitions using the stringizing operator (#) (sometimes called the string-literal operator). When a macro parameter is