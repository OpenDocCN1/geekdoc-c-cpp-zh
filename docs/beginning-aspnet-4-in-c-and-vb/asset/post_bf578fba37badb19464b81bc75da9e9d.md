
```
for (int i = 0; i < 100; i++)
{
    Console::WriteLine(i);
}

' Visual Basic
Dim count as Integer
For count = 0 To 99 Step 1
    Console.WriteLine(count)
Next

// F#
for i = 1 to 10 do
    printfn i
for i = 10 downto 1 do
    printfn i
```

## while and do...while Statements

The while and do...while statements are the same in C# and C++/CLI. Visual Basic has very similar constructs with Do While Loop and Do/Loop While. F# doesn't have a do/while but a while/do:

```
// C#
int i = 0;
while (i < 3)
{
    Console.WriteLine(i++);
}
i = 0;
do
{
    Console.WriteLine(i++);
} while (i < 3);
```

```
// C++/CLI
int i = 0;
while (i < 3)
{
    Console::WriteLine(i++);
}
i = 0;
do
{
    Console::WriteLine(i++);
} while (i < 3);
```

```
' Visual Basic
Dim num as Integer = 0
Do While (num < 3)
    Console.WriteLine(num)
    num += 1
Loop
num = 0
Do
    Console.WriteLine(num)
    num += 1
Loop While (num < 3)
```

```
// F#
let i = 0
let mutable looping = true
while looping do
```

```
try
{
    Method(null);
}
catch (ArgumentException ex)
{
}
catch (Exception ex)
{
}
finally
{
}
}
```

code snippet CSharp/ExceptionDemo.cs

```
// C++/CLI
public:
    void Method(Object* o)
    {
        if (o == nullptr)
            throw gcnew ArgumentException("Error");
    }
void Foo()
    {
        try
        {
            Method(nullptr);
        }
        catch (ArgumentException* ex)
        {
        }
        catch (Exception* ex)
        {
        }
        finally
        {
        }
    }
```

code snippet CPPCLI/ExceptionDemo.h

```
' Visual Basic
Public Sub Method(ByVal o As Object)
    If o = Nothing Then
        Throw New ArgumentException("Error")
    End Sub
Public Sub Foo()
    Try
        Method(Nothing)
    Catch ex As ArgumentException
    '
    Catch ex As Exception
    '
    Finally
    '
    End Try
End Sub
```

code snippet VisualBasic/ExceptionDemo.vb

```
// F#
type ExceptionDemo() as this =
    member this.Method(o : obj) =
        if o = null then
            raise(ArgumentException("error"))
    member this.Foo =
        try
            try
                this.Method(null)
            with
            | :? ArgumentException as ex -> printfn "%s" ex.Message
            | :? IOException as ex -> printfn "%s" ex.Message
        finally
            printfn "finally*"
```

code snippet FSharp/ExceptionDemo.fs

## INHERITANCE

.NET languages offer many keywords to define polymorphic behavior, to override or hide methods, access modifiers to allow or not allow member access. For C#, this functionality is discussed in Chapter 4, "Inheritance." The functionality of C#, C++/CLI, and Visual Basic is very similar, but the keywords are different.

### Access Modifiers

The access modifiers of C++/CLI, Visual Basic, and F# are very similar to C#, with some notable differences. Visual Basic uses the Friend access modifier instead of internal for accessing the types in the same assembly. C++/CLI has one more access modifier: protected private. An internal protected modifier allows accessing the members from within the same assembly, and also from other assemblies if the type is derived from the base type. C# and Visual Basic don't have a way to allow only derived types within the same assembly. This is possible with protected private from C++/CLI. Here private means that outside the assembly there's no access, but from inside the assembly protected access is possible. The order — whether you write protected private or private protected — does not matter. The access modifier allowing more is always located within the assembly, and the access modifier allowing less is always outside the assembly. F# uses three access modifiers but also allows the protected modifier if the type should be used from other .NET languages. Access modifiers can be declared in F# within signature files.

