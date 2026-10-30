# Interfaces and design patterns

After completing this chapter, you will be able to

+   - Define interfaces and identify the ways in which they differ from classes.
+   - Apply design patterns, such as the Adapter and Strategy patterns, by using interfaces.
+   - Understand an interface's versatility through duck-typing, mixins, and fluent interfaces.
+   - Identify the limitations of interfaces and implement workarounds.
+   - Spot common anti-patterns and abuses of interfaces.

The interface is a powerful construct in Microsoft .NET Framework development. Although the interface keyword is very simple, what it represents is a very powerful paradigm. When used correctly, interfaces provide your code with the extension points that make it adaptive. However, some uses of interfaces are not so good, yet they remain in common use.

This chapter provides a reminder of the differences between classes and interfaces and describes how best to use the two together, both to protect client code from implementation changes and to facilitate polymorphism.

It also covers the versatility of interfaces and how they are a ubiquitous tool in modern software solutions. This chapter demonstrates some powerful design patterns that, when applied correctly (in conjunction with other patterns in this book) yield code that is very flexible and able to adapt to the changing requirements that Agile projects embrace.

However, interfaces alone are no panacea. A judicious sprinkling of interfaces can certainly help a project, but the interfaces must be applied in the correct manner. This chapter also explores some of the common abuses of interfaces.

# What is an interface?

An interface defines the behavior that a class has, but not how this behavior is implemented. An interface stands as a separate construct from a class, but it requires a class to provide the working code to fulfill the interface.