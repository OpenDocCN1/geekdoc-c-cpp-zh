
```java
DatagramPacket receivePacket = new DatagramPacket(
    data, data.length );

socket.receive( receivePacket ); // wait for packet

// display packet contents
displayMessage( "\nPacket received:" +
    "\nFrom host: " + receivePacket.getAddress() +
    "\nHost port: " + receivePacket.getPort() +
    "\nLength: " + receivePacket.getLength() +
    "\nContaining:\n\t" + new String( receivePacket.getData(),
        0, receivePacket.getLength() ) );
} // end try
catch ( IOException exception )
{
    displayMessage( exception + "\n" );
    exception.printStackTrace();
} // end catch
} // end while
} // end method waitForPackets

// manipulates displayArea in the event-dispatch thread
private void displayMessage( final String messageToDisplay )
{
    SwingUtilities.invokeLater(
        new Runnable()
        {
            public void run() // updates displayArea
            {
                displayArea.append( messageToDisplay );
            } // end method run
        } // end inner class
    ); // end call to SwingUtilities.invokeLater
} // end method displayMessage
} // end class Client
```

**Fig. 27.11** | Client side of connectionless client/server computing with datagrams. (Part 3 of 3.)

```java
// Fig. 27.12: ClientTest.java
// Tests the Client class.
import javax.swing.JFrame;

public class ClientTest
{
    public static void main( String[] args )
    {
        Client application = new Client(); // create Client
        application.setDefaultCloseOperation( JFrame.EXIT_ON_CLOSE );
        application.waitForPackets(); // run client application
    } // end main
} // end class ClientTest
```

**Fig. 27.12** | Class that tests the Client. (Part 1 of 2.)

![](img/009e962758dcc71dbc43a493362e6dc0_1187_0.png)

**Fig. 27.12** | Class that tests the Client. (Part 2 of 2.)

### Method waitForPackets

Client method waitForPackets (lines 81–107) uses an infinite loop to wait for packets from the server. Line 91 blocks until a packet arrives. This does not prevent the user from sending a packet, because the GUI events are handled in the event-dispatch thread. It only prevents the while loop from continuing until a packet arrives at the Client. When a packet arrives, line 91 stores it in receivePacket, and lines 94–99 call method displayMessage (declared at lines 110–121) to display the packet’s contents in the text area.

## 27.8 Client/Server Tic-Tac-Toe Using a Multithreaded Server

This section presents the popular game Tic-Tac-Toe implemented by using client/server techniques with stream sockets. The program consists of a TicTacToeServer application (Figs. 27.13–27.14) that allows two TicTacToeClient applications (Figs. 27.15–27.16) to connect to the server and play Tic-Tac-Toe. Sample outputs are shown in Fig. 27.17.

### TicTacToeServer Class

As the TicTacToeServer receives each client connection, it creates an instance of inner-class Player (Fig. 27.13, lines 182–304) to process the client in a separate thread. These threads enable the clients to play the game independently. The first client to connect to the server is player X and the second is player O. Player X makes the first move. The server maintains the information about the board so it can determine if a player’s move is valid.