The following table lists the access modifiers for each of the languages.

| C# | C++/CLI | VISUAL BASIC | F# |
|---|---|---|---|
| public | Public | Public | public |
| protected | Protected | Protected |  |
| private | Private | Private | private |
| internal | Internal | Friend | internal |
| internal protected | internal protected | Protected Friend |  |
| not possible | protected private | not possible |  |

F# signature files have the file extension .fsi and define the signature of the members. They can be automatically created from code files with the --sig compiler option. According to the requirements, only the access modifiers need to be changed:

```
// F#
type public Person =
class
    interface IDisplay
    public new : unit -> Person
    public new : FirstName:string * lastName:string -> Person
    override ToString : unit -> string
    member public FirstName : string
    member public FirstName : string
    member public FirstName : string with set
    member public LastName : string with set
end
```

```
// release resource
}
}
```

code snippet CSharp/Resource.cs

```
// C++/CLI
public ref class Resource
{
public:
~Resource()
{
    // release resource
}
};
```

code snippet CPPCLI/Resource.h

```
' Visual Basic
Public Class Resource
Implements IDisposable
Public Sub Dispose() Implements IDisposable.Dispose
' release resource
End Sub
End Class
```

code snippet VisualBasic/Resource.vb

```
// F#
type Resource() as this =
    interface IDisposable with
    member this.Dispose() = printfn "release resource"
```

code snippet FSharp/Resource.fs

> With C++/CLI, the Dispose() method is invoked by using the delete statement.

## using Statement

The C# using statement implements an acquire/use/release pattern to release a resource as soon as it is no longer used, even in the case of an exception. The compiler creates a try/finally statement and invokes the Dispose method inside the finally. Visual Basic supports the using statement just as C# does. C++/CLI has an even more elegant approach to this problem. If a reference type is declared locally, the compiler creates a try/finally statement to invoke the Dispose() method at the end of the block. F# offers two different constructs to easily support resource management. The use binding automatically invokes the Dispose() method when the value goes out of scope. The using expression creates an object that must be disposed and it is disposed at the end of the function that is called. Here, the function bar is called after the Resource object is created:

```
// C#
using (Resource r = new Resource())
{
    r.Foo();
}

// C++/CLI
{
    Resource r;
    r.Foo();
```

```
} // handler implementation
}
//...
EventDemo evd = new EventDemo();
Subscriber subcr = new Subscriber();
evd.DemoEvent += subcr.Handler;
evd.FireEvent();
```

code snippet CSharp/EventDemo.cs

C++/CLI is very similar to C# except that when firing the event, you do not need to first check that the event variable is not null. This is automatically done by the IL code created from the compiler.

> Both C# and C++/CLI use the += operator to register for an event.

```
// C++/CLI
public ref class EventDemo
{
public:
event DemoDelegate^ DemoEvent;
public void FireEvent()
{
    DemoEvent(44);
}
}
public class Subscriber
{
public:
void Handler(int x)
{ // handler implementation
}
//...
EventDemo^ evd = gcnew EventDemo();
Subscriber^ subcr = gcnew Subscriber();
evd->DemoEvent += gcnew DemoDelegate(subcr, &Subscriber::Handler);
evd->FireEvent();
```

code snippet CPPCLI/EventDemo.h

Visual Basic has a different syntax. The event is declared with the Event keyword, which is the same as in C# and C++/CLI. However, the event is raised with the RaiseEvent statement. The RaiseEvent statement checks whether the event variable is initialized by a subscriber. To register a handler, the AddHandler statement has the same functionality as the += operator in C#. AddHandler requires two parameters: the first defines the event, the second the address of the handler. The RemoveHandler statement is used to unregister a handler from the event:

```
' Visual Basic
Public Class EventDemo
Public Event DemoEvent As DemoDelegate
public Sub FireEvent()
RaiseEvent DemoEvent(44);
End Sub
End Class
Public Class Subscriber
Public Sub Handler(ByVal x As Integer)
' handler implementation
```
