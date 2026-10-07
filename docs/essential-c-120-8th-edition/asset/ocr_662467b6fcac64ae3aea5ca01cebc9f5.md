might provide a performance improvement if initialization of static members is expensive and not needed before accessing a static field. For this reason, you should consider either initializing static fields inline rather than using a static constructor or initializing them at declaration time.

> ### Guidelines
CONSIDER initializing static fields inline than explicitly using static constructors or declaration assigned values.

# Static Properties

You can also declare properties as static. For example, Listing 6.50 wraps the data for the next ID into a property.

LISTING 6.50: Declaring a Static Property

```
public class Employee
{
    // ...
    public static int NextId
    {
        get
            return _NextId;
        }
        private set
        {
            _NextId = value;
        }
    }
    public static int _NextId = 42;
    // ...
```

It is almost always better to use a static property than a public static field, because public static fields are callable from anywhere, whereas a static property offers at least some level of encapsulation.