> Note The code segment [<Optional;DefaultParameterValue(0)>] contains two attributes. One is OptionalAttribute, and the other is DefaultParameterValue.

It's easy to invoke C# method with an optional parameter from the F# side. Listing 2-15 shows how to invoke a C# method with an optional parameter.

**LISTING 2-15** Invoking a C# method with an optional parameter from F#

```
C# code defining a method with an optional parameter
public class CSharpClass
{
    public void MyMethod(int a = 11)
    {
        Console.WriteLine("{0}", a);
    }
}

F# code invoking a C# method with an optional parameter
let c = ConsoleApplication1.CSharpClass()
c.MyMethod()
c.MyMethod(100)
c.MyMethod(a=199)

Execution result from F# code
a = 11
a = 100
a = 199
```

# # Defining a Static Method

We have converted the *field, property, and member* methods from C# to F#. We can now convert the static method *FromXY*. In C#, the *static* keyword is needed to define a static method. One approach to accomplishing this is to use a tuple, and another is to define two independent parameters. If you recall the design principle mentioned in the “Defining Tuples” section in Chapter 1, “C# and F# Data Structures,” the tuple approach is a better choice because it requires that both *x* and *y* be passed together. The F# code is shown in Listing 2-16.