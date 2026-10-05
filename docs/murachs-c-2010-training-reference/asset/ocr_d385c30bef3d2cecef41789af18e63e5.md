# The syntax for creating an interface

```
public interface InterfaceName {
    type MethodName(parameters); // Declares a method
    type PropertyName {
        [get]; // Declares a get accessor
        [set]; // Declares a set accessor
    }
}
```

# An interface defines one IDisplayable

```
public interface IDisplayable {
    string GetDisplayText(string sep);
}
```

# An interface defines two methods and a property

```
public interface IPersistable {
    object Read(string id);
    bool Save(object o);
    bool HasChanges {
        get;
        set;
    }
}
```

# The syntax for creating an interface that inherits other interfaces

```
public interface InterfaceName : InterfaceName1, InterfaceName2 {
    interface members...
}
```

# An interface that inherits two interfaces

```
public interface IDataAccessObject : IDisplayable, IPersistable {
    // additional members here
}
```

# Description

+   - The declaration for an interface is similar to the declaration for a class. The only difference is that you use the interface keyword instead of the class keyword.

+   - Methods and properties that are declared within an interface can't include implementation. As a result, method declarations and get and set accessors always end with a semicolon.

+   - You shouldn't include any access modifiers on interface members. All members are considered to be public and abstract, and static members aren't allowed.

![](bbox=[0.061, 0.954, 0.416, 0.969])