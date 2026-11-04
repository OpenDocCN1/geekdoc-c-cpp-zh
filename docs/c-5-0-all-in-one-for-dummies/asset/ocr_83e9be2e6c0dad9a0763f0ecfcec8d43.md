![](bbox=[0.12, 0.14, 0.22, 0.27])

You might think float is the default floating-point variable type, but actually the double is the default in C#. If you don’t specify the type for, say, 12.3, C# calls it a double.

The Accuracy column in Table 2-2 refers to the number of significant digits that such a variable type can represent. For example, ⅔ is actually 0.555… with an unending sequence of 5s. However, a float variable is said to have six significant digits of accuracy — which means numbers after the sixth digit are ignored. Thus ⅔ may appear this way when expressed as a float:

```
0.555551457382
```

Here you know that all the digits after the sixth 5 are untrustworthy.

The same number — ⅔ — may appear this way when expressed as a double:

```
0.5555555555555557823
```

![](bbox=[0.12, 0.54, 0.22, 0.68])

The double packs a whopping 15 to 16 significant digits.

Use double variable types unless you have a specific reason to do otherwise.

# Converting some more temperatures

Here’s the formula for converting from Fahrenheit to Celsius temperatures using floating-point variables:

```
double celsius = (fahr - 32.0) * (5.0 / 9.0)
```

![](bbox=[0.12, 0.78, 0.22, 0.92])

The website contains a floating-point version of the temperature-conversion program called ConvertTemperatureWithFloat.

The following example shows the result of executing the double-based ConvertTemperatureWithFloat program:

```
Enter temp in degrees Fahrenheit:100
Temperature in degrees Celsius = 37.77777777778
Press Enter to terminate...
```

# Examining some limitations of floating-point variables

You may be tempted to use floating-point variables all the time because they solve the truncation problem so nicely. Sure, they use up a bit more memory. But memory is cheap these days, so why not? But floating-point variables also have limitations, which I discuss in the following sections.