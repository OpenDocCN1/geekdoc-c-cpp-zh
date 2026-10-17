
```
Private Sub CustomList()

    Dim list As New SingleLinkedList(Of String)

    list.Add("Nikita")

    list.Add("Elena")

    list.Add("Benjamin")

    list.Add("William")

    list.Add("Abigail")

    list.Add("Johnathan")

    TextBoxOutput.Clear()

    TextBoxOutput.AppendText("Count: " & list.Count)

    TextBoxOutput.AppendText(Environment.NewLine)

    For index As Integer = 0 To list.Count - 1

        TextBoxOutput.AppendText("Item: " & list.Item(index))

        TextBoxOutput.AppendText(Environment.NewLine)

    Next

End Sub
```

Code snippet from Form1

When you run the code, you will see a display similar to Figure 8-5.

![](img/d99870e80390742f93963da7be0b2e61_345_0.png)

FIGURE 8-5

### Other Generic Class Features

Earlier in the chapter, you used the `Dictionary` generic, which specifies multiple type parameters. To declare a class with multiple type parameters, you use syntax like the following:

```
Public Class MyCoolType(Of T, V)

    Private mValue As T

    Private mData As V

    Public Sub New(ByVal value As T, ByVal data As V)

        mValue = value

        mData = data

    End Sub

End Class
```

In addition, it is possible to use regular types in combination with type parameters, as shown here:

```
Public Class MyCoolType(Of T, V)

    Private mValue As T

    Private mData As V

    Private mActual As Double

    Public Sub New(ByVal value As T, ByVal data As V, ByVal actual As Double)

        mValue = value

        mData = data

        mActual = actual

    End Sub

End Class
```

Other than the fact that variables or parameters of types `T` or `V` must be treated as type `System.Object`, you can write virtually any code you choose. The code in a generic class is really no different from the code you'd write in a normal class.

This includes all the object-oriented capabilities of classes, including inheritance, overloading, overriding, events, methods, properties, and so forth. However, there are some limitations on overloading. In particular, when overloading methods with a type parameter, the compiler does not know what that specific type might be at runtime. Thus, you can only overload methods in ways in which the type parameter (which could be any type) does not lead to ambiguity.

For instance, adding these two methods to `MyCoolType` before the .NET Framework 3.5 would have resulted in a compiler error:

```
Public Sub DoWork(ByVal data As Integer)

    ' do work here

End Sub

Public Sub DoWork(ByVal data As V)

    ' do work here

End Sub
```

Now this is possible due to the support for implicitly typed variables. During compilation in .NET, the compiler figures out what the data type of `V` should be. Next it replaces `V` with that type which allows your code to compile correctly. This was not the case prior to .NET 3.5. Before this version of the .NET Framework, this kind of code would have resulted in a compiler error. It wasn't legal because the compiler didn't know whether `V` would be an `Integer` at runtime. If `V` were to end up defined as an `Integer`, then you'd have two identical method signatures in the same class.

### Classes and Inheritance

Not only can you create basic generic class templates, you can also combine the concept with inheritance. This can be as basic as having a generic template inherit from an existing class:

```
Public Class MyControls(Of T)

    Inherits Control

End Class
```

In this case, the `MyControls` generic class inherits from the Windows Forms `Control` class, thus gaining all the behaviors and interface elements of a `Control`.

Alternately, a conventional class can inherit from a generic template. Suppose that you have a simple generic template:

```
Public Class GenericBase(Of T)

End Class
```

It is quite practical to inherit from this generic class as you create other classes:

```
Public Class Subclass

    Inherits GenericBase(Of Integer)

End Class
```

Notice how the `Inherits` statement not only references `GenericBase`, but also provides a specific type for the type parameter of the generic type. Anytime you use a generic type, you must provide values for the type parameters, and this is no exception. This means that your new `Subclass` actually inherits from a specific instance of `GenericBase`, where `T` is of type `Integer`.

Finally, you can also have generic classes inherit from other generic classes. For instance, you can create a generic class that inherits from the `GenericBase` class:

```
Public Class GenericSubclass(Of T)

    Inherits GenericBase(Of Integer)

End Class
```

As with the previous example, this new class inherits from an instance of `GenericBase`, where `T` is of type `Integer`.

Things can get far more interesting. It turns out that you can use type parameters to specify the types for other type parameters. For instance, you could alter `GenericSubclass` like this:

```
Public Class GenericSubclass(Of V)

    Inherits GenericBase(Of V)

End Class
```

Notice that you're specifying that the type parameter for `GenericBase` is `V` — which is the type provided by the caller when declaring a variable of type `GenericSubclass`. Therefore, if a caller uses a declaration that creates an object as a `GenericSubclass(Of String)`, then `V` is of type `String`. This means that the `GenericSubclass` is now inheriting from an instance of `GenericBase`, where its `T` parameter is also of type `String`. The point being that the type flows through from the subclass into the base class. If that is not complex enough, for those who just want a feel for how twisted this logic can become, consider the following class definition:

```
Public Class GenericSubclass(Of V)

    Inherits GenericBase(Of GenericSubclass(Of V))

End Class
```

In this case, the `GenericSubclass` is inheriting from `GenericBase`, where the `T` type in `GenericBase` is actually based on the declared instance of the `GenericSubclass` type. A caller can create such an instance with the simple declaration which follows:

```
Dim obj As GenericSubclass(Of Date)
```

In this case, the `GenericSubclass` type has a `V` of type `Date`. It also inherits from `GenericBase`, which has a `T` of type `GenericSubclass(Of Date)`.

Such complex relationships are typically not useful; in fact, they are often counterproductive, making code difficult to follow and debug. The point was that it is important to recognize how types flow through generic templates, especially when inheritance is involved.

### Structures

You can also define generic `Structure` types. The basic rules and concepts are the same as for defining generic classes, as shown here:

```
Public Structure MyCoolStructure(Of T)

    Public Value As T

End Structure
```

As with generic classes, the type parameter or parameters represent real types that are provided by the user of the `Structure` in actual code. Thus, anywhere you see a `T` in the structure, it will be replaced by a real type such as `String` or `Integer`.

Code can use the `Structure` in a manner similar to how a generic class is used:

```
Dim data As MyCoolStructure(Of Guid)
```

When the variable is declared, an instance of the `Structure` is created based on the type parameter provided. In this example, an instance of `MyCoolStructure` that holds `Guid` objects has been created.

### Interfaces

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
```
