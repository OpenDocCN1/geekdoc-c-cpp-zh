```
pos = posEnd + 1
End If
Loop While pos > 0

Return result
End Function
```

Code snippet from DefinePad

WebClient avoids all of the stream handling required for WebRequest. However, you should still know how WebRequest operates, as this knowledge is directly relatable to WebClient.

# SOCKETS

There may be times when you need to transfer data across a network (either a private network or the Internet) but the existing techniques and protocols do not exactly suit your needs. For example, you cannot download resources using the techniques discussed earlier in this chapter, and you cannot use Windows Communication Foundation, Web services, or remoting. In these cases, the best course of action is to roll your own protocol using sockets.

TCP/IP and, therefore, the Internet itself are based on sockets. The principle is simple: Establish a port at one end and allow clients to “plug in” to that port from the other end. Once the connection is made, applications can send and receive data through a stream. For example, HTTP nearly always operates on port 80, so a Web server opens a socket on port 80 and waits for incoming connections (Web browsers, unless told otherwise, attempt to connect to port 80 in order to make a request of that Web server).

In .NET, sockets are implemented in the System.Net.Sockets namespace and use classes from System.Net and System.IO to get the stream classes. Although working with sockets can be a little tricky outside of .NET, the framework includes classes that enable you to open a socket for inbound connections (System.Net.TcpListener) and for communication between two open sockets (System.Net.TcpClient). These two classes, in combination with some threading shenanigans, enable you to build your own protocol through which you can send any data you like. With your own protocol, you have ultimate control over the communication.

To demonstrate these techniques, you are going to build Wrox Messenger, a very basic instant messenger application similar to MSN Messenger.

# Building the Application

You will wrap all the functionality of your application into a single Windows application, which will act as both a server that waits for inbound connections and a client that has established outbound connections.

Create a new Windows Forms Application project called “WroxMessenger.” Change the title of Form1 to Wrox Messenger and add a TextBox control called ConnectToField and a Button control called ConnectButton. Set the name of the form to ConnectForm. The form should appear as shown in Figure 29-4.

![](bbox=[0.55, 0.68, 0.88, 0.76])

FIGURE 29-4

You will learn more about this in greater detail later, but for now it is very important that all of your UI code runs in the same thread, and that the thread is actually the main application that creates and runs your form.

To keep track of what is happening, you will add a field to the form that enables you to store the ID of the startup thread and report that ID on the caption. This helps provide a context for the thread/UI issues discussed later. You also need some namespace imports and a constant specifying the ID of the default port. Add the following code to your form:

```
Imports System.Net
Imports System.Net.Sockets
Imports System.Threading
Public Class ConnectForm
```