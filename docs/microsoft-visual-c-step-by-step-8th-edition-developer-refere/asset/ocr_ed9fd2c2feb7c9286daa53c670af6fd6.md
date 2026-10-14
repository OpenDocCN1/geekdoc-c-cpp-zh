# Note

An interface, InterfaceA, can inherit from another interface, InterfaceB. Technically, this is known as *interface extension* rather than inheritance. In this case, any class or struct that implements InterfaceA must provide implementations of all the methods in InterfaceB and InterfaceA.

# Referencing a class through its interface

In the same way that you can reference an object by using a variable defined as a class that is higher up the hierarchy, you can reference an object by using a variable defined as an interface that the object’s class implements. Taking the preceding example, you can reference a *Horse* object by using an *ILandBound* variable, as follows:

Click here to view code image

```
Horse myHorse = new Horse(...);
ILandBound iMyHorse = myHorse; // legal
```

This works because all horses are land-bound mammals, although the converse is not true—you cannot assign an *ILandBound* object to a *Horse* variable without casting it first to verify that it does actually reference a *Horse* object and not some other class that also happens to implement the *ILandBound* interface.

The technique of referencing an object through an interface is useful because you can use it to define methods that can take different types as parameters, as long as the types implement a specified interface. For example, the *FindLandSpeed* method shown here can take any argument that implements the *ILandBound* interface:

Click here to view code image

```
int FindLandSpeed(ILandBound landBoundMammal)
{
    ...
}
```

You can verify that an object is an instance of a class that implements a specific interface by using the *is* operator, which is demonstrated in Chapter 8, “Understanding values and references.” You use the *is* operator to determine whether an object has a specified type, and it works with interfaces as well as with classes and structs. For example, the following block of code checks that the variable *myHorse* actually implements the *ILandBound* interface before attempting to assign it to an *ILandBound* variable:

Click here to view code image

```
if (myHorse is ILandBound)
```