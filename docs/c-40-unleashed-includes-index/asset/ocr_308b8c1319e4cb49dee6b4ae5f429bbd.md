This should give you a good initial idea about where type parameters can be used to make a type as generic as possible with regard to the objects it operates on, without losing any of the rich type information at compile time.

# Using Generic Types

In our discussion about generic types, you learned how a generic type is used repeatedly. Let's concentrate on the phonebook example a bit more:

```
var numbers = new Dictionary<string, int> {
    { "Bart", 911 },
    { "John", 119 }
};
```

In the preceding code, we're making a constructed generic type by substituting the TKey type parameter for string and the TValue type parameter for int. As you expect from a great development environment, Visual Studio provides IntelliSense when supplying types for generic type parameters, as shown in Figure 15.9.

![](bbox=[0.15, 0.71, 0.55, 0.8])

FIGURE 15.9 Creating a constructed generic type with help from Visual Studio.

Behind the scenes, the type parameterization specified while creating a constructed generic type survives in the intermediate language (IL) code. Looking at it from a different angle, it's the CLR that's responsible for dealing with the creation of the ultimate type, rather than the front-end language compiler. As mentioned before, this is quite different from the way C++ templates work.

The role of the CLR—and in particular the Just-in-Time (JIT) compiler—is to come up with concrete memory layouts for all the constructed generic types it comes across at runtime. This effectively constitutes substitution of the holes created by type parameters, as you saw earlier during our discussion about the declaration of generic types. Ultimately, the result is just as if someone created a specialized nongeneric class with the parameter types baked into the appropriate positions, as shown in Figure 15.10.

# NO ERASURE

Another platform that provides a way to parameterize types is Java. Despite sharing the name generics, the way it's implemented differs from the CLR's approach. Generic types in Java are more of a compile-time illusion, allowing the runtime to remain the same and even to target existing nongeneric collection types. All the compiler does is make sure the constructed generic types are used correctly, but in the end the type parameters are erased away.