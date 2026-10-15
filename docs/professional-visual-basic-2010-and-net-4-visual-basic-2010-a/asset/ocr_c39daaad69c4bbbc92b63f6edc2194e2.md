# Interfaces

Finally, you can define generic interface types. Generic interfaces are a bit different from generic classes or structures because they are implemented by other types when they are used. You can create a generic interface using the same syntax used for classes and structures:

```
Public Interface ICoolInterface(Of T)
    Sub DoWork(ByVal data As T)
    Function GetAnswer() As T
End Interface
```

Then the interface can be used within another type. For instance, you might implement the interface in a class:

```
Public Class ARegularClass
    Implements ICoolInterface(Of String)
    Public Sub DoWork(ByVal data As String) _
        Implements ICoolInterface(Of String).DoWork
    End Sub
    Public Function GetAnswer() As String _
        Implements ICoolInterface(Of String).GetAnswer
    End Function
End Class
```

Notice that you provide a real type for the type parameter in the Implements statement and Implements clauses on each method. In each case, you are specifying a specific instance of the ICoolInterface interface — one that deals with the String data type.

As with classes and structures, an interface can be declared with multiple type parameters. Those type parameter values can be used in place of any normal type (such as String or Date) in any Sub, Function, Property, or Event declaration.

# Generic Methods

You have already seen examples of methods declared using type parameters such as T or V. While these are examples of generic methods, they have been contained within a broader generic type such as a class, a structure, or an interface.

It is also possible to create generic methods within otherwise normal classes, structures, interfaces, or modules. In this case, the type parameter is not specified on the class, structure, or interface, but rather directly on the method itself.

For instance, you can declare a generic method to compare equality like this:

```
Public Module Comparisons
    Public Function AreEqual(Of T)(ByVal a As T, ByVal b As T) As Boolean
        Return a.Equals(b)
    End Function
End Module
```

In this case, the AreEqual method is contained within a module, though it could just as easily be contained in a class or a structure. Notice that the method accepts two sets of parameters. The first set of parameters is the type parameter — in this example, just T. The second set of parameters consists of the normal parameters that a method would accept. In this example, the normal parameters have their types defined by the type parameter, T.

As with generic classes, it is important to remember that the type parameter is treated as a System.Object type as you write the code in your generic method. This severely restricts what you can do with parameters or variables declared using the type parameters. Specifically, you can perform assignment and call the various methods common to all System.Object variables.

In a moment you will look at constraints, which enable you to restrict the types that can be assigned to the type parameters and expand the operations that can be performed on parameters and variables of those types.