Finally, you must create the COM object, call the FireEvent method, and respond to the Timeout event notification. Listing 6.20 shows the code in the class file that performs these activities.

# LISTING 6.20 Class to Call Event Trigger and Handle Event Notification

```
Option Explicit
Dim WithEvents vbsink As VBSINKLib.MyEventSource
Attribute vbsink.VB_VarHelpID = -1

Private Sub Class_Initialize()

    Set vbsink = New VBSINKLib.MyEventSource

End Sub

Private Sub Class_Terminate()

    Set vbsink = Nothing

End Sub

Private Sub vbsink_Timeout()

    MsgBox "Timeout"

End Sub

Sub Go()

    vbsink.FireEvent 10

End Sub
```

The type of the vbsink object must be the type library name defined in your IDL file and the class name of your coclass, also defined in your IDL file. The COM class is created in the Class_Initialize() subroutine and destroyed in the Class_Terminate() subroutine. The Go() subroutine calls the FireEvent method of the COM object with a parameter indicating a 10-second delay before the timeout event is sent.

The most important part of this class file is the vbsink_Timeout() subroutine that receives the event notification. When Visual Basic receives the event notification, it looks for a subroutine name that matches the object name, followed by an underscore, followed by the notification method's name.

Run the VB executable and click the Trigger button. Ten seconds later, the event notification will be sent and a message box with the caption Timeout will be displayed. That's it.