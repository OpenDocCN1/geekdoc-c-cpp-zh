Here, argnum specifies the number of the argument (starting from zero) to display. The minimum width of the field is specified by width, and the format is specified by fmt. The width and fmt are optional.

During execution, when a format specifier is encountered in the format string, the corresponding argument, as specified by argnum, is substituted and displayed. Thus, the position of a format specification within the format string determines where its matching data will be displayed. Both width and fmt are optional. Therefore, in its simplest form, a format specifier simply indicates which argument to display. For example, {0} indicates arg0, {1} specifies arg1, and so on.

Let’s begin with a simple example. The statement

```
```csharp
Console.WriteLine("February has {0} or {1} days.", 28, 29);
```
```

produces the following output:

```
```text
February has 28 or 29 days.
```
```

As you can see, the value 28 is substituted for {0}, and 29 is substituted for {1}. Thus, the format specifiers identify the location at which the subsequent arguments, in this case 28 and 29, are displayed within the string. Furthermore, notice that the additional values are separated by commas, not + signs.

Here is a variation of the preceding statement that specifies minimum field widths:

```
```csharp
Console.WriteLine("February has {0,10} or {1,5} days.", 28, 29);
```
```

It produces the following output:

```
```text
February has       28 or    29 days.
```
```

As you can see, spaces have been added to fill out the unused portions of the fields. Remember, a minimum field width is just that: the minimum width. Output can exceed that width if needed.

Of course, the arguments associated with a format command need not be constants. For example, this program displays a table of squares and cubes. It uses format commands to output the values.

```
```csharp
// Use format commands.

using System;

class DisplayOptions {
    static void Main() {
        int i;

        Console.WriteLine("Value\tSquared\tCubed");

        for(i = 1; i < 10; i++)
            Console.WriteLine("{0}\t{1}\t{2}", i, i*i, i*i*i);
    }
}
```
```

The output is shown here: