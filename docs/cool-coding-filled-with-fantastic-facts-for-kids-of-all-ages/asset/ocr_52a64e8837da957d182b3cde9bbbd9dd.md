# # Operators

Storing values in variables is all well and good, but computers come into their own when it comes to changing and combining those values. Computers were invented for number-crunching, and they're very good at it!

To manipulate variables, you use operators. This is really just a fancy programming term for plus, minus, divide and multiply, as well as a few others. Plus and minus are written + and - as normal, but multiply is written as * (not ×) and divide is / (not ÷).

However, as well as just adding numbers together and storing them in a variable you can add variables together too. Any place you might use a number on the right-hand side of the equals sign you can put in a variable instead:

```
```text
variable1 = 2 + 5

variable2 = 11 - variable1

variable3 = variable1 * variable2
```
```

> > Be very careful when dividing integers, since the result will be an integer too. So `var2` when `var1` is 5.0 (a floating point) gives 2.5, but when `var1` is 5, an integer gives 2, since it rounds down to the nearest whole number. When dividing integers it's safest to convert to floating point first.

![](bbox=[0.595, 0.067, 0.719, 0.279])

> > variable1 will equal 7

> > variable2 will equal 4

> > variable3 will equal 28