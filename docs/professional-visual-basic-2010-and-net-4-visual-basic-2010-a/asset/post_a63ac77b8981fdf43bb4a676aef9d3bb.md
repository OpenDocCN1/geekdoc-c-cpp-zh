
All of the DownloadX and UploadX methods also support an asynchronous version of the method, called DownloadXAsync, such as DownloadFileAsync or UploadValuesAsync. These methods perform the actual request on a background thread, and fire an event when the task is completed. If your application has some form of user interface, such as a form, then you should generally use these methods to keep your application responsive.

As the WebClient class uses the WebRequest classes to actually perform its magic, it can greatly simplify network coding. For example, just replace the code used in the WebRequest sample created earlier.

**Before:**

```vbnet
Public Function Define(ByVal word As String) As String()
    Dim req As HttpWebRequest = Nothing
    Dim resp As HttpWebResponse
    Dim query As String
    Dim result As New List(Of String)
    query = "http://www.google.com/search?q=define%3A" & _
    HttpUtility.UrlEncode(word)
    Try
        req = DirectCast(WebRequest.Create(query), HttpWebRequest)
        With req
            .Method = "GET"
            resp = req.GetResponse
            If resp.StatusCode = HttpStatusCode.OK Then
                ParseResponse(resp.GetResponseStream, result)
            Else
                MessageBox.Show("Error calling definition service")
            End If
        End With
    Catch ex As Exception
    End Try
    Return result.ToArray()
End Function
```

*Code snippet from DefinePad*

**After:**

```vbnet
Public Function Define(ByVal word As String) As String()
    Dim client As New WebClient
    Dim query As String
    Dim result As New List(Of String)
    query = "http://www.google.com/search?q=define%3A" & _
    HttpUtility.UrlEncode(word)
    Try
        result = ParseResponse(client.DownloadString(query))
    Catch ex As Exception
    End Try
    Return result.ToArray()
End Function

Private Function ParseResponse(ByVal data As String) As List(Of String)
    Dim result As New List(Of String)
    Dim blockStart As String = "<p>Definitions of"
    Dim pos As Integer = data.IndexOf(blockStart)
    Dim posEnd As Integer
    Dim temp As String
    Do
        pos = data.IndexOf("<li>", pos + 1)
        If pos > 0 Then
            posEnd = data.IndexOf("<br>", pos)
            temp = data.Substring(pos + 4, posEnd - pos - 4)
            result.Add(ParseDefinition(temp))
            pos = posEnd + 1
        End If
    Loop While pos > 0

    Return result
End Function
```

*Code snippet from DefinePad*

WebClient avoids all of the stream handling required for WebRequest. However, you should still know how WebRequest operates, as this knowledge is directly relatable to WebClient.

## SOCKETS

There may be times when you need to transfer data across a network (either a private network or the Internet) but the existing techniques and protocols do not exactly suit your needs. For example, you cannot download resources using the techniques discussed earlier in this chapter, and you cannot use Windows Communication Foundation, Web services, or remoting. In these cases, the best course of action is to roll your own protocol using sockets.

TCP/IP and, therefore, the Internet itself are based on sockets. The principle is simple: Establish a port at one end and allow clients to “plug in” to that port from the other end. Once the connection is made, applications can send and receive data through a stream. For example, HTTP nearly always operates on port 80, so a Web server opens a socket on port 80 and waits for incoming connections (Web browsers, unless told otherwise, attempt to connect to port 80 in order to make a request of that Web server).

In .NET, sockets are implemented in the System.Net.Sockets namespace and use classes from System.Net and System.IO to get the stream classes. Although working with sockets can be a little tricky outside of .NET, the framework includes classes that enable you to open a socket for inbound connections (System.Net.TcpListener) and for communication between two open sockets (System.Net.TcpClient). These two classes, in combination with some threading shenanigans, enable you to build your own protocol through which you can send any data you like. With your own protocol, you have ultimate control over the communication.

To demonstrate these techniques, you are going to build Wrox Messenger, a very basic instant messenger application similar to MSN Messenger.

### Building the Application

You will wrap all the functionality of your application into a single Windows application, which will act as both a server that waits for inbound connections and a client that has established outbound connections.

Create a new Windows Forms Application project called “WroxMessenger.” Change the title of Form1 to Wrox Messenger and add a TextBox control called ConnectToField and a Button control called ConnectButton. Set the name of the form to ConnectForm. The form should appear as shown in Figure 29-4.

![](img/d99870e80390742f93963da7be0b2e61_961_0.png)

FIGURE 29-4

You will learn more about this in greater detail later, but for now it is very important that all of your UI code runs in the same thread, and that the thread is actually the main application that creates and runs your form.

To keep track of what is happening, you will add a field to the form that enables you to store the ID of the startup thread and report that ID on the caption. This helps provide a context for the thread/UI issues discussed later. You also need some namespace imports and a constant specifying the ID of the default port. Add the following code to your form:

```vbnet
Imports System.Net
Imports System.Net.Sockets
Imports System.Threading
Public Class ConnectForm
    Private Shared _mainThreadId As Integer
    Public Const ServicePort As Integer = 10101
```

Next, create a New method for the form and add this code to the constructor that populates the field and changes the caption:

```vbnet
Public Sub New()
    ' This call is required by the Windows Form Designer.
    InitializeComponent()
    ' Add any initialization after the InitializeComponent() call.
    _mainThreadId = System.Threading.Thread.CurrentThread.GetHashCode()
    Text &= "-" & _mainThreadId.ToString()
End Sub
```

To listen for incoming connections, you will create a separate class called Listener. This class uses an instance of System.Net.Sockets.TcpListener to wait for incoming connections. Specifically, it opens a TCP port that any client can connect to — sockets are not platform-specific. Although connections are always made on a specific, known port, the actual communication takes place on a port of the TCP/IP subsystem’s choosing, which means you can support many inbound connections at once, despite the fact that each of them connects to the same port. Sockets are an open standard available on pretty much any platform. For example, if you publish the specification for your protocol, then developers working on Linux can connect to your Wrox Messenger service.

When you detect an inbound connection, you are given a System.Net.Sockets.TcpClient object. This is your gateway to the remote client. To send and receive data, you need to obtain a System.Net.NetworkStream object (returned through a call to GetStream on TcpClient), which returns a stream that you can use.

Create a new class called Listener. This thread needs members to hold an instance of a System.Threading.Thread object, and a reference back to the ConnectForm class that is the main form in the application. Not covered here is how to spin up and down threads, or synchronization. (Refer to Chapter 33 if you need more information about that.)

Here is the basic code for the Listener class:

```vbnet
Imports System.Net.Sockets
Imports System.Threading
Imports System.Net

Public Class Listener
    Implements IDisposable

    Private main As ConnectForm
    Private listener As TcpListener
    Private thread As Thread
    Public Sub New(ByVal main As ConnectForm)
        Me.main = main
    End Sub
    Public Sub SpinUp()
        ' create and start the new thread...
        thread = New Thread(AddressOf ThreadEntryPoint)
        thread.Start()
    End Sub
End Class
```

The obvious missing method here is ThreadEntryPoint. This is where you need to create the socket and wait for inbound connections. When you get them, you are given a TcpClient object, which you pass back to your form, where the conversation window can be created. You create this method in the Listener.vb class file.
