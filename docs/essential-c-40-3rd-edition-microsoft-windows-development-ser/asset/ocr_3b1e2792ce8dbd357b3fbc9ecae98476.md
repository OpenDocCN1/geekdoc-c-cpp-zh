The assembly attributes define things such as company, product, and assembly version number. Similar to assembly, identifying an attribute usage as module requires prefixing it with module:. The restriction on assembly and module attributes is that they appear after the using directive but before any namespace or class declarations.

Return attributes, such as the one shown in Listing 17.10, appear before a method declaration but use the same type of syntax structure.

# LISTING 17.10: Specifying a Return Attribute

```
[return: Description("Returns true if the object is in a valid state.")]
public bool IsValid()
{
    // ...
    return true;
}
```

In addition to assembly: and return:, C# allows for explicit target identifications of module:, class:, and method:, corresponding to attributes that decorate the module, class, and method. class: and method:, however, are optional, as demonstrated earlier.

One of the conveniences of using attributes is that the language takes into consideration the attribute naming convention, which is to place Attribute at the end of the name. However, in all the attribute uses in the preceding listings, no such suffix appears, despite the fact that each attribute used follows the naming convention. This is because although the full name (DescriptionAttribute, AssemblyVersionAttribute, and so on) is allowed when applying an attribute, C# makes the suffix optional. Generally, no such suffix appears when applying an attribute; it appears only when defining one or using the attribute inline (such as typeof(DescriptionAttribute)).

# Custom Attributes

Defining a custom attribute is relatively trivial. Attributes are objects; therefore, to define an attribute, you need to define a class. The characteristic that turns a general class into an attribute is that it derives from System.Attribute. Therefore, you can create a CommandLineSwitchRequiredAttribute class, as shown in Listing 17.11.