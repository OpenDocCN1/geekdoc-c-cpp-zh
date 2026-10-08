# **Try It Yourself**

# **String Comparison**

To perform different string comparisons, follow these steps. If you closed Visual Studio, repeat the previous exercise first. Be sure to keep Visual Studio open at the end of this exercise because you will use this application later.

1.  In the **Main** method of the Program.cs file, enter the following statements:

```
Console.WriteLine(original.StartsWith("quick"));
Console.WriteLine(substring2.StartsWith("quick"));
Console.WriteLine(substring.EndsWith("fox"));
Console.WriteLine(original.CompareTo(original));
Console.WriteLine(String.Compare(substring2, "Quick"));
Console.WriteLine(original.Contains(substring2));
```

2.  Run the application using Ctrl+F5 and observe that the output matches what is shown in Figure 8.2.

![](bbox=[0.05, 0.43, 0.14, 0.51])

![](bbox=[0.33, 0.43, 0.74, 0.58])

The standard way to normalize case is to use the ToUpperInvariant method, which creates an all-uppercase representation of the string using the casing rules of the invariant culture. To create an all-lowercase representation, it is preferred that you use the ToLowerInvariant method, which uses the casing rules of the invariant culture. In addition to the invariant methods, you can also use the ToUpper and ToLower methods, which use the casing rules of either the current culture or the specified culture, depending on which overload you use.

# **Modifying Parts of a String**

Although performing string comparisons is common, sometimes you need to modify all or part of a string. Because strings are immutable, these methods actually return a new string rather than modifying the current one.

To remove whitespace and other characters from a string, you can use the Trim, TrimEnd, or TrimStart methods. TrimEnd and TrimStart remove whitespace from