```
boolean userExited = false; // user has not chosen to exit

// loop while user has not chosen option to exit system
while ( !userExited )
{
    // show main menu and get user selection
    int mainMenuSelection = displayMainMenu();

    // decide how to proceed based on user's menu selection
    switch ( mainMenuSelection )
    {
        // user chose to perform one of three transaction types
        case BALANCE_INQUIRY:
        case WITHDRAWAL:
        case DEPOSIT:

            // initialize as new object of chosen type
            currentTransaction =
                createTransaction( mainMenuSelection );

            currentTransaction.execute(); // execute transaction
            break;
        case EXIT: // user chose to terminate session
            screen.displayMessageLine( "\nExiting the system..." );
            userExited = true; // this ATM session should end
            break;
        default: // user did not enter an integer from 1-4
            screen.displayMessageLine(
                "\nYou did not enter a valid selection. Try again." );
            break;
    } // end switch
} // end while
} // end method performTransactions

// display the main menu and return an input selection
private int displayMainMenu()
{
    screen.displayMessageLine( "\nMain menu:" );
    screen.displayMessageLine( "1 - View my balance" );
    screen.displayMessageLine( "2 - Withdraw cash" );
    screen.displayMessageLine( "3 - Deposit funds" );
    screen.displayMessageLine( "4 - Exit\n" );
    screen.displayMessage( "Enter a choice: " );
    return keypad.getInput(); // return user's selection
} // end method displayMainMenu

// return object of specified Transaction subclass
private Transaction createTransaction( int type )
{
    Transaction temp = null; // temporary Transaction variable
```