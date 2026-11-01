```
' Visual Basic
Public Class MyClass2
  Public Sub Foo(ByVal i as Integer)
  End Sub
  Public Function Foo(ByVal i As Integer) As Integer
    Return 2 * i
  End Sub
End Class

// F#
type MyClass as this =
  member this.Foo(i : int) : int = i * 2
```

# Parameter Modifiers

By default, value types are passed by value, and reference types are passed by reference. If a value type that is passed as a parameter should be changed within a calling method, with C# you can use the parameter modifier ref.

C++/CLI defines a managed reference operator %. This operator is similar to the C++ reference operator & except that % can be used with managed types and the garbage collector can keep track of these objects in case they are moved within the managed heap.

With Visual Basic, the keyword ByRef is used for passing parameters by reference:

```
// C#
public class ParameterPassing
{
  public void ChangeVal(ref int i)
  {
    i = 3;
  }
}
```

```
// C++/CLI
public ref class ParameterPassing
{
public:
  int ChangeVal(int% i)
  {
    i = 3;
  }
};
```

```
' Visual Basic
Public Class ParameterPassing
  Public Sub ChangeVal(ByRef i as Integer)
    i = 3
  End Sub
End Class
```

When invoking a method with reference parameters, only the C# language requires you to apply a parameter modifier. C++/CLI and Visual Basic don't differentiate calling a method with or without the parameter modifier. C# has the advantage here because you can immediately see in the calling method that the parameter values can be changed.

Because of the caller syntax, which is not differentiated, Visual Basic does not allow you to overload methods just by changing the modifier. The C++/CLI compiler allows you to overload the method just by changing the modifier, but you cannot compile the caller because the resolved method is ambiguous.