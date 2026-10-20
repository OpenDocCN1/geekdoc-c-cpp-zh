# 27.1 Introduction

+   - 27.1 Introduction
+   - 27.2 Manipulating URLs
+   - 27.3 Reading a File on a Web Server
+   - 27.4 Establishing a Simple Server Using Stream Sockets
+   - 27.5 Establishing a Simple Client Using Stream Sockets
+   - 27.6 Client/Server Interaction with Stream Socket Connections
+   - 27.7 Datagrams: Connectionless Client/Server Interaction
+   - 27.8 Client/Server Tic-Tac-Toe Using a Multithreaded Server
+   - 27.9 [Web Bonus] Case Study: DeitelMessenger
+   - 27.10 Wrap-Up

Summary | Self-Review Exercises | Answers to Self-Review Exercises | Exercises

Java provides a number of built-in networking capabilities that make it easy to develop Internet-based and web-based applications. Java can enable programs to search the world for information and to collaborate with programs running on other computers internationally, nationally or just within an organization (subject to security constraints).

Java’s fundamental networking capabilities are declared by the classes and interfaces of package java.net, through which Java offers stream-based communications that enable applications to view networking as streams of data. The classes and interfaces of package java.net also offer packet-based communications for transmitting individual packets of information—commonly used to transmit data images, audio and video over the Internet. In this chapter, we show how to communicate with packets and streams of data.

We focus on both sides of the client/server relationship. The client requests that some action be performed, and the server performs the action and responds to the client. A common implementation of the request-response model is between web browsers and web servers. When a user selects a website to browse through a browser (the client application), a request is sent to the appropriate web server (the server application). The server normally responds to the client by sending an appropriate web page to be rendered by the browser.

We introduce Java’s socket-based communications, which enable applications to view networking as if it were file I/O—a program can read from a socket or write to a socket as simply as reading from a file or writing to a file. The socket is simply a software construct that represents one endpoint of a connection. We show how to create and manipulate stream sockets and datagram sockets.

With stream sockets, a process establishes a connection to another process. While the connection is in place, data flows between the processes in continuous streams. Stream sockets are said to provide a connection-oriented service. The protocol used for transmission is the popular TCP (Transmission Control Protocol).

With datagram sockets, individual packets of information are transmitted. The protocol used—UDP, the User Datagram Protocol—is a connectionless service and does not guarantee that packets arrive in any particular order. With UDP, packets can even be lost or duplicated. Significant extra programming is required on your part to deal with these problems (if you choose to do so). UDP is most appropriate for network applications that