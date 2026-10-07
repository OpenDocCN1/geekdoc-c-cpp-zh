# Chapter 18: Reflection, Attributes, and Dynamic Programming

Listing 18.3, you dynamically set a class's properties based on the command-line option matching the property name. This approach is insufficient, when when the command-line option is an invalid property name. The command-line option /?, for example, cannot be supported. Furthermore, this mechanism doesn't provide any way of identifying which options are required versus which are truly optional.

Instead of relying on an exact match between the option and the property name, you can use attributes to identify additional metadata about the decorated construct—in this case, the option that the attribute decorates. With attributes, you can decorate a property as Required and provide a ? option alias. In other words, attributes are a means of associating additional data with a property (and other constructs).

Attributes appear within square brackets pre preced the construct they decorate. For example, you can modify the CommandLineInfo class to include attributes, as shown in Listing 18.8.

# Listing 18.8: Decorating a Property with an Attribute

```
public class CommandLineInfo{
    [CommandLineSwitchAlias("?*\)]
    public bool Help { get; set; }

    [CommandLineSwitchRequired]
    public string? Out { get; set; }

    public System.Diagnostics.ProcessPriorityClass Priority
        { get; set; } = System.Diagnostics.ProcessPriorityClass.Normal;
}
```

In Listing 18.8, the Help and Out properties are decorated with attributes. These attributes have two purposes: They allow an alias of ? for /Help, and they indicate that /Out is a required parameter. The idea is that from within the CommandLineHandler.TryParse() method, you enable support for option aliases, assuming the parsing was successful, you check that all required switches were specified.