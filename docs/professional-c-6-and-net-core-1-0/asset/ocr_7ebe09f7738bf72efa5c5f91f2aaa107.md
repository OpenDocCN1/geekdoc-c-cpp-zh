StringFormats/Program.cs):

```
string s1 ="World";
string s2 = $"Hello, {s1}";
```

In reality, this is just syntax sugar. From strings with the $ prefix, the compiler creates invocations to the String.Format method. So the previous code snippet gets translated to this:

```
string s1 ="World";
string s2 = String.Format("Hello, {0}", s1);
```

The first parameter of the String.Format method that is used accepts a format string with placeholders that are numbered starting from 0, followed by the parameters that are put into the string holes.

The new string format is just a lot handier and doesn’t require that much code to write.

It’s not just variables you can use to fill in the holes of the string. Any method that returns a value can be used:

```
string s2 = $"Hello, {s1.ToUpper()}";
```

This translates to a similar statement:

```
string s2 = String.Format("Hello, {0}", s1.ToUpper());
```

It’s also possible to have multiple holes in the string, like so:

```
int x = 3, y = 4;
string s3 = $"The result of {x} + {y} is {x + y}";
```

which translates to

```
string s3 = String.Format("The result of {0} and {1} is {2}", x, y, x + y);
```

# FormattableString

What the interpolated string gets translated to can easily be seen by assigning the string to a FormattableString. The interpolated string can be directly assigned because the FormattableString is a better match than the normal string. This type defines a Format property that returns the resulting format string, an ArgumentCount property, and the method GetArgument to return the values:

```
int x = 3, y = 4;
FormattableString s = $"The result of {x} + {y} is {x + y}";
WriteLine($"format: {s.Format}");
for (int i = 0; i < s.ArgumentCount; i++)
{
    WriteLine($"argument {i}: {s.GetArgument(i)}");
}
```

Running this code snippet results in this output:

```
format: The result of {0} + {1} is {2}
argument 0: 3
argument 1: 4
```