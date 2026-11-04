As is the case with the Convert methods, this works only if the text can reasonably be converted into a decimal. If the user types “12,345.67,” the parsing works. If the user types “ten” or “1.2,3,” the parsing fails.

> NOTE Unfortunately, C#’s conversion and parsing methods get confused by some formats that you might expect them to understand. For example, they can’t handle currency characters, so they fail on strings like “$12.34” and “€54.32.” You can tell the decimal class’s Parse method to allow currency values by passing it a second parameter, as shown in the following code:

```
decimal salary = decimal.Parse(salaryTextBox.Text, System.Globalization.NumberStyles.Any);
```

# PERFORMING CALCULATIONS

You’ve already seen several pieces of code that assign a value to a variable. For example, the following code converts the text in the salaryTextBox into a decimal and saves it in the variable salary:

```
decimal salary = decimal.Parse(salaryTextBox.Text);
```

You can also save a value that is the result of a more complex calculation into a variable on the left side of an equals sign. Fortunately, the syntax for these kinds of calculations is usually easy to understand. The following code calculates the value 2736 + 7281 / 3 and saves the result in the variable result:

```
double result = 2736 + 7281 / 3;
```

The operands (the values used in the expression on the right) can be literal values, values stored in variables, or the results of methods. For example, the following code calculates the sales tax on a purchase’s subtotal. It multiplies the tax rate stored in the taxRate variable by the decimal value stored in the subtotalTextBox and saves the result in the variable salesTax:

```
decimal salesTax = taxRate * decimal.Parse(subtotalTextBox.Text);
```

Note that a variable can appear on both sides of the equals sign. In that case, the value on the right is the variable’s current value and, after the calculation, the new result is saved back into the same variable.

For example, the following code takes x’s current value, doubles it, adds 10, and saves the result back in variable x. If x started with the value 3, then when this statement finishes x holds the value 16:

```
x = 2 * x + 10;
```

A variable may appear more than once on the right side of the equals sign but it can appear only once on the left.

The following sections provide some additional details about performing calculations.