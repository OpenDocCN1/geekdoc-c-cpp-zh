# EXAMPLE 2.18

```
double price = 1089.30;
Console.WriteLine("The price is {0:C}.", price);
// Displays The price is $1,089.30
```

To indicate that you want the value displayed as money with the dollar symbol, comma separators, and two positions to the right of the decimal, the currency format is specified using C or c. The format specifier is placed inside the curly braces ({ }), thus becoming part of the string literal argument for the WriteLine() method.

Notice two values are placed inside the braces. The first value in the curly brace is a placeholder. It indicates which of the arguments that are placed outside of the double quotes you want displayed. The argument formatted in Example 2-18 is price, which is the first argument. You will find that most modern computer programming languages use 0 to reference the first entry. After indicating the argument, you can add an optional format specification. In this case, the currency, C, specifier was added.

NOTE
A string is expected for the first argument to the WriteLine() method.
To increase readability, the statement can be placed on two lines, with the string joined together by the concatenation operator, + sign.

Table 2-15 shows examples using the two most common format specifiers, c and f.

# TABLE 2-15 Examples using format specifiers

| Character | Description | Examples | Output |
|---|---|---|---|
| C or c | Currency | Console.Write("{0:c}", 26666.7888); | $26,666.79 |
| C or c | Currency | Console.Write("{0:c}", -2); | ($2.00) |
| C or c | Currency | Console.Write("{0:c}", 38.8); | $38.80 |
| F or f | Fixed point | Console.Write("{0:F4}", 50); | 50.0000 |
| F or f | Fixed point | Console.Write("{0:F0} {1}", 50, 22); | 50 22 |