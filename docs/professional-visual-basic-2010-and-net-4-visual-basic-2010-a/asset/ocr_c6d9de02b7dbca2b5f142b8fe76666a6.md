To create the socket, create an instance of TcpListener and give it a port. In your application, the port you are going to use is 10101. This port should be free on your computer, but if the debugger breaks on an exception when you instantiate TcpListener or call Start, then try another port. Once you have done that and called Start to configure the object to listen for connections, you drop into an infinite loop and call AcceptTcpClient. This method blocks until the socket is closed or a connection becomes available. If you get Nothing back, then either the socket is closed or there is a problem, so you drop out of the thread. If you get something back, then you pass the TcpClient over to your form through a call to the (not yet built) ReceiveInboundConnection method. Add this new method to the Listener class you created earlier:

```
' ThreadEntryPoint...
Protected Sub ThreadEntryPoint()
' Create a socket...
listener = New TcpListener(IPAddress.Loopback, ConnectForm.ServicePort)
listener.Start()
' Loop infinitely, waiting for connections.
Try
    Do While True
    ' Get a connection...
    Dim client As TcpClient = listener.AcceptTcpClient()
    If client Is Nothing Then
        Exit Do
    End If
    ' Process it...
    main.ReceiveInboundConnection(client)
Loop
Catch
    'eat any exceptions
End Try
End Sub
```

It is in the ReceiveInboundConnection method that you create the Conversation form that the user can use to send messages. You'll add this method to the form shortly.

# Creating Conversation Windows

When building Windows Forms applications that support threading, there is always the possibility of running into a problem with the Windows messaging subsystem. This is a very old part of Windows that powers the Windows user interface (the idea has been around since version 1.0 of the platform, although the implementation on modern Windows versions is far removed from the original).

Even those who are not familiar with old-school Windows programming, such as MFC, Win32, or even Win16 development, should be familiar with events. When you move a mouse over a form, you get MouseMove events. When you close a form, you get a Closed event. There is a mapping between these events and the messages that Windows passes around to support the actual display of the windows. For example, whenever you receive a MouseMove event, a message called WM_MOUSEMOVE is sent to the window by Windows, in response to the mouse driver. In .NET and other rapid application development (RAD) environments such as Visual Basic and Delphi, this message is converted into an event that you can write code against.

Although this is getting way off the topic — you know how to build Windows Forms applications by now and don't need the details of messages such as WM_NCHITTEST or WM_PAINT — it has an important implication. In effect, Windows creates a message queue for each thread into which it posts the messages that the thread's windows have to work with. This queue is looped on a virtually constant basis, and the messages are distributed to the appropriate window (remember that small controls such as buttons and text boxes are also windows). In .NET, these messages are turned into events, but unless the message queue is looped, the messages do not get through.