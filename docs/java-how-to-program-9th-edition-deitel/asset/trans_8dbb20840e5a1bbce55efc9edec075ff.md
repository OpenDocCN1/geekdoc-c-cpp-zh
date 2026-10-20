

Address 返回一个 InetAddress（包 java.net），其中包含有关客户端计算机的信息。InetAddress 方法 getHostName 返回客户端计算机的主机名。例如，特殊 IP 地址（127.0.0.1）和主机名（localhost）对于在本地计算机上测试网络应用程序非常有用（这也称为回环地址）。如果在包含 127.0.0.1 的 InetAddress 上调用 getHostName，则方法返回的相应主机名将为 localhost。

## Method getStreams

Method getStreams（第 98–108 行）获取 Socket 的流并分别用它们初始化 ObjectOutputStream（第 101 行）和 ObjectInputStream（第 105 行）。请注意第 102 行对 ObjectOutputStream 方法 flush 的调用。此语句会导致服务器上的 ObjectOutputStream 向相应客户端的 ObjectInputStream 发送流头。流头包含诸如用于发送对象的对象序列化版本等信息。ObjectInputStream 需要此信息，以便它可以准备正确接收这些对象。

## Software Engineering Observation 27.4

在使用 ObjectOutputStream 和 ObjectInputStream 通过网络连接发送和接收数据时，始终先创建 ObjectOutputStream 并刷新流，以便客户端的 ObjectInputStream 可以准备接收数据。这对于使用 ObjectOutputStream 和 ObjectInputStream 进行通信的网络应用程序是必需的。

## Performance Tip 27.3

计算机的 I/O 组件通常比其内存慢得多。输出缓冲区用于通过更少次数发送更多数据来提高应用程序的效率，从而减少应用程序访问计算机 I/O 组件的次数。

## Method processConnection

processConnection 方法（第 111–132 行）的第 114 行调用方法 sendData，将 "SERVER>>> Connection successful" 作为 String 发送给客户端。第 119–131 行的循环一直执行，直到服务器接收到消息 "CLIENT>>> TERMINATE"。第 123 行使用 ObjectInputStream 方法 readObject 从客户端读取一个 String。第 124 行调用方法 displayMessage 将消息附加到 JTextArea。

## Method closeConnection

传输完成后，method processConnection 返回，程序调用 method closeConnection（第 135–150 行）关闭与 Socket 关联的流并关闭 Socket。然后服务器通过继续执行 while 循环开始处的第 67 行等待来自客户端的下一次连接尝试。

服务器接收连接，处理它，关闭它并等待下一个连接。更可能的情况是，服务器接收到连接，将其设置为作为单独的执行线程进行处理，然后立即等待新的连接。处理现有连接的单独线程可以继续执行，同时服务器专注于新的连接请求。这使服务器更高效，因为可以并发处理多个客户端请求。我们在第 27.8 节中演示了多线程服务器。

## Processing User Interactions

当服务器应用程序的用户在文本字段中输入一个 `String` 并按下 *Enter* 键时，程序调用方法 `actionPerformed`（第 39–43 行），该方法从文本字段读取 `String` 并调用实用方法 `sendData`（第 153–165 行）将 `String` 发送给客户端。方法 `sendData` 写入对象，刷新输出缓冲区并将相同的 `String` 附加到服务器窗口中的文本区域。这里不需要调用 `displayMessage` 来修改文本区域，因为方法 `sendData` 是从事件处理程序调用的——因此，`sendData` 作为 *event-dispatch thread* 的一部分执行。

## Client Class

与类 Server 类似，类 Client 的构造函数（图 27.7，第 29–56 行）创建应用程序的 GUI（一个 `JTextField` 和一个 `JTextArea`）。Client 在文本区域显示其输出。当方法 `main`（图 27.8 的第 7–19 行）执行时，它创建类 Client 的一个实例，指定窗口的默认关闭操作并调用方法 `runClient`（图 27.7，第 59–79 行）。在此示例中，您可以从 Internet 上的任何计算机执行客户端，并将服务器计算机的 IP 地址或主机名指定为程序的命令行参数。例如，命令

