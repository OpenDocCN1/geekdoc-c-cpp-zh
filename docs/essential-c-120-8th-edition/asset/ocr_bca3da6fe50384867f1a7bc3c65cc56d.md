# LISTING 18.11: Specifying a Return Attribute

```
[return: Description(
  "Returns true if the object is in a valid state.")
public bool IsValid(
{
  // ...
  return true;
}
```

In addition to assembly and return:, C allows for explicit target identifications of module:, class:, and method:, corresponding to attributes that decorate the module, class, and method, respectively. class: and method;: however, are optional, as demonstrated earlier.

One of the conveniences of using attributes is that the language takes into consideration the attribute naming convention, which calls for Attribute to appear at the end of the name. However, in all attribute uses in the preceding listings, no such suffix appears, even though each attribute follows the naming convention. This is because although the full name (DescriptionAttribute, AssemblyVersionAttribute, and so on) is allowed when applying an attribute, C# makes the suffix optional. Generally, no such suffix appears when applying an attribute; rather, it appears only when defining one or using the attribute inline (such as typeof(DescriptionAttribute)).

Note that instead of generating an AssemblyInfo.cs file,.NET Core-based projects allow specification of the assembly information within the *.csproj file. Listing 18.12, for example, injects corresponding assembly attributes into the assembly at compile time. The results are shown in Output 18.5.

# LISTING 18.12: Defining a Custom Attribute

```
<Project>
  <PropertyGroup>
    <Company>Addison Wesley</Company>
    <Copyright>Copyright © Addison Wesley 2020</Copyright>
    <Product>Essential C# 8.0</Product>
    <Version>8.0</Version>
  </PropertyGroup>
</Project>
```