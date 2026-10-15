
```
Messagebox.Show("Caught any other errors")
Finally
Messagebox.Show(Str(intZ))
End Try
End Sub
```

Code snippet from ExceptionHandlingSampleCodeForm

As before, you catch the divide-by-zero error in the first Catch block, and the exception is stored in objA so that you can reference its properties later.

You throw a new exception with a more general message ("0 as divisor") that is easier to interpret, and you build up your stack by appending objA as the InnerException object using an overloaded constructor for the Exception object:

```
Throw (New Exception("0 as divisor", objA))
```

You catch your newly thrown exception in another Catch statement. Note how it does not catch a specific type of error:

```
Catch objB As Exception
```

Then you construct an error message for the new exception and display it in a message box:

```
Dim sError As String
sError = "My Message: " & objB.Message & vbCrLf & vbCrLf
sError &= "Inner Exception Message: " & _
objB.InnerException.Message & vbCrLf & vbCrLf
sError &= "Method Error Occurred: " & objB.TargetSite.Name
MessageBox.Show(sError)
```

Code snippet from ExceptionHandlingSampleCodeForm

The message box that is produced is shown in Figure 6-3.

First your own message is included, based on the new exception thrown by your own code. Then the InnerException gets the next exception in the stack, which is the divide-by-zero exception, and its message is included. Finally, the TargetSite property gives you the name of the method that threw the exception. TargetSite is particularly helpful in logs or error reports from users that are used by developers to track down unexpected problems.

![](img/d99870e80390742f93963da7be0b2e61_295_0.png)

FIGURE 6-3

After this message box, the Finally clause displays another message box that just shows the current value of intZ, which is zero because the divide failed. This second box also occurs in other examples that follow.

## Source and StackTrace

The Source and StackTrace properties provide the user with information regarding where the error occurred. This supplemental information can be invaluable, as the user can pass it on to the troubleshooter in order to help resolve errors more quickly. The following example uses these two properties and shows the feedback when the error occurs:

```
Sub HandlerExample2()
Dim intX As Integer
Dim intY As Integer
Dim intZ As Integer
intY = 0
intX = 5
' First Required Error Statement.
Try
' Cause a "Divide by Zero"
intZ = CType((intX \ intY), Integer)
' Catch the error.
Catch objA As System.DivideByZeroException
    objA.Source = "HandlerExample2"
    Messagebox.Show("Error Occurred at: " & _
        objA.Source & objA.StackTrace)
Finally
    Messagebox.Show(Str(intZ))
End Try
End Sub
```

Code snippet from ExceptionHandlingSampleCodeForm

The output from the Messagebox statement is very detailed, providing the entire path and line number where the error occurred, as shown in Figure 6-4.
Notice that this information is also included in the ToString method examined earlier (refer to Figure 6-1).

![](img/d99870e80390742f93963da7be0b2e61_296_0.png)

FIGURE 6-4

## GetBaseException

The GetBaseException method comes in very handy when you are deep in a set of thrown exceptions. This method returns the originating exception by recursively examining the InnerException until it reaches an exception object that has a null InnerException property. That exception is normally the exception that started the chain of unanticipated events.

In the following code, a chain of exceptions starts with a divide by zero, which results in exception object objA. The chain then continues with exception objects objB and objC, both created in code. Both of those last two exceptions are created by using a constructor on the Exception class that takes an argument for the InnerException of that new exception. Finally, the GetBaseException method is accessed on objC:

```
Sub HandlerExample3()
    Dim intX As Integer
    Dim intY As Integer
    Dim intZ As Integer
    intY = 0
    intX = 5
    ' First Required Error Statement.
    Try
        ' Cause a "Divide by Zero"
        intZ = CType((intX \ intY), Integer)
        ' Catch the error.
    Catch objA As System.DivideByZeroException
        Try
            Throw (New Exception("0 as divisor", objA))
        Catch objB As Exception
            Try
                Throw (New Exception("New error", objB))
            Catch objC As Exception
                Messagebox.Show(objC.GetBaseException.Message)
            End Try
        End Try
    Finally
        Messagebox.Show(Str(intZ))
    End Try
End Sub
```

Code snippet from ExceptionHandlingSampleCodeForm

The call objC.GetBaseException will trace back though the InnerException, for ObjC, which is objB, and then through objB's InnerException, which is the original exception, objA. However, objA has a null InnerException because it's an original exception caused by the divide by zero. Thus, objC.GetBaseException.Message returns the Message property of the original OverflowException message even though you've thrown multiple errors since the original error occurred:

```
MessageBox.Show(objC.GetBaseException.Message)
```

