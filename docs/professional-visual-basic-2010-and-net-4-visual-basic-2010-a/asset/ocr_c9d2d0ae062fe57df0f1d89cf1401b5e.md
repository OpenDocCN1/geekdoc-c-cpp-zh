Finally, you can use the Friend keyword:

```
Friend Sub DoSomething()

End Sub
```

In this case, the DoSomething method can be called by code within the class, or from other classes or modules within the current Visual Basic project. Code from outside the project will not have access to the method.

The Friend scope is very similar to the Public scope in that it makes methods available for use by code outside the object itself. Unlike Public, however, the Friend keyword restricts access to code within the current Visual Basic project, preventing code in other .NET assemblies from calling the method. One of the more common uses of Protected is with the Friend modifier as will be discussed in Chapter 3.

# Implementation or Behavior

The code inside a method is called the implementation. Sometimes it is also called behavior, as it is this code that actually makes the object do useful work. For instance, you might have an Age property as part of the object’s interface. Within that method, you might have code similar to the following:

```
Public ReadOnly Property Age() As Integer
```

In this case, the code is returning a value directly out of a variable, rather than doing something better, such as calculate the value based on a birth date. However, this kind of code is often written in applications, and it seems to work fine for a while.

The key point is to understand that client applications can use the object even if you change the implementation, as long as you do not change the public interface. If the method name and its parameter list and return data type remain unchanged, then you can change the implementation any way you want.

The code necessary to call the Age property would look something like this:

```
theAge = myObject.Age
```

The result of running this code is that you get the Age value returned. While the client application will work fine, you will soon discover that hard-coding the age into the application is a problem, so at some point you’ll want to improve this code. Fortunately, you can change the implementation without changing the client code:

```
Private _BirthDate As Date

Public ReadOnly Property Age() As Integer
    Get
        Return CInt(DateDiff(DateInterval.Year, _BirthDate, Now))
    End Get
End Property
```

You have changed the implementation behind the public interface, effectively changing how it behaves without changing the interface itself. Now, when you run the client application, the Age value returned is accurate over time, whereas in the previous implementation it was not.

Additionally, to implement this change you’ve moved from one of the new features of Visual Basic 2010 — auto-implemented properties, to a traditional property with a backing field implementation. Much of the existing .NET code you’ll see in Visual Basic will use a backing field for properties because up until this release that was the only way to implement a property.

Keep in mind that encapsulation is a syntactic tool — it enables the code to continue to run without change. However, it is not semantic, meaning that just because the code continues to run, that does not mean it continues to do what you actually want it to do.