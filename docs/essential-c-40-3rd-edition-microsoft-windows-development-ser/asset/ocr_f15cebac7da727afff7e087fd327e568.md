Since changing an implementation from implicit to explicit results in a version-breaking change, it is better to err on the side of defining interfaces explicitly, allowing them to be changed to implicit later on. Furthermore, since the decision between implicit and explicit does not have to be consistent across all interface members, defining some methods as explicit and others as implicit is fully supported.

# Converting between the Implementing Class and Its Interfaces

Just as with a derived class and a base type, a conversion from an object to its implemented interface is an implicit conversion. No cast operator is required because an instance of the implementing class will always contain all the members in the interface, and therefore, the object will always cast successfully to the interface type.

Although the conversion will always be successful from the implementing class to the implemented interface, many different classes could implement a particular interface, so you can never be certain that a downward cast from the interface to the implementing class will be successful. The result is that converting from an interface to its implementing class requires an explicit cast.

# Interface Inheritance

Interfaces can derive from each other, resulting in an interface that inherits all the members in its base interfaces. As shown in Listing 7.6, the interfaces directly derived from IReadableSettingsProvider are the explicit base interfaces.

```
LISTING 7.6: Deriving One Interface from Another

interface IReadableSettingsProvider
{
    string GetSetting(string name, string defaultValue);
}

interface ISettingsProvider : IReadableSettingsProvider
{
    void SetSetting(string name, string value);
}
```