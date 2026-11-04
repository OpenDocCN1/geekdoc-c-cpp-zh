# Interfaces

When defining a class, you have to provide the implementation for all its methods and properties. However, there are times when you do not want to provide the actual implementation of how a class might work. Rather, you want to describe the functionalities of the class. This set of descriptions is like a contract, dictating what the class will do, the types of parameters needed, and the type of return results. In object-oriented programming, this contract is known as an interface.

An interface defines a class and its members without providing any implementation. When using interfaces in programming, generally three parties are involved:

+   - Interface definition — The interface defines the composition of a class, such as methods, properties, and so on. However, the interface does not provide any implementation for any of these members.
+   - Implementing class — The class that implements a particular interface provides the implementation for all the members defined in that interface.
+   - Clients — Objects that instantiate from the implementing classes are known as the client. The client invokes the methods defined in the interface, whose implementation is provided by the implementing class.

# Differences between an Interface and an Abstract Base Class

Conceptually, an abstract class is similar to an interface; however, they do have some subtle differences:

+   - An abstract class can contain a mixture of concrete methods (implemented) and abstract methods (an abstract class needs at least one abstract method); an interface does not contain any method implementations.
+   - An abstract class can contain constructors and destructors; an interface does not.
+   - A class can implement multiple interfaces, but it can inherit from only one abstract class.