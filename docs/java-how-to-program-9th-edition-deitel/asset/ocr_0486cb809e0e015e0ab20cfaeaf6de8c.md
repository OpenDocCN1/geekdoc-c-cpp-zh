```
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
```