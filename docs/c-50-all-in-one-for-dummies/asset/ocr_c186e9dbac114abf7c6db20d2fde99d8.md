# Figure 9-2:
Sending your delegate to the bungee-jump on your behalf.

![](bbox=[0.22, 0.14, 0.78, 0.6])

A delegate is a data type, similar to a class. As with a class, you create an instance of the delegate type in order to use the delegate. Figure 9-2 shows the sequence of events in the delegate’s life cycle as you complete these steps:

+   1. **Define the delegate type (in much the same way as you would define a class).**

Sometimes, C# has already defined a delegate you can use. Much of the time, though, you need to define your own, custom delegates.

Under the surface, a delegate is a class, derived from the class System.MulticastDelegate, which knows how to store one or more “pointers” to methods and invoke them for you. Relax: The compiler writes the class part of it for you.

+   2. **Create an instance of the delegate type — such as instantiating a class.**

During creation, you hand the new delegate instance the name of a method that you want it to use as a callback or an action method.

![](bbox=[0.11, 0.77, 0.2, 0.83])

![](bbox=[0.11, 0.83, 0.2, 0.89])

```
void DoLongComplexProcess(<aDelegate parameter>)
{
    // ... Some code.
    aDelegate(3, 4, 5)
}
```