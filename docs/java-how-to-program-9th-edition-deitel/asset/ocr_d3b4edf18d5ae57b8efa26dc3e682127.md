```
53          // credit account to reflect the deposit
54          bankDatabase.credit( getAccountNumber(), amount );
55      } // end if
56      else // deposit envelope not received
57      {
58          screen.displayMessageLine( "\nYou did not insert an " +
59              "envelope, so the ATM has canceled your transaction." );
60      } // end else
61      } // end if
62      else // user canceled instead of entering amount
63      {
64          screen.displayMessageLine( "\nCanceling transaction..." );
65      } // end else
66  } // end method execute
67
68  // prompt user to enter a deposit amount in cents
69  private double promptForDepositAmount()
70  {
71      Screen screen = getScreen(); // get reference to screen
72
73      // display the prompt
74      screen.displayMessage( "\nPlease enter a deposit amount in " +
75          "CENTS (or 0 to cancel): " );
76      int input = keypad.getInput(); // receive input of deposit amount
77
78      // check whether the user canceled or entered a valid amount
79      if ( input == CANCELED )
80          return CANCELED;
81      else
82      {
83          return ( double ) input / 100; // return dollar amount
84      } // end else
85  } // end method promptForDepositAmount
86 } // end class Deposit
```

# Fig. 13.23 | Class Deposit represents a deposit ATM transaction. (Part 2 of 2.)

Like Withdrawal, class Deposit contains a constructor (lines 12–22) that passes three parameters to superclass Transaction’s constructor. The constructor also has parameters atmKeypad and atmDepositSlot, which it assigns to corresponding attributes (lines 20–21).

Method execute (lines 25–66) overrides the abstract version in superclass Transaction with a concrete implementation that performs the steps required in a deposit transaction. Lines 28–29 get references to the database and the screen. Line 31 prompts the user to enter a deposit amount by invoking private utility method promptForDepositAmount (declared in lines 69–85) and sets attribute amount to the value returned. Method promptForDepositAmount asks the user to enter a deposit amount as an integer number of cents (because the ATM’s keypad does not contain a decimal point; this is consistent with many real ATMs) and returns the double value representing the dollar amount to be deposited.

Line 71 in method promptForDepositAmount gets a reference to the ATM’s screen. Lines 74–75 display a message asking the user to input a deposit amount as a number of cents or “0” to cancel the transaction. Line 76 receives the user’s input from the keypad. Lines 79–84 determine whether the user has entered a real deposit amount or chosen to