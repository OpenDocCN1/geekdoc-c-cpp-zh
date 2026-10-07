# Chapter 18: Reflection, Attributes, and Dynamic Programming

# OUTPUT 18.5

```
[assembly: AssemblyCompany("Addison Wesley")
[assembly: AssemblyCopyright("Copyright © Addison Wesley 2020")
[assembly: AssemblyFileVersion("8.0.0.0")
[assembly: AssemblyInformationalVersion("8.0.0")
[assembly: AssemblyProduct("Essential C# 8.0")
[assembly: AssemblyVersion("8.0.0.0")
```

# Guidelines

**DO** apply AssemblyVersionAttribute to assemblies with public types.

**CONSIDER** applying AssemblyFileVersionAttribute and AssemblyCopyrightAttribute to provide additional information about the assembly.

**DO** apply the following information attributes:
System.Reflection.AssemblyCompanyAttribute,
System.Reflection.AssemblyCopyrightAttribute,
System.Reflection.AssemblyDescriptionAttribute, and
System.Reflection.AssemblyProductAttribute.

# Custom Attributes

Defining a custom attribute is relatively trivial. Attributes are objects; therefore, to define an attribute, you need to define a class. The characteristic that turns a general class into an attribute is that it derives from System.Attribute. Consequently, you can create a CommandLineSwitchRequiredAttribute class, as shown in Listing 18.13.

Listing 18.13: Defining a Custom Attribute

```
public class CommandLineSwitchRequiredAttribute : Attribute
{
}
```

With simple definition, you can now use the attribute as demonstrated in Listing 18.8. So far, no code responds to the attribute; therefore, the Out property that includes the attribute will have no effect on command-line parsing.