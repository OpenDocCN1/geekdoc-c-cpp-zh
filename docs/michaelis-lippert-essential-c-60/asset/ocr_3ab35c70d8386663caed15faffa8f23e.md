```
if ((optionParts.Length < 2)
    || optionParts[1] == ""
    || optionParts[1] == ":")
{
    // No setting was provided for the switch.
    success = false;
    errorMessage = string.Format(
        "You must specify the value for the {0} option.",
        property.Name);
}
else if (
    property.PropertyType == typeof(string))
{
    property.SetValue(
        commandLine, optionParts[1], null);
    success = true;
}
else if (property.PropertyType.IsEnum)
{
    success = TryParseEnumSwitch(
        commandLine, optionParts,
        property, ref errorMessage);
}
else
{
    success = false;
    errorMessage = string.Format(
        "Data type '{0}' on {1} is not supported.",
        property.PropertyType.ToString(),
        commandLine.GetType().ToString());
}
}
return success;
}
```

# Guidelines

DO provide get-only properties (with private setters) on attributes with required property values.

DO provide constructor parameters to initialize properties on attributes with required properties. Each parameter should have the same name (albeit with different casing) as the corresponding property.

AVOID providing constructor parameters to initialize attribute properties corresponding to the optional arguments (and therefore, avoid overloading custom attribute constructors).