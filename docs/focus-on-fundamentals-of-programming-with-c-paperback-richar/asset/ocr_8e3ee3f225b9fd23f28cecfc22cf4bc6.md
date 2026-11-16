# Can you see why?

Note that integer division truncates towards zero:

```
int a, b;
:
a = 1/3;   // produces 0
b = 6/7;   // produces 0
```

However, if either operand of the division is a float, both operands are converted to float:

```
float w, x, y, z;
:
w = 1.0 / 3.0;   // 0.333333
x = 1.0 / 3;     // 0.333333
y = 6.0 / 7.0;   // 0.857143
z = 6 / 7.0;     // 0.857143
```

# Explicit (automatic) Conversions

The cast operator converts (casts) the value of a variable into a type that is different from the original type of the variable. The cast is specified by giving the cast type in parentheses followed by the expression to be cast:

```
(cast-type) expression
```

For example::

```
int x;
float y;
:
y = (float) x;
```