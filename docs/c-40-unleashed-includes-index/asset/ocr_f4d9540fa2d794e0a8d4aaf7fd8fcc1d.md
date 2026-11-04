The preceding code is turned into this equivalent:

```
```csharp
class Person
{
    private string <Name>k__BackingField;
    private int <Age>k__BackingField;

    public string Name
    {
        get { return <Name>k__BackingField; }
        set { <Name>k__BackingField = value; }
    }

    public int Age
    {
        get { return <Age>k__BackingField; }
        set { <Age>k__BackingField = value; }
    }
}
```
```

Although the accessibility of the generated get and set accessor can be specified, it's not possible to declare the backing fields as read-only. I hope that this little feature omission gets rectified in a future release of the language, maybe as part of larger immutability crusades undertaken by the language designers. Auto-implemented properties can easily be inserted in Visual Studio by using the prop snippet. Type prop and press Tab twice, as shown in Figure 11.12.

![](bbox=[0.034, 0.507, 0.282, 0.566])

FIGURE 11.12 Auto-implemented property snippet in Visual Studio 2010.

# ## How Properties Work

Properties are nothing but one or two accessor *methods* that are grouped together by a piece of metadata. This allows code editors and runtime services like reflection to see them as a unique kind of member. Some other languages don't have such a first-class treatment for concepts like properties (and indexers, and events, and so on) and rely on some naming convention instead:

```
```csharp
class Person
{
    public string getName() { ... }
    public void setName(string name) { ... }
}
```
```