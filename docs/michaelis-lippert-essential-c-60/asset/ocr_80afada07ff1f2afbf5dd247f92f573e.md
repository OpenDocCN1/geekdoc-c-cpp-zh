# LISTING 17.12: Defining a Custom Attribute

```
public class CommandLineSwitchRequiredAttribute : Attribute
{
}
```

With that simple definition, you now can use the attribute as demonstrated in Listing 17.8. So far, no code responds to the attribute; therefore, the Out property that includes the attribute will have no effect on command-line parsing.

# Guidelines

DO name custom attribute classes with the suffix “Attribute”.

# Looking for Attributes

In addition to providing properties for reflecting on a type’s members, Type includes methods to retrieve the Attributes decorating that type. Similarly, all the reflection types (PropertyInfo and MethodInfo, for example) include members for retrieving a list of attributes that decorate a type. Listing 17.13 defines a method to return a list of required switches that are missing from the command line.

# LISTING 17.13: Retrieving a Custom Attribute

```
using System;
using System.Collections.Specialized;
using System.Reflection;

public class CommandLineSwitchRequiredAttribute : Attribute
{
    public static string[] GetMissingRequiredOptions(
        object commandLine)
    {
        List<string> missingOptions = new List<string>();
        PropertyInfo[] properties =
            commandLine.GetType().GetProperties();

        foreach (PropertyInfo property in properties)
        {
            Attribute[] attributes =
                (Attribute[])property.GetCustomAttributes(
                    typeof(CommandLineSwitchRequiredAttribute),
                    false);
            if ((attributes.Length > 0) &&
                (property.GetValue(commandLine, null) == null))
```