# System.AttributeUsageAttribute

Most attributes are intended to decorate only particular constructs. For example, it makes no sense to allow CommandLineOptionAttribute to decorate a class or an assembly. The attribute in those contexts would be meaningless. To avoid inappropriate use of an attribute, custom attributes can be decorated with System.AttributeUsageAttribute. Listing 17.18 (for CommandLineOptionAttribute) demonstrates how to do this.

# LISTING 17.18: Restricting the Constructs an Attribute Can Decorate

```
[AttributeUsage(AttributeTargets.Property)]
public class CommandLineSwitchAliasAttribute : Attribute
{
    // ...
}
```

If the attribute is used inappropriately, as it is in Listing 17.19, it will cause a compile-time error, as Output 17.5 demonstrates.

# LISTING 17.19: AttributeUsageAttribute Restricting Where to Apply an Attribute

```
// ERROR: The attribute usage is restricted to properties
[CommandLineSwitchAlias("?")]
class CommandLineInfo
{
}
```

# OUTPUT 17.5

```
...Program+CommandLineInfo.cs(24,17): error CS0592: Attribute 'CommandLineSwitchAlias' is not valid on this declaration type. It is valid on 'property', indexer' declarations only.
```

AttributeUsageAttribute’s constructor takes an AttributeTargets flag. This enum provides a list of all possible targets that the runtime allows an attribute to decorate. For example, if you also allowed CommandLineSwitchAliasAttribute on a field, you would update the AttributeUsageAttribute class as shown in Listing 17.20.

# LISTING 17.20: Limiting an Attribute’s Usage with AttributeUsageAttribute

```
// Restrict the attribute to properties and methods
[AttributeUsage(
    AttributeTargets.Field | AttributeTargets.Property)]
```