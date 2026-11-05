The examples in Tables 2-16 and 2-17 show how the format specifiers can be used as arguments to the Console.Write() or Console.WriteLine() methods. They can also be stored in a string variable and then used as arguments to methods such as the ToString() method. In Chapter 3, you will read about creating your own methods and using many of the predefined ones that are part of the C# language.

# Width Specifier

You may specify a width as part of the format specifier. This is especially useful when you want to control the alignment of items on multiple lines. Add the Alignment component following the index ordinal before the colon. A comma is used as a separator. If the number value of alignment is less than the actual length of the formatted string, alignment is ignored and the length of the actual formatted string is used as the field width. Consider the following example:

```
Console.WriteLine("{0,10:F0} {1,8:C} ", 9, 14);
```

The result is as follows:

```
9      $14.00
```

The formatted data in the field is right-aligned if alignment number value is positive and left-aligned if alignment number value is negative. If padding is necessary, white space is used. The comma is required if alignment is specified.

Consider the following example:

```
Console.WriteLine("{0,-10:F0} {1,8:C} ", 9, 14);
```

The result is as follows:

```
9          $14.00
```

Here the first argument (9) is left justified because the alignment component is negative.