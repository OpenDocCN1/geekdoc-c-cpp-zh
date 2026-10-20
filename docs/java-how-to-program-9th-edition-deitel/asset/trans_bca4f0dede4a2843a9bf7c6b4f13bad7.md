
```java
133     try
134     {
135         output.close(); // close output stream
136         input.close(); // close input stream
137         client.close(); // close socket
138     } // end try
139     catch ( IOException ioException )
140     {
141         ioException.printStackTrace();
142     } // end catch
143 } // end method closeConnection
144
145 // send message to server
146 private void sendData( String message )
147 {
148     try // send object to server
149     {
150         output.writeObject( "CLIENT>> " + message );
151         output.flush(); // flush data to output
152         displayMessage( "\nCLIENT>> " + message );
153     } // end try
154     catch ( IOException ioException )
155     {
156         displayArea.append( "\nError writing object" );
157     } // end catch
158 } // end method sendData
159
160 // manipulates displayArea in the event-dispatch thread
161 private void displayMessage( final String messageToDisplay )
162 {
163     SwingUtilities.invokeLater(
164         new Runnable()
165         {
166             public void run() // updates displayArea
167             {
168                 displayArea.append( messageToDisplay );
169             } // end method run
170         } // end anonymous inner class
171     ); // end call to SwingUtilities.invokeLater
172 } // end method displayMessage
173
174 // manipulates enterField in the event-dispatch thread
175 private void setTextFieldEditable( final boolean editable )
176 {
177     SwingUtilities.invokeLater(
178         new Runnable()
179         {
180             public void run() // sets enterField's editability
181             {
182                 enterField.setEditable( editable );
183             } // end method run
184         } // end anonymous inner class
185     ); // end call to SwingUtilities.invokeLater
186 } // end method setTextFieldEditable
187 } // end class Client
```

Fig. 27.7 | Client portion of a stream-socket connection between client and server. (Part 5 of 5.)

```java
1  // Fig. 27.8: ClientTest.java
2  // Class that tests the Client.
3  import javax.swing.JFrame;
4
5  public class ClientTest
6  {
7      public static void main( String[] args )
8      {
9          Client application; // declare client application
10
11         // if no command line args
12         if ( args.length == 0 )
13             application = new Client( "127.0.0.1" ); // connect to localhost
14         else
15             application = new Client( args[ 0 ] ); // use args to connect
16
17         application.setDefaultCloseOperation( JFrame.EXIT_ON_CLOSE );
18         application.runClient(); // run client application
19     } // end main
20  } // end class ClientTest
```

![](img/009e962758dcc71dbc43a493362e6dc0_1178_0.png)

Fig. 27.8 | Class that tests the Client.

### Method runClient

Client method runClient (Fig. 27.7, lines 59–79) sets up the connection to the server, processes messages received from the server and closes the connection when communication is complete. Line 63 calls method connectToServer (declared at lines 82–92) to perform the connection. After connecting, line 64 calls method getStreams (declared at lines 95–105) to obtain references to the Socket’s stream objects. Then line 65 calls method processConnection (declared at lines 108–126) to receive and display messages sent from the server. The finally block (lines 75–78) calls closeConnection (lines 129–144) to close the streams and the Socket even if an exception occurred. Method displayMessage (lines 162–173) is called from these methods to use the event-dispatch thread to display messages in the application’s text area.

### Method connectToServer

Method connectToServer (lines 82–92) creates a Socket called client (line 87) to establish a connection. The arguments to the Socket constructor are the IP address of the server computer and the port number (12345) where the server application is awaiting client connections. In the first argument, InetAddress static method getByName returns an InetAddress object containing the IP address specified as a command-line argument to the application (or 127.0.0.1 if none was specified). Method getByName can receive a String containing either the actual IP address or the host name of the server. The first argument also could have been written other ways. For the localhost address 127.0.0.1, the first argument could be specified with either of the following expressions:

```java
InetAddress.getByName( "localhost" )
InetAddress.getLocalHost()
```

