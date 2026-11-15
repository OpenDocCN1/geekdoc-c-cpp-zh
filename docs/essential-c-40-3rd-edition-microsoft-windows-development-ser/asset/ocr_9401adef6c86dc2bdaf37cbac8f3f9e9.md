```
```csharp
CommandlineSwitchAliasAttribute attribute =
    (CommandlineSwitchAliasAttribute)
    property.GetCustomAttributes(
        typeof(CommandlineSwitchAliasAttribute), false)[0];
if(attribute.Alias == "?")
{
    Console.WriteLine("Help(?)");
};
```
```

Furthermore, as Listing 17.15 and Listing 17.16 demonstrate, you can use similar code in a GetSwitches() method on CommandlineAliasAttribute that returns a dictionary collection of all the switches, including those from the property names, and associate each name with the corresponding attribute on the command-line object.

# LISTING 17.15: Retrieving Custom Attribute Instances

```
```csharp
using System;
using System.Reflection;
using System.Collections.Generic;

public class CommandLineSwitchAliasAttribute : Attribute
{
    public CommandLineSwitchAliasAttribute(string alias)
    {
        Alias = alias;
    }

    public string Alias
    {
        get { return _Alias; }
        set { _Alias = value; }
    }
    private string _Alias;

    public static Dictionary<string, PropertyInfo> GetSwitches(
        object commandLine)
    {
        PropertyInfo[] properties = null;
        Dictionary<string, PropertyInfo> options =
            new Dictionary<string, PropertyInfo>();

        properties = commandLine.GetType().GetProperties(
            BindingFlags.Public | BindingFlags.NonPublic |
            BindingFlags.Instance);

        foreach (PropertyInfo property in properties)
        {
            options.Add(property.Name.ToLower(), property);
```
```