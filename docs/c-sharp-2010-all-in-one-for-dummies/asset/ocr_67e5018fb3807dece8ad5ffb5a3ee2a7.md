class because the property name is all you know. For that reason, you must have both get and set. You can initialize such properties using the property syntax.

```
```csharp
public int AnInt { get; set; } // Compiler provides a private variable.

AnInt = 2; // Initialize compiler-written instance variable via property.
```
```

# ## Accessors with access levels

Accessor properties don't necessarily have to be declared public. You can declare them at any appropriate level, even private, if the accessor is used only inside its class. (The upcoming example marks the Name property internal.)

You can even adjust the access levels of the get and set portions of an accessor individually. Suppose that you don't want to expose the set accessor outside your class — it's for internal use only. You can write the property like this:

```
```csharp
internal string Name { get; private set; }
```
```

![](bbox=[0.02, 0.46, 0.12, 0.55])

The AccessorPropertyShortcuts example at csharptwo.info illustrates this usage.

# # Getting Your Objects Off to a Good Start — Constructors

Controlling class access is only half the problem: An object needs a good start in life if it is to grow. A class can supply an initialization method that the application calls to get things started, but the application could forget to call the method. The class starts out with garbage, and the situation gets no better after that. If you want to hold the class accountable, you have to ensure that it has a chance to start out correctly.

![](bbox=[0.02, 0.62, 0.12, 0.69])

C# solves that problem by calling the initialization method for you — for example:

```
```csharp
MyObject mo = new MyObject();
```
```

In other words, this statement not only grabs an object from a special memory area, but it also initializes that object's members.

Keep the terms class and object separate in your mind. Cat is a class. My cat Striper is an object of class Cat.

![](bbox=[0.02, 0.85, 0.12, 0.92])

Book II
Chapter 5
Holding a Class Responsible