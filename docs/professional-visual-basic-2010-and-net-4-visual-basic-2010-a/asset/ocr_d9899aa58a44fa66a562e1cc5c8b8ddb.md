value, including a reference to any type of object. Thus, code such as the following could be run against any object that implements a DoSomething method that accepts no parameters:

```
Option Strict Off

Module LateBind
    Public Sub DoWork(ByVal obj As Object)
        obj.DoSomething()
    End Sub
End Module
```

If the object passed into this routine does not have a DoSomething method that accepts no parameters, then an exception will be thrown. Thus, it is recommended that any code that uses late binding always provide exception handling:

```
Option Strict Off

Module LateBind
    Public Sub DoWork(ByVal obj As Object)
        Try
            obj.DoSomething()
        Catch ex As MissingMemberException
            ' do something appropriate given failure
            ' to call this method
        End Try
    End Sub
End Module
```

Here, the call to the DoSomething method has been put in a Try block. If it works, then the code in the Catch block is ignored; but in the case of a failure, the code in the Catch block is run. You need to write code in the Catch block to handle the case in which the object does not support the DoSomething method call. This Catch block only catches the MissingMemberException, which indicates that the method does not exist on the object.

While late binding is flexible, it can be error prone and is slower than early-bound code. To make a late-bound method call, the .NET runtime must dynamically determine whether the target object actually has a method that matches the one you are calling. It must then invoke that method on your behalf. This takes more time and effort than an early-bound call, whereby the compiler knows ahead of time that the method exists and can compile the code to make the call directly. With a late-bound call, the compiler has to generate code to make the call dynamically at runtime.

# DATA TYPE CONVERSIONS

So far, this chapter has focused primarily on individual variables; but when developing software, it is often necessary to take a numeric value and convert it to a string to display in a text box. Similarly, it is often necessary to accept input from a text box and convert this input to a numeric value. These conversions, unlike some, can be done in one of two fashions: implicitly or explicitly.

Implicit conversions are those that rely on the system to adjust the data at runtime to the new type without any guidance. Often, Visual Basic’s default settings enable developers to write code containing many implicit conversions that the developer may not even notice.

Explicit conversions, conversely, are those for which the developer recognizes the need to change a variable’s type and assign it to a different variable. Unlike implicit conversions, explicit conversions are easily recognizable within the code. Some languages such as C# require that essentially all conversions that might be type unsafe be done through an explicit conversion; otherwise, an error is thrown.

It is therefore important to understand what a type-safe implicit conversion is. In short, it’s a conversion that cannot fail because of the nature of the data involved. For example, if you assign the value of a smaller type, Short, into a larger type, Long, then there is no way this conversion can fail. As both values are