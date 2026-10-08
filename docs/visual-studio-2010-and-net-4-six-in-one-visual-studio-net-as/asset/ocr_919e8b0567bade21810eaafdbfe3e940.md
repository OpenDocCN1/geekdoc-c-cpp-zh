+   - An entire class is an exported part, and an import referencing a related contract must be satisfied.
In this case, the exported class is instantiated, and this instance is assigned to the import.

+   - A property (or field) of a class is exported. To satisfy a related import, this class is instantiated, and then the appropriate property's value (or field value) is assigned to the import.

+   - A method of class is exported. In this case, the hosting class is created, and a delegate to the exported method is assigned to the import.

Of course, if exported parts are members of static classes, you do not have the same control, as in the

case when instantiation occurs behind the scenes, you are the one who explicitly creates those instances. By default, MEF uses the default constructor of the class (the constructor with no parameters). If there is no default constructor, MEF looks for a constructor of exactly one decorated with the `ImportingConstructor` attribute. If there is such a constructor, its parameters are taken into account as imports. MEF satisfies those imports, and you use those parameters with which to call the constructor. If there is no such constructor, MEF raises an exception, because it cannot create an instance.

Earlier in 10-25, the import of an `IContextInfo` part was implemented in this way:

```
[Export(typeof(IGreeting))]
class UserGreeting{
    [Import]
    IContextInfo ContextInfo { get; set; }

    public string SayHello(
        string username;
        var props = ContextInfo.Get();
        props.TryGetValue("Username", out username);
        return "Hello " + username ?? "<None>";
    }
}
```

With `ImportingConstructor`, it could also be done as follows:

```
[Export(typeof(IGreeting))]
class UserGreeting{
    IContextInfo ContextInfo { get; set; }

    [ImportingConstructor]
    public UserGreeting(IContextInfo contextInfo)
{
        ContextInfo = contextInfo;
    }

    public string SayHello()
{
        // ... Omitted for the sake of brevity
    }
}
```