Other versions of the Socket constructor receive the IP address or host name as a String. The first argument could have been specified as the IP address "127.0.0.1" or the host name "localhost". We chose to demonstrate the client/server relationship by connecting between applications on the same computer (localhost). Normally, this first argument would be the IP address of another computer. The InetAddress object for another computer can be obtained by specifying the computer’s IP address or host name as the argument to InetAddress method getByName. The Socket constructor’s second argument is the server port number. This must match the port number at which the server is waiting for connections (called the handshake point). Once the connection is made, lines 90–91 display a message in the text area indicating the name of the server computer to which the client has connected.

The Client uses an ObjectOutputStream to send data to the server and an ObjectInputStream to receive data from the server. Method getStreams (lines 95–105) creates the ObjectOutputStream and ObjectInputStream objects that use the streams associated with the client socket.

### Methods processConnection and closeConnection

Method processConnection (lines 108–126) contains a loop that executes until the client receives the message "SERVER>>> TERMINATE". Line 117 reads a String object from the server. Line 118 invokes displayMessage to append the message to the text area. When the transmission is complete, method closeConnection (lines 129–144) closes the streams and the Socket.

### Processing User Interactions

When the client application user enters a String in the text field and presses Enter, the program calls method actionPerformed (lines 41–45) to read the String, then invokes utility method sendData (lines 147–159) to send the String to the server. Method sendData writes the object, flushes the output buffer and appends the same String to the client window’s JTextArea. Once again, it’s not necessary to invoke utility method displayMessage to modify the text area here, because method sendData is called from an event handler.

## 27.7 Datagrams: Connectionless Client/Server Interaction

We’ve been discussing connection-oriented, streams-based transmission. Now we consider connectionless transmission with datagrams.

Connection-oriented transmission is like the telephone system in which you dial and are given a connection to the telephone of the person with whom you wish to communicate. The connection is maintained for your phone call, even when you're not talking.

Connectionless transmission with datagrams is more like the way mail is carried via the postal service. If a large message will not fit in one envelope, you break it into separate pieces that you place in sequentially numbered envelopes. All of the letters are then mailed at once. The letters could arrive in order, out of order or not at all (the last case is rare). The person at the receiving end reassembles the pieces into sequential order before attempting to make sense of the message.

If your message is small enough to fit in one envelope, you need not worry about the “out-of-sequence” problem, but it’s still possible that your message might not arrive. One disadvantage of datagrams over postal mail is that duplicates of datagrams can arrive at the receiving computer.

Figures 27.9–27.12 use datagrams to send packets of information via the User Datagram Protocol (UDP) between a client application and a server application. In the Client application (Fig. 27.11), the user types a message into a text field and presses Enter. The program converts the message into a byte array and places it in a datagram packet that’s sent to the server. The Server (Figs. 27.9–27.10) receives the packet and displays the information in it, then echoes the packet back to the client. Upon receiving the packet, the client displays the information it contains.

### Server Class

Class Server (Fig. 27.9) declares two DatagramPackets that the server uses to send and receive information and one DatagramSocket that sends and receives the packets. The constructor (lines 19–37), which is called from main (Fig. 27.10, lines 7–12), creates the GUI in which the packets of information will be displayed. Line 30 creates the DatagramSocket in a try block. Line 30 in Fig. 27.9 uses the DatagramSocket constructor that takes an integer port-number argument (5000 in this example) to bind the server to a port where it can receive packets from clients. Clients sending packets to this Server specify the same port number in the packets they send. A SocketException is thrown if the DatagramSocket constructor fails to bind the DatagramSocket to the specified port.

### Common Programming Error 27.2

> Specifying a port that’s already in use or specifying an invalid port number when creating a DatagramSocket results in a SocketException.

```java
1  // Fig. 27.9: Server.java
2  // Server side of connectionless client/server computing with datagrams.
3  import java.io.IOException;
4  import java.net.DatagramPacket;
5  import java.net.DatagramSocket;
6  import java.net.SocketException;
7  import java.awt.BorderLayout;
8  import javax.swing.JFrame;
9  import javax.swing.JScrollPane;
10 import javax.swing.JTextArea;
```

