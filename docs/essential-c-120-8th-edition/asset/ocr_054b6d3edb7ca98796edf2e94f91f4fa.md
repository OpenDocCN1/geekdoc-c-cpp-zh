# Attributes 895

```
LISTING 18.7: Dynamically Invoking a Member
using System.ComponentModel;
npublic class Person : INotifyPropertyChanged
{
    public event PropertyChangedEventHandler? PropertyChanged;
    public Person(string name)
    {
        Name = name;
    }
    private string _Name = string.Empty;
    public string Name
    {
        get { return _Name; }
        set
        {
            if (_Name != value)
            {
                _Name = value;
                PropertyChanged?.Invoke(
                    this,
                    new PropertyChangedArgs(nameof(Name)));
            }
        }
    }
    // ...
}
```

No matter whether only the unqualified "Name" is provided (because it's in scope) or the fully (or partially) qualified name such as Person.Name is used, the result is only the final identifier (the last element in a dotted name).

You can still use the CallerMemberName parameter attribute⁴ to obtain a property’s name; see http://itl.lc/CallerMemberName for an example.

# Attributes

Before delving into the details of how to program attributes, we should consider a use case that demonstrates their utility. In the CommandLineHandler example in

+   4. Starting in C# 5.0.