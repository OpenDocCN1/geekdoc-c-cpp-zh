A macro without arguments is a symbolic constant. When the preprocessor encounters a macro with arguments, it substitutes the arguments in the replacement text, then expands the macro—that is, it replaces the macro with its replacement-text and argument list.

# 14.4.1 Macro with One Argument

Consider the following one-argument macro definition that calculates a circle’s area:

```
#define CIRCLE_AREA(x) ((PI) * (x) * (x))
```

# Expanding a Macro with an Argument

Wherever CIRCLE_AREA(argument) appears in the file, the preprocessor:

+   - substitutes argument for x in the replacement-text,
+   - replaces PI with its value 3.14159 (from Section 14.3), and
+   - expands the macro in the program.

For example, the preprocessor expands

```
double area = CIRCLE_AREA(4);
```

to

```
double area = ((3.14159) * (4) * (4));
```

At compile time, the compiler evaluates the preceding expression and assigns the result to the variable area.

# Importance of Parentheses

The parentheses around each x in the replacement-text force the proper evaluation order when a macro’s argument is an expression. Consider the statement

```
double area = CIRCLE_AREA(c + 2);
```

which expands to

```
double area = ((3.14159) * (c + 2) * (c + 2));
```

# It’s Better to Use a Function

Defining the CIRCLE_AREA macro as a function is safer. The circleArea function

```
double circleArea(double x) {
    return 3.14159 * x * x;
}
```