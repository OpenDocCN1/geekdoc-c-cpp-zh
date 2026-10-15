Another reason why a custom delegate type might be used concerns parts of the CLR API that were defined prior to C# 2.0. Given that these parts represent a fairly significant percentage of the more common types within the framework, it is not uncommon to encounter specific delegate types rather than the generic form on events coming from the CLR API. Regardless, in the majority of circumstances when using events in C# 2.0 and later, it is not necessary to declare a custom delegate data type.

# Guidelines

DO use System.EventHandler<T> instead of manually creating new delegate types for event handlers, unless the parameter names of a custom type offer significant clarification.

# ADVANCED TOPIC

# Event Internals

Events restrict external classes from doing anything other than adding subscribing methods to the publisher via the += operator and then unsubscribing using the -= operator. In addition, they restrict classes, other than the containing class, from invoking the event. To do so, the C# compiler takes the public delegate variable with its event keyword modifier and declares the delegate as private. In addition, it adds a couple of methods and two special event blocks. Essentially, the event keyword is a C# shortcut for generating the appropriate encapsulation logic. Consider the example in the event declaration shown in Listing 13.17.

# LISTING 13.17: Declaring the OnTemperatureChange Event

```
public class Thermostat
{
    public event EventHandler<TemperatureArgs> OnTemperatureChange;
    ...
}
```

When the C# compiler encounters the event keyword, it generates CIL code equivalent to the C# code shown in Listing 13.18.