Advanced math like absolute value, rounding to the nearest decimal, rounding up, or rounding down can be performed using math functions. Python has some functions which are built-in pre-written code that can be referenced to make performing certain tasks easier. The general syntax to use Python math functions is to list the function name, followed by the variable name or value as an argument, as follows:

```
```python
method(value)
method(variable)
```
```

The math functions for absolute value and rounding follow the syntax above, but some math functions, like rounding up or rounding down are stored in a separate math module. To use these math functions you must:

+   - Write the statement `import math` just once in your code before using the math functions in the math module.
+   - Reference the math module, as follows: `math.method(value)` or `math.method(variable)`.

See these math functions with examples in Table 14-2.

![](bbox=[0.116, 0.465, 0.205, 0.537])

`Modules` are separate files that contain Python code, and the module must be referenced or imported before any code from the module can be used.

| Function name | Description | Example | Result |
|---|---|---|---|
| `abs(n)` | Return the absolute value of a number (n) | `abs(-99)` | `99` |
| `round(n, d)` | Round a number (n) to a number of decimal points (d) | `round(3.1415, 2)` | `3.14` |
| `math.floor(n)` | Round down to the nearest integer | `math.floor(4.7)` | `4.0` |
| `math.ceil(n)` | Round up to the nearest integer | `math.ceil(7.3)` | `8.0` |

![](bbox=[0.132, 0.794, 0.215, 0.865])

See all the function in the math module by visiting `https://docs.python.org/2/library/math.html`.