```java
// Fig. 27.13: TicTacToeServer.java
// Server side of client/server Tic-Tac-Toe program.
import java.awt.BorderLayout;
import java.net.ServerSocket;
import java.net.Socket;
import java.io.IOException;
import java.util.Formatter;
import java.util.Scanner;
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;
import java.util.concurrent.locks.Lock;
import java.util.concurrent.locks.ReentrantLock;
import java.util.concurrent.locks.Condition;
import javax.swing.JFrame;
import javax.swing.JTextArea;
import javax.swing.SwingUtilities;

public class TicTacToeServer extends JFrame
{
    private String[] board = new String[ 9 ]; // tic-tac-toe board
    private JTextArea outputArea; // for outputting moves
    private Player[] players; // array of Players
    private ServerSocket server; // server socket to connect with clients
    private int currentPlayer; // keeps track of player with current move
    private final static int PLAYER_X = 0; // constant for first player
    private final static int PLAYER_O = 1; // constant for second player
    private final static String[] MARKS = { "X", "O" }; // array of marks
    private ExecutorService runGame; // will run players
    private Lock gameLock; // to lock game for synchronization
    private Condition otherPlayerConnected; // to wait for other player
    private Condition otherPlayerTurn; // to wait for other player's turn

    // set up tic-tac-toe server and GUI that displays messages
    public TicTacToeServer()
    {
        super( "Tic-Tac-Toe Server" ); // set title of window

        // create ExecutorService with a thread for each player
        runGame = Executors.newFixedThreadPool( 2 );
        gameLock = new ReentrantLock(); // create lock for game

        // condition variable for both players being connected
        otherPlayerConnected = gameLock.newCondition();

        // condition variable for the other player's turn
        otherPlayerTurn = gameLock.newCondition();

        for ( int i = 0; i < 9; i++ )
            board[ i ] = new String( "" ); // create tic-tac-toe board
        players = new Player[ 2 ]; // create array of players
        currentPlayer = PLAYER_X; // set current player to first player

        try
        {
            server = new ServerSocket( 12345, 2 ); // set up ServerSocket
        } // end try
        catch ( IOException ioException )
        {
            ioException.printStackTrace();
            System.exit( 1 );
        } // end catch

        outputArea = new JTextArea(); // create JTextArea for output
        add( outputArea, BorderLayout.CENTER );
        outputArea.setText( "Server awaiting connections\n" );

        setSize( 300, 300 ); // set size of window
        setVisible( true ); // show window
    } // end TicTacToeServer constructor

    // wait for two connections so game can be played
    public void execute()
    {
        // wait for each client to connect
        for ( int i = 0; i < players.length; i++ )
        {
            try // wait for connection, create Player, start runnable
            {
                players[ i ] = new Player( server.accept(), i );
                runGame.execute( players[ i ] ); // execute player runnable
            } // end try
            catch ( IOException ioException )
            {
                ioException.printStackTrace();
                System.exit( 1 );
            } // end catch
        } // end for

        gameLock.lock(); // lock game to signal player X's thread

        try
        {
            players[ PLAYER_X ].setSuspended( false ); // resume player X
            otherPlayerConnected.signal(); // wake up player X's thread
        } // end try
        finally
        {
            gameLock.unlock(); // unlock game after signalling player X
        } // end finally
    } // end method execute

    // display message in outputArea
    private void displayMessage( final String messageToDisplay )
    {
        // display message from event-dispatch thread of execution
        SwingUtilities.invokeLater(
            new Runnable()
            {
                public void run() // updates outputArea
                {
                    outputArea.append( messageToDisplay ); // add message
                } // end method run
            } // end inner class
        ); // end call to SwingUtilities.invokeLater
    } // end method displayMessage

    // determine if move is valid
    public boolean validateAndMove( int location, int player )
    {
        // while not current player, must wait for turn
        while ( player != currentPlayer )
        {
            gameLock.lock(); // lock game to wait for other player to go

            try
            {
                otherPlayerTurn.await(); // wait for player's turn
            } // end try
            catch ( InterruptedException exception )
            {
                exception.printStackTrace();
            } // end catch
            finally
            {
                gameLock.unlock(); // unlock game after waiting
            } // end finally
        } // end while

        // if location not occupied, make move
        if ( !isOccupied( location ) )
        {
            board[ location ] = MARKS[ currentPlayer ]; // set move on board
            currentPlayer = ( currentPlayer + 1 ) % 2; // change player

            // let new current player know that move occurred
            players[ currentPlayer ].otherPlayerMoved( location );

            gameLock.lock(); // lock game to signal other player to go

            try
            {
                otherPlayerTurn.signal(); // signal other player to continue
            } // end try
            finally
            {
                gameLock.unlock(); // unlock game after signaling
            } // end finally

            return true; // notify player that move was valid
        } // end if
        else // move was not valid
            return false; // notify player that move was invalid
    } // end method validateAndMove

    // determine whether location is occupied
    public boolean isOccupied( int location )
    {
```

**Fig. 27.13** | Server side of client/server Tic-Tac-Toe program. (Part 1 of 7.)
