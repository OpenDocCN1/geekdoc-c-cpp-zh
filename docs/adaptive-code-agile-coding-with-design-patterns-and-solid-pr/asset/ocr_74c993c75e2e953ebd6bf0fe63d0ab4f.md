One of the limitations of Re-mix is that you do not—and cannot—know the exact type of the instance returned by ObjectFactory.Create. All you know is that it is an instance of a subclass TargetImplementation. This is sort of bad news for clients, because the only interface you can guarantee that TargetImplementation fulfills at compile time is ITargetInterface. Clients of the mixin, therefore, must type-sniff by using is and as to cast the mixin to the desired interface. Listing 4-33 highlights this problem.

# LISTING 4-33 Type-sniffing is bad practice but necessary for using mixins.

```
public class MixinClient
{
    public MixinClient(ITargetInterface target)
    {
        this.target = target;
    }

    public void Run()
    {
        target.DoSomething();

        var targetAsMixinA = target as IMixinInterfaceA;
        if(targetAsMixinA != null)
        {
            targetAsMixinA.MethodA();
        }

        var targetAsMixinB = target as IMixinInterfaceB;
        if(targetAsMixinB != null)
        {
            targetAsMixinB.MethodB(30);
        }

        var targetAsMixinC = target as IMixinInterfaceC;
        if(targetAsMixinC != null)
        {
            targetAsMixinC.MethodC("Hello!");
        }
    }

    private readonly ITargetInterface target;
}
```

Applying mixins to a solution works best when type-sniffing is already present or necessary. This is true with some libraries and frameworks. For example, Prism (the Windows Presentation Foundation/Model-View-Viewmodel library) makes use of type-sniffing, and the functionality required of client classes can be segregated into different implementations and recombined via mixins.