```
java Client 192.168.1.15
```

尝试连接到 IP 地址为 192.168.1.15 的计算机上的 Server。

```
// Fig. 27.7: Client.java
// Client portion of a stream-socket connection between client and server.
import java.io.IOException;
import java.io.ObjectInputStream;
import java.io.ObjectOutputStream;
import java.net.InetAddress;
import java.net.Socket;
import java.awt.BorderLayout;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import javax.swing.JFrame;
import javax.swing.JScrollPane;
import javax.swing.JTextArea;
import javax.swing.JTextField;
import javax.swing.SwingUtilities;

public class Client extends JFrame
{
    private JTextField enterField; // enters information from user
    private JTextArea displayArea; // display information to user
    private ObjectOutputStream output; // output stream to server
    private ObjectInputStream input; // input stream from server
    private String message = ""; // message from server
    private String chatServer; // host server for this application
    private Socket client; // socket to communicate with server
}
```

**Fig. 27.7** | Client portion of a stream-socket connection between client and server. (Part 1 of 5.)

```
// initialize chatServer and set up GUI
public Client( String host )
{
    super( "Client" );

    chatServer = host; // set server to which this client connects

    enterField = new JTextField(); // create enterField
    enterField.setEditable( false );
    enterField.addActionListener(
        new ActionListener()
    {
        // send message to server
        public void actionPerformed( ActionEvent event )
        {
            sendData( event.getActionCommand() );
            enterField.setText( "" );
        } // end method actionPerformed
    } // end anonymous inner class
); // end call to addActionListener

    add( enterField, BorderLayout.NORTH );

    displayArea = new JTextArea(); // create displayArea
    add( new JScrollPane( displayArea ), BorderLayout.CENTER );

    setSize( 300, 150 ); // set size of window
    setVisible( true ); // show window
} // end Client constructor

// connect to server and process messages from server
public void runClient()
{
    try // connect to server, get streams, process connection
    {
        connectToServer(); // create a Socket to make connection
        getStreams(); // get the input and output streams
        processConnection(); // process connection
    } // end try
    catch ( EOFException eofException )
    {
        displayMessage( "\nClient terminated connection" );
    } // end catch
    catch ( IOException ioException )
    {
        ioException.printStackTrace();
    } // end catch
    finally
    {
        closeConnection(); // close connection
    } // end finally
} // end method runClient
```

```
// connect to server
private void connectToServer() throws IOException
{
    displayMessage( "Attempting connection\n" );

    // create Socket to make connection to server
    client = new Socket( InetAddress.getByName( chatServer ), 12345 );

    // display connection information
    displayMessage( "Connected to: " +
        client.getInetAddress().getHostName() );
} // end method connectToServer

// get streams to send and receive data
private void getStreams() throws IOException
{
    // set up output stream for objects
    output = new ObjectOutputStream( client.getOutputStream() );
    output.flush(); // flush output buffer to send header information

    // set up input stream for objects
    input = new ObjectInputStream( client.getInputStream() );

    displayMessage( "\nGot I/O streams\n" );
} // end method getStreams

// process connection with server
private void processConnection() throws IOException
{
    // enable enterField so client user can send messages
    setTextFieldEditable( true );

    do // process messages sent from server
    {
        try // read message and display it
        {
            message = ( String ) input.readObject(); // read new message
            displayMessage( "\n" + message ); // display message
        } // end try
        catch ( ClassNotFoundException classNotFoundException )
        {
            displayMessage( "\nUnknown object type received" );
        } // end catch

    } while ( !message.equals( "SERVER>>> TERMINATE" ) );
} // end method processConnection

// close streams and socket
private void closeConnection()
{
    displayMessage( "\nClosing connection" );
    setTextFieldEditable( false ); // disable enterField

