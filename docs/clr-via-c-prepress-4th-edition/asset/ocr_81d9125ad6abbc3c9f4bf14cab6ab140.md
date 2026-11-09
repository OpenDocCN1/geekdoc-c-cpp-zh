Many programmers are familiar with the concept of multiple inheritance: the ability to define a class that is derived from two or more base classes. For example, imagine a class named *TransmitData*, whose function is to transmit data, and another class named *ReceiveData*, whose function is to receive data. Now imagine that you want to create a class named *SocketPort*, whose function is to transmit and receive data. In order to accomplish this, you would want to derive *SocketPort* from both *TransmitData* and *ReceiveData*.

Some programming languages allow multiple inheritance, making it possible for the *SocketPort* class to be derived from the two base classes, *TransmitData* and *ReceiveData*. However, the common language runtime (CLR)—and therefore all managed programming languages—does not support multiple inheritance. Rather than not offer any kind of multiple inheritance at all, the CLR does offer scaled-down multiple inheritance via *interfaces*. This chapter will discuss how to define and use interfaces as well as provide some guidelines to help you determine when to use an interface rather than a base class.

# ## Class and Interface Inheritance

In the Microsoft .NET Framework, there is a class called `System.Object` that defines four public instance methods: `ToString`, `Equals`, `GetHashCode`, and `GetType`. This class is the root or ultimate base class of all other classes—all classes will inherit `Object`'s four instance methods. This also means that code written to operate on an instance of the `Object` class can actually perform operations on an instance of any class.

Since someone at Microsoft has implemented `Object`'s methods, any class derived from `Object` is actually inheriting the following:

+   - **The method signatures** This allows code to think that it is operating on an instance of the `Object` class, when in fact, it could be operating on an instance of some other class.
+   - **The implementation of these methods** This allows the developer defining a class derived from `Object` not to be required to manually implement `Object`'s methods.

In the CLR, a class is always derived from one and only one class (that must ultimately be derived from `Object`). This base class provides a set of method signatures and implementations for these methods. And a cool thing about defining a new class is that it can become the base class for another class defined in the future by some other developer—all of the method signatures and their implementations will be inherited by the new derived class.

The CLR also allows developers to define an *interface*, which is really just a way to give a name to a set of method signatures. These methods do not come with any implementation at all. A class inherits an interface by specifying the interface's name, and the class must explicitly provide implementations of the interface's methods before the CLR will consider the type definition to be valid. Of course,