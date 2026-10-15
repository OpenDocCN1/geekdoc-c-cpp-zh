> Rather than declare variables with Public or Friend scope, it is better to expose the value using a Property so that you can apply any of your business rules to control how the value is altered as appropriate.

Of course, you know that variables can be of Private scope, and this is typically the case. This makes the variables accessible only to the code within your class, and it is the most restrictive scope.

As with methods, however, you can also use the Protected scope when declaring variables. This makes the variable accessible to the code in your class and to the code in any class that derives from your class — all the way down the hierarchy chain.

Sometimes this is useful, because it enables you to provide and accept data to and from subclasses, but to act on that data from code in the base class. At the same time, exposing variables to subclasses is typically not ideal, and you should use Property methods with Protected scope for this instead, as they allow your base class to enforce any business rules that are appropriate for the value, rather than just hope that the author of the subclass provides only good values.

# Events and Inheritance

So far, we’ve discussed methods, properties, and variables in terms of inheritance — how they can be added, overridden, overloaded, and shadowed. In Visual Basic, events are also part of the interface of an object, and they are affected by inheritance as well.

# Inheriting Events

Chapter 2 discusses how to declare, raise, and receive events from objects. You can add such an event to the Person class by declaring it at the top of the class:

```
Public Class Person
    Private mName As String
    Private mBirthDate As String
    Private mID As String

    Public Event NameChanged(ByVal newName As String)
```

Code snippet from Person

Then, you can raise this event within the class anytime the person’s name is changed:

```
Public Overridable Property Name() As String
    Get
        Return mName
    End Get
    Set(ByVal value As String)
        mName = value
        RaiseEvent NameChanged(mName)
    End Set
End Property
```

Code snippet from Person

At this point, you can receive and handle this event within your form anytime you are working with a Person object. The nice thing about this is that your events are inherited automatically by subclasses — meaning your Employee and OfficeEmployee objects will also raise this event. Thus, you can change the code in your form to handle the event, even though you are working with an object of type OfficeEmployee.

First, you can add a method to handle the event to Form1: