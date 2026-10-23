![](bbox=[0.15, 0.12, 0.8, 0.21])

# FIGURE 27.5 Delegate as proxy (intermediary)

# 27.10 MODELLING EVENT-DRIVEN APPLICATIONS WITH DELEGATES

In this section we introduce Delegates in the .NET Framework. From a design perspective delegates are a realisation of the Proxy pattern; in this case a delegate plays the role of the proxy and it has a reference to a target method having the same signature as that of the proxy interface. Clients communicate with the delegate without knowing (or having to know) the details of the target method ‘behind’ the delegate. It is possible to replace one target method by another one at run-time. Client code communicates directly with the delegate and not with any target method. A UML diagram showing the structural relationships between these entities is given in Figure 27.5.

A delegate type is a specification of a function signature, that is it has a return type, a name and zero or more input arguments. In this sense the delegate type represents a protocol or contract. We note that a delegate type has no body. In a sense it is similar to an abstract method in that it must be instantiated so that clients can use it. In native C++, a delegate is similar to the universal function wrapper std::function. To this end, we introduce the concept of a delegate instance, which is a specific method with a body whose signature conforms to that of the delegate type.

We take our first example in C#. Consider the delegate type that specifies scalar-valued functions of a scalar variable:

```
delegate double ComputableFunction(double x);  // The protocol
```

This type can now be assigned to specific delegate instances (called target methods) if these instances have the same signature as that of the type. For convenience, we define some instances as static methods:

```
class Delegates

    // Some delegate instances
    public static double Square(double x)
    {
        return x * x;
    }

    public static double Cube(double x)
    {
        return x * x * x;
    }
```