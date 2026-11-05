```
else
    Console.WriteLine("Unknown");
}
}
```

Example: https://dotnetfiddle.net/I5Rwie

# Section 22.9: Adding additional description information to an enum value

In some cases you might want to add an additional description to an enum value, for instance when the enum value itself is less readable than what you might want to display to the user. In such cases you can use the System.ComponentModel.DescriptionAttribute class.

For example:

```
public enum PossibleResults
{
    [Description("Success")]
    OK = 1,
    [Description("File not found")]
    FileNotFound = 2,
    [Description("Access denied")]
    AccessDenied = 3
}
```

Now, if you would like to return the description of a specific enum value you can do the following:

```
public static string GetDescriptionAttribute(PossibleResults result)
{
    return ((DescriptionAttribute)Attribute.GetCustomAttribute((result.GetType().GetField(result.ToString())), typeof(DescriptionAttribute))).Description;
}

static void Main(string[] args)
{
    PossibleResults result = PossibleResults.FileNotFound;
    Console.WriteLine(result); // Prints "FileNotFound"
    Console.WriteLine(GetDescriptionAttribute(result)); // Prints "File not found"
}
```

This can also be easily transformed to an extension method for all enums:

```
static class EnumExtensions
{
    public static string GetDescription(this Enum enumValue)
    {
        return ((DescriptionAttribute)Attribute.GetCustomAttribute((enumValue.GetType().GetField(enumValue.ToString())), typeof(DescriptionAttribute))).Description;
    }
}
```

And then easily used like this: Console.WriteLine(result.GetDescription());