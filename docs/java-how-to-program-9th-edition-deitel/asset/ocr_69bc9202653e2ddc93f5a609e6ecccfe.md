```
// Fig. 27.6: ServerTest.java
// Test the Server application.
import javax.swing.JFrame;

public class ServerTest
{
    public static void main( String[] args )
    {
        Server application = new Server(); // create server
        application.setDefaultCloseOperation( JFrame.EXIT_ON_CLOSE );
        application.runServer(); // run server application
    } // end main
} // end class ServerTest
```

Fig. 27.6 | Test class for Server.

# Method runServer

Method runServer (Fig. 27.5, lines 57–86) sets up the server to receive a connection and processes one connection at a time. Line 61 creates a ServerSocket called server to wait for connections. The ServerSocket listens for a connection from a client at port 12345. The second argument to the constructor is the number of connections that can wait in a queue to connect to the server (100 in this example). If the queue is full when a client attempts to connect, the server refuses the connection.

Common Programming Error 27.1
Specifying a port that's already in use or specifying an invalid port number when creating a ServerSocket results in a BindException.

Line 67 calls method waitForConnection (declared at lines 89–95) to wait for a client connection. After the connection is established, line 68 calls method getStreams (declared at lines 98–108) to obtain references to the connection's streams. Line 69 calls method processConnection (declared at lines 111–132) to send the initial connection message to the client and to process all messages received from the client. The finally block (lines 75–79) terminates the client connection by calling method closeConnection (lines 135–150), even if an exception occurs. These methods call displayMessage (lines 168–179), which uses the event-dispatch thread to display messages in the application's JTextArea. SwingUtilities method invokeLater receives a Runnable object as its argument and places it into the event-dispatch thread for execution. This ensures that we don't modify a GUI component from a thread other than the event-dispatch thread, which is important since Swing GUI components are not thread safe. We use a similar technique in method setTextFieldEditable (lines 182–193), to set the editability of enterField. For more information on interface Runnable, see Chapter 26.

# Method waitForConnection

Method waitForConnection (lines 89–95) uses ServerSocket method accept (line 92) to wait for a connection from a client. When a connection occurs, the resulting Socket is assigned to connection. Method accept blocks until a connection is received (i.e., the thread in which accept is called stops executing until a client connects). Lines 93–94 output the host name of the computer that made the connection. Socket method getInet-