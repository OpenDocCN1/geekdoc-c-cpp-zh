
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

Here is an example:

```
Console.WriteLine("{0:#.##;(#.##);0.00}", num);
```

If num is positive, the value is displayed with two decimal places. If num is negative, the value is displayed with two decimal places and is between a set of parentheses. If num is zero, the string 0.00 is displayed. When using the separators, you don't need to supply all parts. If you just want to specify how positive and negative values will look, omit the zero format. To use the default for negative values, omit the negative format. In this case, the positive format and the zero format will be separated by two semicolons.

The following program demonstrates just a few of the many possible custom formats that you can create:

```
// Using custom formats.
using System;
class PictureFormatDemo {
    static void Main() {
        double num = 64354.2345;
        Console.WriteLine("Default format: " + num);
        // Display with 2 decimal places.
        Console.WriteLine("Value with two decimal places: " +
            "{0:#.##}", num);
        // Display with commas and 2 decimal places.
        Console.WriteLine("Add commas: {0:##,##0.##}", num);
        // Display using scientific notation.
        Console.WriteLine("Use scientific notation: " +
            "{0:#.###E+00}", num);
        // Scale the value by 1000.
        Console.WriteLine("Value in 1,000s: " +
            "{0:#0,}", num);
        /* Display positive, negative, and zero
        values differently. */
        Console.WriteLine("Display positive, negative, " +
            "and zero values differently.");
        Console.WriteLine("{0:#.##;(#.##);0.00}", num);
        num = -num;
        Console.WriteLine("{0:#.##;(#.##);0.00}", num);
        num = 0.0;
        Console.WriteLine("{0:#.##;(#.##);0.00}", num);
        // Display a percentage.
        num = 0.17;
        Console.WriteLine("Display a percentage: {0:#%}", num);
    }
}
```

| Placeholder | Meaning |
|---|---|
| # | Digit |
| . | Decimal point |
| , | Thousands separator |
| % | Percentage, which is the value being formatted multiplied by 100 |
| 0 | Pads with leading and trailing zeros |
| ; | Separates sections that describe the format for positive, negative, and zero values |
| E0 E+0 E-0 e0 e+0 e-0 | Scientific notation |

TABLE 22-6 Custom Format Placeholder Characters

The output is shown here:

```
Default format: 64354.2345
Value with two decimal places: 64354.23
Add commas: 64,354.23
Use scientific notation: 6.435e+04
Value in 1,000s: 64
Display positive, negative, and zero values differently.
64354.2
(64354.23)
0.00
Display a percentage: 17%
```

## Formatting Date and Time

In addition to formatting numeric values, another data type to which formatting is often applied is DateTime. DateTime is a structure that represents date and time. Date and time values can be displayed a variety of ways. Here are just a few examples:

- 06/05/2006
- Monday, June 5, 2006
- 12:59:00
- 12:59:00 PM

Also, the date and time representations can vary from country to country. For these reasons, the .NET Framework provides an extensive formatting subsystem for time and date values. Date and time formatting is handled through format specifiers. The format specifiers for date and time are shown in Table 22-7. Because the specific date and time representation may vary from country to country and by language, the precise representation generated will be influenced by the cultural settings.

| Specifier | Format |
|---|---|
| D | Date in long form. |
| d | Date in short form. |
| F | Date and time in long form. |
| f | Date and time in short form. |
| G | Date in short form, time in long form. |
| gg | Date in short form, time in short form. |
| M | Month and day. |
| m | Same as M. |
| O | A form of date and time that includes the time zone. The string produced by the O format can be parsed back into the equivalent date and time. This is called the "round trip" format. |
| o | Same as O. |
| R | Date and time in standard, GMT form. |
| r | Same as R. |
| s | A sortable form of date and time. |
| T | Time in long form. |
| t | Time in short form. |
| U | Long form, universal form of date and time. Time is displayed as UTC. |
| u | Short form, universal form of date and time. |
| Y | Month and year. |
| y | Same as Y. |

TABLE 22-7 The Date and Time Format Specifiers

Here is a program that demonstrates the date and time format specifiers:

```
// Format time and date information.
using System;

class TimeAndDateFormatDemo {
    static void Main() {
        DateTime dt = DateTime.Now; // obtain current time

        Console.WriteLine("d format: {0:d}", dt);
        Console.WriteLine("D format: {0:D}", dt);

        Console.WriteLine("t format: {0:t}", dt);
        Console.WriteLine("T format: {0:T}", dt);

        Console.WriteLine("f format: {0:f}", dt);
        Console.WriteLine("F format: {0:F}", dt);
    }
}
```

```
Console.WriteLine("g format: {0:g}", dt);
Console.WriteLine("G format: {0:G}", dt);

Console.WriteLine("m format: {0:m}", dt);
Console.WriteLine("M format: {0:M}", dt);

Console.WriteLine("o format: {0:o}", dt);
Console.WriteLine("O format: {0:O}", dt);

Console.WriteLine("r format: {0:r}", dt);
Console.WriteLine("R format: {0:R}", dt);

Console.WriteLine("s format: {0:s}", dt);

Console.WriteLine("u format: {0:u}", dt);
Console.WriteLine("U format: {0:U}", dt);

Console.WriteLine("y format: {0:y}", dt);
Console.WriteLine("Y format: {0:Y}", dt);
}
```

Sample output is shown here:

```
d format: 6/18/2008
D format: Wednesday, June 18, 2008
t format: 11:53 AM
T format: 11:53:09 AM
f format: Wednesday, June 18, 2008 11:53 AM
F format: Wednesday, June 18, 2008 11:53:09 AM
g format: 6/18/2008 11:53 AM
G format: 6/18/2008 11:53:09 AM
m format: June 18
M format: June 18
o format: 2008-06-18T11:53:09.5074933-05:00
O format: 2008-06-18T11:53:09.5074933-05:00
r format: Wed, 18 Jun 2008 11:53:09 GMT
R format: Wed, 18 Jun 2008 11:53:09 GMT
s format: 2008-06-18T11:53:09
u format: 2008-06-18 11:53:09Z
U format: Wednesday, June 18, 2008 4:53:09 PM
y format: June, 2008
Y format: June, 2008
```

The next program creates a very simple clock. The time is updated once every second. At the top of each hour, the computer’s bell is sounded. It uses the ToString() method of DateTime to obtain the formatted time prior to outputting it. If the top of the hour has been reached, then the alert character (\a) is appended to the formatted time, thus ringing the bell.

// A simple clock.

using System;

class SimpleClock {
    static void Main() {
        string t;
