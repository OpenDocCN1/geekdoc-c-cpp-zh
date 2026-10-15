For instance, you may have a series of different objects in an application: product, customer, invoice, and so forth. Each of these would have default interfaces appropriate to each individual object — and each of them is a different class — so there’s no natural inheritance relationship implied between these classes. At the same time, you may need to be able to generate a printed document for each type of object, so you would like to make them all act as a printable object.

> This chapter discusses the is-a and act-as relationships in more detail later.

To accomplish this, you can define a generic interface that enables generating such a printed document. You can call it IPrintableObject.

> By convention, this type of interface is typically prefixed with a capital “I” to indicate that it is a formal interface.

Each of your application objects can choose to implement the IPrintableObject interface. Every object that implements this interface must include code to provide actual implementation of the interface, which is unlike inheritance, whereby the code from a base class is automatically reused.

By implementing this common interface, you can write a routine that accepts any object that implements the IPrintableObject interface and then print it — while remaining totally oblivious to the “real” data type of the object or methods its native interface might expose. Before you learn how to use an interface in this manner, let’s walk through the process of actually defining an interface.

# Defining the Interface

You define a formal interface using the Interface keyword. This can be done in any code module in your project, but a good place to put this type of definition is in a standard module. An interface defines a set of methods (Sub, Function, or Property) and events that must be exposed by any class that chooses to implement the interface.

Add a module to the project using Project ▸ Add Module and name it Interfaces.vb. Then, add the following code to the module, outside the Module code block itself:

```
Public Interface IPrintableObject

End Interface

Module Interfaces

End Module
```

Code snippet from Interfaces

A code module can contain a number of interface definitions, and these definitions must exist outside of any other code block. Thus, they do not go within a Class or Module block; they are at a peer level to those constructs.

Interfaces must be declared using either Public or Friend scope. Declaring a Private or Protected interface results in a syntax error. Within the Interface block of code, you can define the methods, properties, and events that make up your particular interface. Because the scope of the interface is defined by the Interface declaration itself, you can’t specify scopes for individual methods and events; they are all scoped like the interface itself.