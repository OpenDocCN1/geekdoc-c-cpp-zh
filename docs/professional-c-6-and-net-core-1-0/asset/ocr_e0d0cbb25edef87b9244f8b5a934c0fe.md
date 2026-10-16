This dilemma is solved with dependency properties. With dependency properties, an object memory is not allocated for every property and every instance. Instead, the dependency property system manages a dictionary of all properties and allocates memory only if a value is changed. Otherwise, the default value is shared between all instances.

Dependency properties also have built-in support for change notification. With normal properties, you need to implement the interface INotifyPropertyChanged for change notification. How this can be done is explained in Chapter 31, “Patterns with XAML Apps.” Such a change mechanism is built-in with dependency properties. For data binding, the property of the UI element that is bound to the source of a .NET property must be a dependency property. Now, let’s get into the details of dependency properties.

From the outside, a dependency property looks like a normal .NET property. However, with a normal .NET property you usually also define the data member that is accessed by the get and set accessors of the property:

```
private int _value;
public int Value
{
    get
    {
        return _value;
    }
    set
    {
        _value = value;
    }
}
```

That’s not the case with dependency properties. A dependency property usually has a get and set accessor of a property as well. This is common with normal properties. However, with the implementation of the get and set accessors, the methods GetValue and SetValue are invoked. GetValue and SetValue are members of the base class DependencyObject, which also stipulates a requirement for dependency objects—that they must be implemented in a class that derives from DependencyObject. With WPF, the base class is defined in the namespace System.Windows, with UWP in the namespace Windows.UI.Xaml.

With a dependency property, the data member is kept inside an internal collection that is managed by the base class and only allocates data if the value changes. With unchanged values the data can be shared between different instances or base classes. The GetValue and SetValue methods require a DependencyProperty argument. This argument is defined by a static member of the class that has the same name as the property appended to the term Property. With the property Value, the static member has the name ValueProperty. DependencyProperty.Register is a helper method that registers the property in the dependency property system. The following code snippet