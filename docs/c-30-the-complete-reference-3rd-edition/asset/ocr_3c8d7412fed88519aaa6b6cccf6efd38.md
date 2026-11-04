Values containing more digits will be displayed in full on the left side of the decimal point and rounded on the right side.

You can insert commas into large numbers by specifying a pattern that embeds a comma within a sequence of #s. For example, this

```
Console.WriteLine("{0:0,###.#}", 3421.3);
```

displays

3,421.3.

It is not necessary to specify each comma for each position. Specifying one comma causes it to be inserted into the value every third digit from the left of the decimal point. For example,

```
Console.WriteLine("{0:0,###.#}", 8763421.3);
```

produces this output:

8,763,421.3.

Commas have a second meaning. When they occur on the immediate left of the decimal point, they act as a scaling factor. Each comma causes the value to be divided by 1,000. For example,

```
Console.WriteLine("Value in thousands: {0:###,##}", 8763421.3);
```

produces this output:

Value in thousands: 8,763.4

As the output shows, the value is scaled in terms of thousands.

In addition to the placeholders, a custom format specifier can contain other characters. Any other characters are simply passed through, appearing in the formatted string exactly as they appear in the format specifier. For example, this WriteLine() statement:

```
Console.WriteLine("Fuel efficiency is {0:##.# mpg}", 21.3);
```

produces this output:

Fuel efficiency is 21.3 mpg

You can also use the escape sequences, such as \t or \n, if necessary.

The E and e placeholders cause a value to be displayed in scientific notation. At least one 0, but possibly more, must follow the E or e. The 0s indicate the number of decimal digits that will be displayed. The decimal component will be rounded to fit the format. Using an uppercase E causes an uppercase E to be displayed; using a lowercase e causes a lowercase e to be displayed. To ensure that a sign character precedes the exponent, use the E+ or e+. To display a sign character for negative values only, use E-, e-, or e-. The ":" is a separator that enables you to specify different formats for positive, negative, and zero values. Here is the general form of a custom format specifier that uses the ":":

positive-fmt;negative-fmt;zero-fmt