```
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

# System.AttributeUsageAttribute

Most attributes are intended to decorate only particular constructs. For example, it makes no sense to allow CommandLineOptionAttribute to decorate a class or an assembly. Those contexts would be meaningless. To avoid inappropriate use of an attribute, custom attributes can be decorated with System.AttributeUsageAttribute. Listing 17.17 (for CommandLineOptionAttribute) demonstrates how to do this.

# LISTING 17.17: Restricting the Constructs an Attribute Can Decorate

```
[AttributeUsage(AttributeTargets.Property)]
public class CommandLineSwitchAliasAttribute : Attribute
{
    // ...
}
```

If the attribute is used inappropriately, as it is in Listing 17.18, it will cause a compile-time error, as Output 17.5 demonstrates.

# LISTING 17.18: AttributeUsageAttribute Restricting Where to Apply an Attribute

```
// // ERROR: The attribute usage is restricted to properties
[CommandLineSwitchAlias("**")]
class CommandLineInfo
{
}
```

# OUTPUT 17.5:

```
..\Program\CommandLineInfo.cs(24,17): error CS0592: Attribute
'CommandLineSwitchAlias' is not valid on this declaration type. It is
valid on 'property, indexer' declarations only.
```