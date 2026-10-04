# Class and Interface Inheritance

In the Microsoft .NET Framework, there is a class called System.Object that defines public instance methods: ToString, Equals, GetHashCode, and GetType. This class is the root or ultimate base class of all classes—all classes inherit Object's four instance methods. This also means code written to operate on an instance of the Object class can actually perform operations on an instance of any class.

Because some at Microsoft has implemented Object's methods, any class derived from Object is actually inheriting the following:

+   * The method signatures This code allows to think that it is operating on an instance of the Object class, when in fact, it could be operating on an instance of some class.
* The implementation of these methods This allows the developer defining a derived class from Object not to be required to manually implement Object's methods.

In the CLR, a class is always derived from one and only class (that ultimately be derived from Object). This base class provides a set of method signatures and implementations for these methods. A cool thing about defining a new class is that it can become the base class for other class defined in the future—all of the method signatures and their implementations will be inherited by the new derived class.

The CLR also allows developers to define an interface, which is really just to give a name to a set of method signatures. These methods do not come with any implementation at all. A class inherits an interface by specifying the interface's name, and the class must explicitly implement the interface's methods before the CLR will consider the referred type to be valid. Of course, implementing interface methods can be tedious, which is why I referred to inheritance as a scaled-down mechanism to achieve multiple inheritance. The C# compiler and the CLR actually allow a class to inherit several interfaces, and of course, the class must provide implementations for all of the inherited interface methods.

One of the great features of class inheritance is that it allows instances of a derived type to be substituted in all contexts that expect instances of a base type. Similarly, interface inheritance allows instances of a type that implements the interface to be substituted in all contexts that expect instances of the named interface type. We will now look at how to define interfaces to make our discussion concrete.

# Defining an Interface

As mentioned in the previous section, an interface is a named set of method signatures. Note that interfaces can also define events, parameterless properties, and parameterized properties (indexers in C#) because all of these are just syntax shortcuts that map to methods away, shown in previous chapters. However, an interface cannot define any constructor methods. In addition, an interface is not allowed to define any instance fields.