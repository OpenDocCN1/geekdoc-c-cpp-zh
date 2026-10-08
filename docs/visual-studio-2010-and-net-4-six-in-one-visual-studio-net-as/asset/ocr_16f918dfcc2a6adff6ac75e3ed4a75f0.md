End Function

Private Sub PrivateHello()
    Call SayHelloWithGreetings("Hello from a private subroutine")
End Sub
End Module

Of these methods, only SayHello is a macro. The others are not, because SayHelloWithGreetings is a function, and PrivateHello is not public.

Beside the modules, you can use code settings in a class. For example, you can move the functionality of the SayHelloWithGreetings method into a separate class:

```
Imports System
Imports EnvDTE
Imports EnvDTE80
Imports EnvDTE90
Imports System.Diagnostics
Imports System.Windows.Forms
```

Public Class Greetings

```
Public Sub ShowGreetings(ByVal Greetings As String)
    MessageBox.Show(Greetings)
Sub
```

End Class

The SayHello method can be changed to use the Greetings class:

```
Imports System
Imports EnvDTE
Imports EnvDTE80
Imports EnvDTE90
Imports System.SimpleMacros
```

Public Module SimpleMacros

```
Public Sub SayHello()
    Dim greetings = New Greetings()
    greetings.ShowGreetings("Hello from a class")
End Sub
```

End Module

Classes also can contain macros, but, of course, they cannot be instances. Rather, use only shared (in C# terminology) methods with no input parameters and return values. So, if you put the ShowSimpleGreetings method into the previous Greetings class, it can be started as a macro:

```
Public Shared Sub ShowSimpleGreetings()
    MessageBox.Show("Greetings")
End Sub
```