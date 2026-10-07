```
#region IReadableSettingsProvider Members
public string GetSetting(string name, string defaultValue)
{
    // ...
}
#endregion
```

In this listing, there is no change to the interface's implementations on the class. Although the additional interface implementation declaration on the class header is superfluous, it provides for better readability.

The decision to provide multiple interfaces rather than just one combined interface depends largely on what the interface designer wants to require of the implementing class. By providing an IReadableSettingsProvider interface, the designer communicates that implementers are required only to implement a settings provider that retrieves settings; they do not have to be able to write to those settings. This reduces the implementation burden by not imposing the complexities of writing settings as well.

In contrast, implementing ISettingsProvider assumes that there is never a reason to have a class that can write settings without reading them. The inheritance relationship between ISettingsProvider and IReadableSettingsProvider, therefore, forces the combined total of both interfaces on the ISettingsProvider class.

One final but important note: Although inheritance is the correct term, conceptually it is more accurate to say that an interface represents a contract, and one contract can specify that the properties of another contract must also be followed. So, the code ISettingsProvider : IReadableSettingsProvider conceptually states that the ISettingsProvider contract requires also respecting the IReadableSettingsProvider contract, rather than that the ISettingsProvider “is a kind of” IReadableSettingsProvider. That being said, the remainder of the chapter will continue using the inheritance relationship terminology in accordance with the standard C# terminology.