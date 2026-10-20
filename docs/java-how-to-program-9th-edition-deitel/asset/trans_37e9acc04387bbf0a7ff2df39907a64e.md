

validMove 返回 false。否则，服务器在自己对棋盘的本地表示中为玩家放置一个标记（第 142 行），通知另一个 Player 对象（第 146 行）已做出移动（以便可以将消息发送给客户端），调用 signal 方法（第 152 行）以便等待的 Player（如果有的话）可以验证移动并返回 true（第 159 行）以指示移动有效。

## TicTacToeClient 类

每个 TicTacToeClient 应用程序（图 27.15–27.16；示例输出见图 27.17）维护自己 GUI 版本的井字棋棋盘，在其上显示游戏状态。客户端只能在空方格中放置标记。内部类 Square（图 27.15，第 205–261 行）实现了棋盘上的九个方格中的每一个。当 TicTacToeClient 开始执行时，它会创建一个 JTextArea，用来显示来自服务器的消息以及使用九个 Square 对象表示的棋盘。startClient 方法（第 80–100 行）打开与服务器的连接并从 Socket 对象获取关联的输入和输出流。第 85–86 行建立与服务器的连接。类 TicTacToeClient 实现接口 Runnable，以便单独的线程可以从服务器读取消息。这种方法使用户能够在等待来自服务器的消息的同时与棋盘交互（在事件分发线程中）。在建立与服务器的连接后，第 99 行使用 worker ExecutorService 执行客户端。run 方法（第 103–126 行）控制单独的执行线程。该方法首先从服务器读取标记字符（X 或 O）（第 105 行），然后连续循环（第 121–125 行）并从服务器读取消息（第 124 行）。每条消息都传递给 processMessage 方法（第 129–156 行）进行处理。

```java
// Fig. 27.15: TicTacToeClient.java
// Client side of client/server Tic-Tac-Toe program.
import java.awt.BorderLayout;
import java.awt.Dimension;
import java.awt.Graphics;
import java.awt.GridLayout;
import java.awt.event.MouseAdapter;
import java.awt.event.MouseEvent;
import java.net.Socket;
import java.net.InetAddress;
import java.io.IOException;
import javax.swing.JFrame;
import javax.swing.JPanel;
import javax.swing.JScrollPane;
import javax.swing.JTextArea;
import javax.swing.JTextField;
import javax.swing.SwingUtilities;
import java.util.Formatter;
import java.util.Scanner;
import java.util.concurrent.Executors;
import java.util.concurrent.ExecutorService;

public class TicTacToeClient extends JFrame implements Runnable
{
    private JTextField idField; // textfield to display player's mark
    private JTextArea displayArea; // JTextArea to display output
    private JPanel boardPanel; // panel for tic-tac-toe board
    private JPanel panel2; // panel to hold board
    private Square[][] board; // tic-tac-toe board
    private Square currentSquare; // current square
    private Socket connection; // connection to server
    private Scanner input; // input from server
    private Formatter output; // output to server
    private String ticTacToeHost; // host name for server
    private String myMark; // this client's mark
    private boolean myTurn; // determines which client's turn it is
    private final String X_MARK = "X"; // mark for first client
    private final String O_MARK = "O"; // mark for second client

    // set up user-interface and board
    public TicTacToeClient( String host )
    {
        ticTacToeHost = host; // set name of server
        displayArea = new JTextArea( 4, 30 ); // set up JTextArea
        displayArea.setEditable( false );
        add( new JScrollPane( displayArea ), BorderLayout.SOUTH );

        boardPanel = new JPanel(); // set up panel for squares in board
        boardPanel.setLayout( new GridLayout( 3, 3, 0, 0 ) );

        board = new Square[ 3 ][ 3 ]; // create board

        // loop over the rows in the board
        for ( int row = 0; row < board.length; row++ )
        {
            // loop over the columns in the board
            for ( int column = 0; column < board[ row ].length; column++ )
            {
                // create square
                board[ row ][ column ] = new Square( " ", row * 3 + column );
                boardPanel.add( board[ row ][ column ] ); // add square
            } // end inner for
        } // end outer for

        idField = new JTextField(); // set up textfield
        idField.setEditable( false );
        add( idField, BorderLayout.NORTH );

        panel2 = new JPanel(); // set up panel to contain boardPanel
        panel2.add( boardPanel, BorderLayout.CENTER ); // add board panel
        add( panel2, BorderLayout.CENTER ); // add container panel

        setSize( 300, 225 ); // set size of window
        setVisible( true ); // show window

        startClient();
    } // end TicTacToeClient constructor
```

```java
    // valid move occurred
    if ( message.equals( "Valid move." ) )
    {
        displayMessage( "Valid move, please wait.\n" );
        setMark( currentSquare, myMark ); // set mark in square
    } // end if
    else if ( message.equals( "Invalid move, try again" ) )
    {
        displayMessage( message + "\n" ); // display invalid move
        myTurn = true; // still this client's turn
    } // end else if
    else if ( message.equals( "Opponent moved" ) )
    {
        int location = input.nextInt(); // get move location
        input.nextLine(); // skip newline after int location
        int row = location / 3; // calculate row
        int column = location % 3; // calculate column

        setMark( board[ row ][ column ],
            ( myMark.equals( X_MARK ) ? O_MARK : X_MARK ) ); // mark move
        displayMessage( "Opponent moved. Your turn.\n" );
        myTurn = true; // now this client's turn
    } // end else if
    else
        displayMessage( message + "\n" ); // display the message
} // end method processMessage

// manipulate displayArea in event-dispatch thread
private void displayMessage( final String messageToDisplay )
{
    SwingUtilities.invokeLater(
        new Runnable()
        {
            public void run()
            {
                displayArea.append( messageToDisplay ); // updates output
            } // end method run
        } // end anonymous inner class
    ); // end call to SwingUtilities.invokeLater
} // end method displayMessage

// utility method to set mark on board in event-dispatch thread
private void setMark( final Square squareToMark, final String mark )
{
    SwingUtilities.invokeLater(
        new Runnable()
        {
            public void run()
            {
                squareToMark.setMark( mark ); // set mark in square
            } // end method run
        } // end anonymous inner class
    ); // end call to SwingUtilities.invokeLater
} // end method setMark

// send message to server indicating clicked square
public void sendClickedSquare( int location )
{
    // if it is my turn
    if ( myTurn )
    {
        output.format( "%d\n", location ); // send location to server
        output.flush();
        myTurn = false; // not my turn any more
    } // end if
} // end method sendClickedSquare

// set current Square
public void setCurrentSquare( Square square )
{
    currentSquare = square; // set current square to argument
} // end method setCurrentSquare

// private inner class for the squares on the board
private class Square extends JPanel
{
    private String mark; // mark to be drawn in this square
    private int location; // location of square

    public Square( String squareMark, int squareLocation )
    {
        mark = squareMark; // set mark for this square
        location = squareLocation; // set location of this square

        addMouseListener(
            new MouseAdapter()
            {
                public void mouseReleased( MouseEvent e )
                {
                    setCurrentSquare( Square.this ); // set current square

                    // send location of this square
                    sendClickedSquare( getSquareLocation() );
                } // end method mouseReleased
            } // end anonymous inner class
        ); // end call to addMouseListener
    } // end Square constructor

    // return preferred size of Square
    public Dimension getPreferredSize()
    {
        return new Dimension( 30, 30 ); // return preferred size
    } // end method getPreferredSize
```

