```
}
)
```

# Interface restrictions

There’s another reason for keeping the default implementation of a method simple. Essentially, an interface is not a class, and you shouldn’t treat it as such. Remember that an interface is a definition of the shape of a type, rather than an implementation of the type. The following restrictions are natural consequences of this:

+   - You’re not allowed to define any fields in an interface, not even static fields. A field is an implementation detail of a class or structure.

+   - You’re not allowed to define any constructors in an interface. A constructor is also considered to be an implementation detail of a class or structure.

+   - You’re not allowed to define a destructor in an interface. A destructor contains the statements used to destroy an object instance. (Destructors are described in Chapter 14, “Using garbage collection and resource management.")

+   - You cannot specify an access modifier for any method. All methods in an interface are implicitly public.

+   - You cannot nest any types (such as enumerations, structures, classes, or interfaces) inside an interface.

+   - An interface is not allowed to inherit from a structure, record, or class, although an interface can inherit from another interface. Structures, records, and classes can contain implementation details; if an interface were to inherit from any of these types, it would be inheriting some implementation details.

# Defining and using interfaces

In the following exercises, you’ll define and implement interfaces that constitute part of a simple graphical drawing package. You will define two interfaces, called IDraw and IColor, and then you’ll define classes that implement them. Each class will define a shape that can be drawn on a canvas on a form. (A canvas is a control that you can use to draw lines, text, and shapes on the screen.)

The IDraw interface defines the following methods: