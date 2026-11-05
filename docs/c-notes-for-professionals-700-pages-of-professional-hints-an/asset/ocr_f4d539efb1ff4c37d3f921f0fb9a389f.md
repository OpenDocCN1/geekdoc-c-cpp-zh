```
Animal.Yawn();
```

This will output:

> Animal initialized
> Yawn!

See also Exceptions in static constructors and Generic Static Constructors .

Singleton example:

```
```csharp
public class SessionManager
{
    public static SessionManager Instance;
    static SessionManager()
    {
        Instance = new SessionManager();
    }
}
```
```

# Section 39.2: Singleton constructor pattern

```
```csharp
public class SingletonClass
{
    public static SingletonClass Instance { get; } = new SingletonClass();
    private SingletonClass()
    {
        // Put custom constructor code here
    }
}
```
```

Because the constructor is private, no new instances of SingletonClass can be made by consuming code. The only way to access the single instance of SingletonClass is by using the static property SingletonClass.Instance.

The Instance property is assigned by a static constructor that the C# compiler generates. The .NET runtime guarantees that the static constructor is run at most once and is run before Instance is first read. Therefore, all synchronization and initialization concerns are carried out by the runtime.

Note, that if the static constructor fails the Singleton class becomes permanently unusable for the life of the AppDomain.

Also, the static constructor is not guaranteed to run at the time of the first access of Instance. Rather, it will run at some point before that. This makes the time at which initialization happens non-deterministic. In practical cases the JIT often calls the static constructor during compilation (not execution) of a method referencing Instance. This is a performance optimization.

See the Singleton Implementations page for other ways to implement the singleton pattern.

# Section 39.3: Default Constructor

When a type is defined without a constructor: