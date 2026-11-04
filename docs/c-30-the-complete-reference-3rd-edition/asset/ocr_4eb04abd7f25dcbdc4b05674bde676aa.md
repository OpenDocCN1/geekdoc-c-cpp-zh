| Value | Squared | Cubed |
|---|---|---|
| 1 | 1 | 1 |
| 2 | 4 | 8 |
| 3 | 9 | 27 |
| 4 | 16 | 64 |
| 5 | 25 | 125 |
| 6 | 36 | 216 |
| 7 | 49 | 343 |
| 8 | 64 | 512 |
| 9 | 81 | 729 |

In the preceding examples, no formatting was applied to the values themselves. Of course, the purpose of using format specifiers is to control the way the data looks. The types of data most commonly formatted are floating-point and decimal values. One of the easiest ways to specify a format is to describe a template that WriteLine( ) will use. To do this, show an example of the format that you want, using #s to mark the digit positions. You can also specify the decimal point and commas. For example, here is a better way to display 10 divided by 3:

```
```csharp
Console.WriteLine("Here is 10/3: {0:#.##}", 10.0/3.0);
```
```

The output from this statement is shown here:

```
```
Here is 10/3: 3.33
```
```

In this example, the template is #.##, which tells WriteLine( ) to display two decimal places. It is important to understand, however, that WriteLine( ) will display more than one digit to the left of the decimal point, if necessary, so as not to misrepresent the value. Here is another example. This statement

```
```csharp
Console.WriteLine("{0:##,###.##}", 123456.56);
```
```

generates this output:

```
```
123,456.56
```
```

If you want to display monetary values, use the C format specifier. For example:

```
```csharp
decimal balance;

balance = 12323.09m;
Console.WriteLine("Current balance is {0:C}", balance);
```
```

The output from this sequence is shown here (in U.S. dollar format):

```
```
Current balance is $12,323.09
```
```

The C format can be used to improve the output from the price discount program shown earlier:

```
```csharp
// Use the C format specifier to output dollars and cents.

using System;
```
```