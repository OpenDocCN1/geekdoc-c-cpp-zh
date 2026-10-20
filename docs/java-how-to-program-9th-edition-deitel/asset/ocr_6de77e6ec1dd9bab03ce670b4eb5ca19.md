When this occurs, the program calls method actionPerformed (Fig. 27.11, lines 32–57), which converts the String the user entered into a byte array (line 41). Lines 44–45 create a DatagramPacket and initialize it with the byte array, the length of the String that was entered by the user, the IP address to which the packet is to be sent (InetAddress.getLocalHost() in this example) and the port number at which the Server is waiting for packets (5000 in this example). Line 47 sends the packet. The client in this example must know that the server is receiving packets at port 5000—otherwise, the server will not receive the packets.

The DatagramSocket constructor call (Fig. 27.11, line 71) in this application does not specify any arguments. This no-argument constructor allows the computer to select the next available port number for the DatagramSocket. The client does not need a specific port number, because the server receives the client’s port number as part of each DatagramPacket sent by the client. Thus, the server can send packets back to the same computer and port number from which it receives a packet of information.

```
1  // Fig. 27.11: Client.java
2  // Client side of connectionless client/server computing with datagrams.
3  import java.io.IOException;
4  import java.net.DatagramPacket;
5  import java.net.DatagramSocket;
6  import java.net.InetAddress;
7  import java.net.SocketException;
8  import java.awt.BorderLayout;
9  import java.awt.event.ActionEvent;
10 import java.awt.event.ActionListener;
11 import javax.swing.JFrame;
12 import javax.swing.JScrollPane;
13 import javax.swing.JTextArea;
14 import javax.swing.JTextField;
15 import javax.swing.SwingUtilities;
16 
17 public class Client extends JFrame
18 {
19     private JTextField enterField; // for entering messages
20     private JTextArea displayArea; // for displaying messages
21     private DatagramSocket socket; // socket to connect to server
22 
23     // set up GUI and DatagramSocket
24     public Client()
25     {
26         super( "Client" );
27 
28         enterField = new JTextField( "Type message here" );
29         enterField.addActionListener(
30             new ActionListener()
31             {
32                 public void actionPerformed( ActionEvent event )
33                 {
34                     try // create and send packet
35                     {

```