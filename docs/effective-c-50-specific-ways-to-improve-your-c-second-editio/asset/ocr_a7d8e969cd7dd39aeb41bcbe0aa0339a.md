scope of the classes, you have limited the code you need to change to update and extend the entire system.

You could also create a public abstract base class for PhoneValidator, which could contain common implementation algorithms. The consumers could access the public functionality through the accessible base class. In this example, I prefer the implementation using public interfaces because there is little, if any, shared functionality. Other uses would be better served with public abstract base classes. Either way you implement it, fewer classes are publicly accessible.

In addition, fewer public types will create a smaller public surface area that will facilitate unit testing coverage. If there are fewer public types, there are fewer publicly accessible methods for which you need to create tests. Also, if more of the public APIs are exposed through interfaces, you have automatically created a system whereby you can replace those types using some kind of stubs for unit test purposes.

Those classes and interfaces that you expose publicly to the outside world are your contract: You must live up to them. The more cluttered that interface is, the more constrained your future direction is. The fewer public types you expose, the more options you have to extend and modify any implementation in the future.

# Item 22: Prefer Defining and Implementing Interfaces to Inheritance

Abstract base classes provide a common ancestor for a class hierarchy. An interface describes one atomic piece of functionality that can be implemented by a type. Each has its place, but it is a different place. Interfaces are a way to design by contract: A type that implements an interface must supply an implementation for expected methods. Abstract base classes provide a common abstraction for a set of related types. It’s a cliché, but it’s one that works: Inheritance means “is a,” and interfaces means “behaves like.” These clichés have lived so long because they provide a means to describe the differences in both constructs: Base classes describe what an object is; interfaces describe one way in which it behaves.

Interfaces describe a set of functionality, or a contract. You can create placeholders for anything in an interface: methods, properties, indexers, and events. Any type that implements the interface must supply concrete