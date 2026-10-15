# LISTING 6.13: Forcing the Desirable Run() Semantics

```
public class Controller
{
    public void Start()
    {
        // Critical code
    }

    private void Run()
    {
        Start();
        InternalRun();
        Stop();
    }

    protected virtual void InternalRun()
    {
        // Default implementation
    }

    public void Stop()
    {
        // Critical code
    }
}
```

With this new listing, on the one hand, the Controller programmer prevents users from mistakenly calling InternalRun(), because it is protected. On the other hand, declaring Run() as public ensures that Start() and Stop() are invoked appropriately. It is still possible for users to modify the default implementation of how the Controller executes by overriding the protected InternalRun() member from within the derived class.

Virtual methods provide default implementations only—that is, implementations that derived classes could override entirely. However, because of the complexities of inheritance design, it is important to consider (and preferably to implement) a specific scenario that requires the virtual method definition rather than declaring members as virtual by default.

Finally, only instance members can be virtual. The CLR uses the concrete type, specified at instantiation time, to determine where to dispatch a virtual method call, so static virtual methods are meaningless and the compiler prohibits them.