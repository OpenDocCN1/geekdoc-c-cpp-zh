```
36    // get message from textfield
37    String message = event.getActionCommand();
38    displayArea.append( "\nSending packet containing: " +
39    message + "\n" );
40
41    byte[] data = message.getBytes(); // convert to bytes
42
43    // create sendPacket
44    DatagramPacket sendPacket = new DatagramPacket( data,
45    data.length, InetAddress.getLocalHost(), 5000 );
46
47    socket.send( sendPacket ); // send packet
48    displayArea.append( "Packet sent\n" );
49    displayArea.setCaretPosition(
50    displayArea.getText().length() );
51    } // end try
52    catch ( IOException ioException )
53    {
54    displayMessage( ioException + "\n" );
55    ioException.printStackTrace();
56    } // end catch
57    } // end actionPerformed
58    } // end inner class
59    ); // end call to addActionListener
60
61    add( enterField, BorderLayout.NORTH );
62
63    displayArea = new JTextArea();
64    add( new JScrollPane( displayArea ), BorderLayout.CENTER );
65
66    setSize( 400, 300 ); // set window size
67    setVisible( true ); // show window
68
69    try // create DatagramSocket for sending and receiving packets
70    {
71    socket = new DatagramSocket();
72    } // end try
73    catch ( SocketException socketException )
74    {
75    socketException.printStackTrace();
76    System.exit( 1 );
77    } // end catch
78    } // end Client constructor
79
80    // wait for packets to arrive from Server, display packet contents
81    public void waitForPackets()
82    {
83    while ( true )
84    {
85    try // receive packet and display contents
86    {
87    byte[] data = new byte[ 100 ]; // set up packet
```