```
```csharp
    set
    {
        age = value;
    }

// Overrides ToString( ) method from the Object class.
public override string ToString( )
{
    return firstName + " " + lastName;
}

// Virtual method can be overridden by classes that
// derive from the Person class.
public virtual int GetSleepAmt( )
{
    return 8;
}
}
```
```

The program statements that constitute the Student class are shown in Example 11-10. Note that a new using statement is added (using PersonNamespace). This is typed manually and matches the name of the namespace in the Person class. Adding references to other classes is discussed in the next section.

Also, notice that the identifier for the namespace in the Student class is StudentNamespace. This identifier is different from the namespace identifier in the Person class, because two separate projects are developed to demonstrate use of components.

The Student class includes two additional data fields, properties for those fields, and a GetSleepAmt( ) method that overrides the GetSleepAmt( ) method of the Person class. A second method is included to illustrate how a base method that has been overridden can be called. The Student class appears in Example 11-10.

# **Example 11-10**

```
```csharp
// Student.cs
using System;
using PersonNamespace; // Added to avoid using fully qualified names

namespace StudentNamespace
{
```
```