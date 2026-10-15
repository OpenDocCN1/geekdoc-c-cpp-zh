Now this class also implements the `IShared` interface, and you are ready to see polymorphism implemented in your code. Bring up the code window for `Form1` and change your `ShowDistance` method as follows:

```
Private Sub ShowDistance(ByVal obj As IShared)
    MsgBox(obj.CalculateDistance(10, 10))
End Sub
```

Note that this eliminates the compiler error you saw after removing the `Option Strict` directive from Form1.

Instead of accepting the parameter using the generic `Object` data type, you are now accepting an `IShared` parameter — a strong data type known by both the IDE and the compiler. Within the code itself, you are calling the `CalculateDistance` method as defined by that interface.

This routine can now accept any object that implements `IShared`, regardless of what class that object was created from or what other interfaces that object may implement. All you care about here is that the object implements `IShared`.

# Polymorphism through Reflection

You have learned how to use late binding to invoke a method on any arbitrary object as long as that object has a method matching the method signature you are trying to call. You have also walked through the use of multiple interfaces, which enables you to achieve polymorphism through a faster, early-bound technique. The challenge with these techniques is that late binding can be slow and hard to debug, and multiple interfaces can be somewhat rigid and inflexible.

Enter reflection. Reflection is a technology built into the .NET Framework that enables you to write code that interrogates an assembly to dynamically determine the classes and data types it contains. Using reflection, you can load the assembly into your process, create instances of those classes, and invoke their methods.

When you use late binding, Visual Basic makes use of the `System.Reflection` namespace behind the scenes on your behalf. The `System.Reflection` namespace can give you insight into classes by enabling to traverse information about an assembly or class. You can choose to manually use reflection as well. This gives you even more flexibility in terms of how you interact with objects.

For example, suppose that the class you want to call is located in some other assembly on disk — an assembly you did not specifically reference from within your project when you compiled it. How can you dynamically find, load, and invoke such an assembly? Reflection enables you to do this, assuming that the assembly is polymorphic. In other words, it has either an interface you expect or a set of methods you can invoke via late binding.

To see how reflection works with late binding, we’ll create a new class in a separate assembly (project) and use it from within the existing application. Choose File ⇨ Add ⇨ New Project to add a new Class Library project to your solution. Name it “Objects.” It begins with a single class module that you can use as a starting point. Change the code in that class to the following:

```
Public Class External
    Public Function DistanceTo(ByVal x As Single, ByVal y As Single) As Single
        Return x * y
    End Function
End Class
```

![](bbox=[0.753, 0.778, 0.931, 0.802])

Now compile the assembly by choosing Build ⇨ Build Objects. Next, bring up the code window for Form1. Add an Imports statement at the top, and add back the Option Strict Off statement:

```
Option Strict Off
Imports System.Reflection
```

Remember that because you are using late binding, Form1 also must use `Option Strict Off`. Otherwise, late binding isn’t available.