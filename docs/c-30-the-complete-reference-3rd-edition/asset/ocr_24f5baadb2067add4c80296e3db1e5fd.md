# Using the Substring() Method

You can obtain a portion of a string by using the Substring() method. It has these two forms:

```
public string Substring(int idx)
public string Substring(int idx, int count)
```

In the first form, the substring begins at the index specified by idx and runs to the end of the invoking string. In the second form, the substring begins at idx and runs for count characters. In each case, the substring is returned.

The following program demonstrates the Substring() method:

```
// Use Substring().

using System;

class SubstringDemo {
    static void Main() {
        string str = "ABCDEFGHIJKLMNOPQRSTUVWXYZ";

        Console.WriteLine("str: " + str);

        Console.Write("str.Substring(15): ");
        string substr = str.Substring(15);
        Console.WriteLine(substr);

        Console.Write("str.Substring(0, 15): ");
        substr = str.Substring(0, 15);
        Console.WriteLine(substr);
    }
}
```

The following output is produced:

```
str: ABCDEFGHIJKLMNOPQRSTUVWXYZ
str.Substring(15): PQRSTUVWXYZ
str.Substring(0, 15): ABCDEFGHIJKLMNO
```

# The String Extension Methods

As mentioned earlier, String implements IEnumerable<T>. This means that beginning with C# 3.0, a String object can call the extension methods defined by Enumerable and Queryable, which are both in the System.Linq namespace. These extension methods primarily provide support for LINQ, but some can also be used for other purposes, such as certain types of string handling. See Chapter 19 for a discussion of extension methods.

# Formatting

When a human-readable form of a built-in type, such as int or double, is needed, a string representation must be created. Although C# automatically supplies a default format for this representation, it is also possible to specify a format of your own choosing. For example, as you saw in Part I, it is possible to output numeric data using a dollars and cents format. A number