being said, the remainder of the chapter will continue using the inheritance relationship terminology in accordance with the standard C# terminology.

# Multiple Interface Inheritance

Just as classes can implement multiple interfaces, so interfaces can inherit from multiple interfaces. The syntax used for this purpose is consistent with class derivation and implementation, as shown in Listing 8.9.

**LISTING 8.9: Multiple Interface Inheritance**

```
```csharp
interface IReadableSettingsProvider
{
    string GetSetting(string name, string defaultValue);
}

interface IWritableSettingsProvider
{
    void SetSetting(string name, string value);
}

interface ISettingsProvider : IReadableSettingsProvider,
                           IWritableSettingsProvider
{
}
```
```

It is unusual to have an interface with no members, but if implementing both interfaces together is predominant, it is a reasonable choice for this case. The difference between Listing 8.9 and Listing 8.6 is that it is now possible to implement IWritableSettingsProvider without supplying any read capability. Listing 8.6’s FileSettingsProvider is unaffected, but if it used explicit member implementation, specifying the interface to which a member belongs changes slightly.

# Extension Methods on Interfaces

Perhaps one of the most important features of extension methods is the fact that they work with interfaces in addition to classes. The syntax used is identical to that used for extension methods for classes. The extended type (the first parameter and the parameter prefixed with this) is the interface