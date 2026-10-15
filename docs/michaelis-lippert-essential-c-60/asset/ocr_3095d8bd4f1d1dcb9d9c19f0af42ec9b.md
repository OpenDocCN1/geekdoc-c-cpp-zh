# OUTPUT 6.1

In Listing 6.11, `item.Name` is called; `item` is declared as a `PdaItem` there. However, the contact’s `FirstName` and `LastName` are still set. The rule is that whenever the runtime encounters a virtual method, it calls the most derived and overriding implementation of the virtual member. In this case, the code instantiates a `Contact` and calls `Contact.Name` because `Contact` contains the most derived implementation of `Name`.

In creating a class, programmers should be careful when choosing to allow overriding a method, since they cannot control the derived implementation. Virtual methods should not include critical code because such methods may never be called if the derived class overrides them. Furthermore, converting a method from a virtual method to a nonvirtual method could break derived classes that override the method. You should avoid such a code-breaking change, especially for assemblies intended for use by third parties.

Listing 6.12 includes a virtual `Run()` method. If the Controller programmer calls `Run()` with the expectation that the critical `Start()` and `Stop()` methods will be called, he will run into a problem.

```
```csharp
public class Controller
{
    public void Start()
    {
        // Critical code
    }
    public virtual void Run()
    {
        Start();
        Stop();
    }
    public void Stop()
    {
        // Critical code
    }
}
```
```

In overriding `Run()`, a developer could perhaps not call the critical `Start()` and `Stop()` methods. To force the `Start()`/`Stop()` expectation, the Controller programmer should define the class as shown in Listing 6.13.