# Chapter 12: String.Format

| Parameter | Details |
|---|---|
| format | A composite format string, which defines the way args should be combined into a string. |
| args | A sequence of objects to be combined into a string. Since this uses a params argument, you can either use a comma-separated list of arguments or an actual object array. |
| provider | A collection of ways of formatting objects to strings. Typical values include CultureInfo.InvariantCulture and CultureInfo.CurrentCulture. |

The Format methods are a set of overloads in the System.String class used to create strings that combine objects into specific string representations. This information can be applied to String.Format, various WriteLine methods as well as other methods in the .NET framework.

# Section 12.1: Since C# 6.0

Version ≥ 6.0

Since C# 6.0 it is possible to use string interpolation in place of String.Format.

```
string name = "John";
string lastname = "Doe";
Console.WriteLine($"Hello {name} {lastname}!");
```

> Hello John Doe!

More examples for this under the topic C# 6.0 features: String interpolation.

# Section 12.2: Places where String.Format is ‘embedded’ in the framework

There are several places where you can use String.Format indirectly: The secret is to look for the overload with the signature string format, params object[] args, e.g.:

# Section 12.3: Create a custom format provider