To put it another way, the code traverses back to the exception caught as objA and displays the same message as the objA.Message property would, as shown in Figure 6-5.

![](img/d99870e80390742f93963da7be0b2e61_297_0.png)

## HelpLink

The HelpLink property gets or sets the help link for a specific Exception object. It can be set to any string value, but it's typically set to a URL. If you create your own exception in code, you might want to set HelpLink to a URL (or a URN) describing the error in more detail. Then the code that catches the exception can go to that link. You could create and throw your own custom application exception with code like the following:

```
Dim exc As New ApplicationException("A short description of the problem")
exc.HelpLink = "http://mysite.com/somehtmlfile.htm"
Throw exc
```

Code snippet from ExceptionHandlingSampleCodeForm

When trapping an exception, the HelpLink can be used to launch a viewer so the user can see details about the problem. The following example shows this in action, using the built-in Explorer in Windows:

```
Sub HandlerExample4()
Try
    Dim exc As New ApplicationException("A short description of the problem")
    exc.HelpLink = "http://mysite.com/somehtmlfile.htm"
    Throw exc
    ' Catch the error.
Catch objA As System.Exception
    Shell("explorer.exe " & objA.HelpLink)
End Try
End Sub
```

Code snippet from ExceptionHandlingSampleCodeForm

This results in launching Internet Explorer to show the page specified by the URL. Most exceptions thrown by the CLR or the .NET Framework's classes have a blank HelpLink property. You should only count on using HelpLink if you have previously set it to a URL (or some other type of link information) yourself.

## INTEROPERABILITY WITH VB6-STYLE ERROR HANDLING

Because Visual Basic 2010 still supports the older On Error statement from pre-.NET versions of VB, you may encounter code that handles errors with On Error instead of with structured exception handling. You can use both techniques in a single program, but it is not possible to use both in a single routine. If you attempt to use both On Error and Try...Catch in a single routine, you will get a syntax error.

The Visual Basic compiler does allow the two techniques for handling errors to communicate with each other. For example, suppose you have a routine that uses Err.Raise to promote the error to the calling code. Also suppose that the calling code makes the call in a Try...Catch block. In that case, the error created by Err.Raise becomes an exception in the calling code and is trapped by a Catch block just as a normal exception would be. Here's a code example to illustrate. First, create a subroutine that creates an error with Err.Raise, like this:

```
Private Sub RaiseErrorWithErrRaise()
    Err.Raise(53)  ' indicates File Not Found
End Sub
```

Code snippet from ExceptionHandlingSampleCodeForm

Then call this routine from a button's Click event, with the call inside a Try...Catch block:

```
Private Sub Button2_Click(ByVal sender As System.Object, _
    ByVal e As System.EventArgs) Handles Button2.Click
    Try
        RaiseErrorWithErrRaise()
    Catch ex As Exception
        MessageBox.Show(ex.Message)
    End Try
End Sub
```

Code snippet from ExceptionHandlingSampleCodeForm

When the button is clicked, it will display a message box with "File Not Found." Even though the File Not Found error is raised by Err.Raise, it is translated to a .NET exception automatically.

Similarly, exceptions that are generated by a Throw statement in a called routine can be trapped by On Error in a calling routine. The exception is then translated into an Err object that works like the VB6 Err object.

## ERROR LOGGING

Error logging is important in many applications for thorough troubleshooting. It is common for end users of an application to forget exactly what an error said. Recording specific errors in a log enables you to get the specific error message without recreating the error.

While error logging is very important, you only want to use it to trap specific levels of errors because it carries overhead and can reduce the performance of your application. Specifically, log only errors that are critical to your application integrity — for instance, an error that would cause the data that the application is working with to become invalid.

There are three main approaches to error logging:

- Write error information in a text file or flat file located in a strategic location.
- Write error information to a central database.
- Write error information to the system's Event Logs, which are available on all versions of Windows supported by the .NET Framework 4. The .NET Framework includes a component that can be used to write to and read from the System, Application, and Security Logs on any given machine.

The type of logging you choose depends on the categories of errors you wish to trap and the types of machines on which you will run your application. If you choose to write to an Event Log, then you need to categorize the errors and write them in the appropriate log file. Resource-, hardware-, and system-level errors fit best into the System Event Log. Data access errors fit best into the Application Event Log. Permission errors fit best into the Security Event Log.

### The Event Log

Three Windows Event Logs are available: the System, Application, and Security Logs. Events in these logs can be viewed using the Event Viewer, which is accessed from the Control Panel. Access Administrative Tools and then select the Event Viewer subsection to view events. Typically, your applications would use the Application Event Log.
