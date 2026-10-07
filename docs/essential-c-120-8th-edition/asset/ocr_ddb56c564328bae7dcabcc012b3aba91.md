# Guidelines

DO name custom attribute classes with the suffix Attribute.

# Looking for Attributes

In addition to providing properties for reflecting on a type's members, Type includes methods to retrieve the Attributes decorating that type. Similarly, all the reflection types (e.g., PropertyInfo and MethodInfo) include members for retrieving a list of attributes that decorate a type. Listing 18.14 defines a method to retrieve a list of required switches that are missing from the command line.

Listing 18.14: Retrieving a Custom Attribute

```
using System.Reflection;
using System.Collections.Generic;

public class CommandLineSwitchRequiredAttribute : Attribute
{
    public static string[] GetRequiredOptions(
        object commandLine)
    {
        List<string> missingOptions = new();
        PropertyInfo[] properties = 
            commandLine.GetType().GetProperties();

        foreach (PropertyInfo property in properties)
        {
            Attribute[] attributes = 
                property.GetCustomAttributes(typeof(CommandLineSwitchRequiredAttribute), false);
            if (attributes.Length > 0 && 
                property.GetValue(commandLine, null) == null)
            {
                missingOptions.Add(property.Name);
            }
        }
        return missingOptions.ToArray();
    }
}
```