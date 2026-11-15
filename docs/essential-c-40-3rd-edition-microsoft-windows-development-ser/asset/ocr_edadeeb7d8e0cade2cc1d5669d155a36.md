# LISTING 17.13: Providing an Attribute Constructor

```
public class CommandLineSwitchAliasAttribute : Attribute
{
    public CommandLineSwitchAliasAttribute(string alias)
    {
        Alias = alias;
    }

    public string Alias
    {
        get { return _Alias; }
        set { _Alias = value; }
    }
    private string _Alias;
}
```

```
class CommandLineInfo
{
    [CommandLineSwitchAlias("?")]
    public bool Help
    {
        get { return _Help; }
        set { _Help = value; }
    }
    private bool _Help;
    // ...
}
```

The only restriction on the constructor is that when applying an attribute to a construct, only literal values and types (such as typeof(int)) are allowed as arguments. This is to enable their serialization into the resultant CIL. Therefore, it is not possible to call a static method when applying an attribute. In addition, providing a constructor that takes arguments of type System.DateTime would be of little value, since there is no System.DateTime literal. Given the constructor call, the objects returned from PropertyInfo.GetCustomAttributes() will be initialized with the specified constructor arguments, as demonstrated in Listing 17.14.

# LISTING 17.14: Retrieving a Specific Attribute and Checking Its Initialization

```
PropertyInfo property =
    typeof(CommandLineInfo).GetProperty("Help");
```