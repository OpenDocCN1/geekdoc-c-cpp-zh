```
{
}

// C++/CLI
public ref class MyClass
{
public:
    void Foo()
    {
    }
};

' Visual Basic
Public Class MyClass1
    Public Sub Foo
    End Sub
End Class

// F# function
let foo x = x + 3
let add (x : int, y : int) : int = x + y

// method within a class
type MyClass as this =
    member this.Foo() =
        printfn "MyClass.Foo"
```

# Method Parameters and Return Types

With C# and C++/CLI, parameters that are passed to methods are defined inside a bracket. The type of the parameter is declared before the variable name. If a value is returned from a method, the method is defined with the type to return instead of void.

Visual Basic uses Sub statements to declare a method without returning a value, and the Function statement with a method that does have a return type. The return type is followed after the method name and the brackets. Visual Basic also has a different order with variable declaration and type in the parameter. The type follows the variable, which is the reverse direction from C# and C++/CLI.

With F#, if nothing is returned from a method, it is declared a unit. unit is similar to C# void. The method Foo is declared to receive an int parameter and returns an int:

```
// C#
public class MyClass
{
    public int Foo(int i)
    {
        return 2 * i;
    }
}

// C++/CLI
public ref class MyClass
{
public:
    int Foo(int i)
    {
        return 2 * i;
    }
};
```