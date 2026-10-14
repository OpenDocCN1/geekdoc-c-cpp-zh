```
```csharp
void MethodC(string parameter);
}
// ...
public class MixinImplementationC : IMixinInterfaceC
{
    public void MethodC(string parameter)
    {
        Console.WriteLine("IMixinInterfaceC.MethodC(\"{0}\")", parameter);
    }
}
```
```

Note that there is no single class that implements all of these interfaces. Instead, the next step is to configure Re-mix so that, when it is asked for an instance of TargetImplementation, it will return a mixin containing all of the interfaces and classes combined. [Listing 3-30](#listing-3-30) shows such a configuration.

# **LISTING 3-30** Instructing Re-mix how to construct TargetImplementation instances.

[Click here to view code image](#code-image)

```
```csharp
var config = MixinConfiguration.BuildFromActive()
    .ForClass<TargetImplementation>()
    .AddMixin<MixinImplementationA>()
    .AddMixin<MixinImplementationB>()
    .AddMixin<MixinImplementationC>()
    .BuildConfiguration();

MixinConfiguration.SetActiveConfiguration(config);
```
```

Unfortunately, you cannot simply call new on the TargetImplementation and expect a mixin. Instead, you have to ask Re-mix to create a TargetImplementation instance so that it can build a new type to your specification and instantiate it. [Listing 3-31](#listing-3-31) shows how it can do that—and luckily, it is trivial.

# **LISTING 3-31** Re-mix is in charge of creating mixins.

[Click here to view code image](#code-image)

```
```csharp
ITargetInterface target = ObjectFactory.Create<TargetImplementation>(ParamList.Empty)
```
```

One of the limitations of Re-mix is that you do not—and cannot—know the exact type of the instance returned by ObjectFactory.Create. All you know is that it is an instance of a subclass TargetImplementation. This is sort of bad news for clients, because the only interface you can guarantee that TargetImplementation fulfills at compile time is ITargetInterface. Clients of the mixin, therefore, must type-sniff by using is and as to cast the mixin to the desired interface. [Listing 3-32](#listing-3-32) highlights this problem.