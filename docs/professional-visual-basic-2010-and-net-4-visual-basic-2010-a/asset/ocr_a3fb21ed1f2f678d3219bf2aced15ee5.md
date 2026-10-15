You can also declare events as part of the interface by using the Event keyword:

```
Public Event AnEvent()
```

Finally, you can include actual variables, or attributes, as part of the interface:

```
Public AnInteger As Integer
```

This is strongly discouraged, because it directly exposes the internal variables for use by code outside the class. Because the variable is directly accessible from other code, you give up any and all control over the way the value may be changed or the code may be accessed.

Rather than make any variable Public, it is far preferable to make use of a Property method to expose the value. That way, you can implement code to ensure that your internal variable is set only to valid values and that only the appropriate code has access to the value based on your application’s logic.

# Using the Native Interface

Ultimately, the native (or primary) interface for any class is defined by looking at all the methods, properties, events, and variables that are declared as anything other than Private in scope. This includes any methods, properties, events, or variables that are inherited from a base class.

You are used to interacting with the default interface on most objects, so this should seem pretty straightforward. Consider this simple class:

```
Public Class TheClass
    Public Sub DoSomething()

    End Sub

    Public Sub DoSomethingElse()

    End Sub
End Class
```

> Code snippet from TheClass

This defines a class and, by extension, defines the native interface that is exposed by any objects you instantiate based on this class. The native interface defines two methods: DoSomething and DoSomethingElse. To make use of these methods, you simply call them:

```
Dim myObject As New TheClass()

myObject.DoSomething()

myObject.DoSomethingElse()
```

> Code snippet from Form1

This is the same thing you did in Chapter 2 and so far in this chapter. However, let’s take a look at creating and using secondary interfaces, because they are a bit different.

# Secondary Interfaces

Sometimes it’s helpful for an object to have more than one interface, thereby enabling you to interact with the object in different ways. Inheritance enables you to create subclasses that are specialized cases of the base class. For example, your Employee is a Person. Throughout this section we will be referencing the InheritanceAndInterfaces project we created earlier in this chapter.

However, sometimes you have a group of objects that are not the same thing, but you want to be able to treat them as though they were the same. You want all these objects to act as the same thing, even though they are all different.