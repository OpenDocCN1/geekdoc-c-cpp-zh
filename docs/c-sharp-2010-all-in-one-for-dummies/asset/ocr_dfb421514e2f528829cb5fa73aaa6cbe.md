The same number — % — may appear this way when expressed as a double:

```
    0.55555555555555557823
```

The double packs a whopping 15 to 16 significant digits.

Use double variable types unless you have a specific reason to do otherwise.

![](bbox=[0.06, 0.177, 0.14, 0.24])

# ## Converting some more temperatures

Here’s the formula for converting from Fahrenheit to Celsius temperatures using floating-point variables:

```
    double celsius = (fahr - 32.0) * (5.0 / 9.0)
```

![](bbox=[0.06, 0.333, 0.14, 0.42])

The Web site contains a floating-point version of the temperature-conversion program called ConvertTemperatureWithFloat.

The following example shows the result of executing the double-based ConvertTemperatureWithFloat program:

```
    Enter temp in degrees Fahrenheit:100
    Temperature in degrees Celsius = 37.77777777777778
    Press Enter to terminate...
```

# ## Examining some limitations of floating-point variables

You may be tempted to use floating-point variables all the time because they solve the truncation problem so nicely. Sure, they use up a bit more memory. But memory is cheap these days, so why not? But floating-point variables also have limitations, which I discuss in the following sections.

# ### Counting

You can’t use floating-point variables as counting numbers. Some C# structures need to count (as in 1, 2, 3, and so on). You know that 1.0, 2.0, and 3.0 are counting numbers just as well as 1, 2, and 3, but C# doesn’t know that. For example, given the accuracy limitations of floating-points, how does C# know that you aren’t actually saying 1.000001?

![](bbox=[0.06, 0.788, 0.14, 0.87])

Whether you find that argument convincing, you can’t use a floating-point variable when counting things.

# ### Comparing numbers

You have to be careful when comparing floating-point numbers. For example, 12.5 may be represented as 12.500001. Most people don’t care about that little extra bit on the end. However, the computer takes things extremely literally. To C#, 12.500000 and 12.500001 are not the same numbers.

Book I  
Chapter 2  
Living with Variability  
— Declaring  
Value-Type Variables