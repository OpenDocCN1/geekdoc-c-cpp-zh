
```cpp
cashDispensed = true; // cash was dispensed

// instruct user to take cash
screen.displayMessageLine(
    "\nPlease take your cash from the cash dispenser.");
} // end if
else // cash dispenser does not have enough cash
screen.displayMessageLine(
    "\n\nInsufficient cash available in the ATM."
    "\n\nPlease choose a smaller amount.");
} // end if
else // not enough money available in user's account
{
    screen.displayMessageLine(
        "\nInsufficient funds in your account."
        "\n\nPlease choose a smaller amount.");
} // end else
} // end if
else // user chose cancel menu option
{
    screen.displayMessageLine( "\nCancelling transaction..." );
    transactionCanceled = true; // user canceled the transaction
} // end else
} while ( !cashDispensed && !transactionCanceled ); // end do...while
} // end function execution

// display a menu of withdrawal amounts and the option to cancel;
// return the chosen amount or 0 if the user chooses to cancel
int Withdrawal::displayMenuOfAmounts() const
{
    int userChoice = 0; // local variable to store return value

    Screen &screen = getScreen(); // get screen reference

    // array of amounts to correspond to menu numbers
    int amounts[] = { 0, 20, 40, 60, 100, 200 };

    // loop while no valid choice has been made
    while ( userChoice == 0 )
    {
        // display the menu
        screen.displayMessageLine( "\nWithdrawal options:" );
        screen.displayMessageLine( "1 - $20" );
        screen.displayMessageLine( "2 - $40" );
        screen.displayMessageLine( "3 - $60" );
        screen.displayMessageLine( "4 - $100" );
        screen.displayMessageLine( "5 - $200" );
        screen.displayMessageLine( "6 - Cancel transaction" );
        screen.displayMessage( "\nChoose a withdrawal option (1-6): " );

        int input = keypad.getInput(); // get user input through keypad

        // determine how to proceed based on the input value
        switch ( input )
        {
            case 1: // if the user chose a withdrawal amount
            case 2: // (i.e., chose option 1, 2, 3, 4 or 5), return the
            case 3: // corresponding amount from amounts array
            case 4:
            case 5:
                userChoice = amounts[ input ]; // save user's choice
                break;
            case CANCELED: // the user chose to cancel
                userChoice = CANCELED; // save user's choice
                break;
            default: // the user did not enter a value from 1-6
                screen.displayMessageLine(
                    "\nInvalid selection. Try again. ");
        } // end switch
    } // end while

    return userChoice; // return withdrawal amount or CANCELED
} // end function displayMenuOfAmounts
```

Fig. 26.33 | Withdrawal class member-function definitions. (Part 3 of 4.)

Fig. 26.33 | Withdrawal class member-function definitions. (Part 4 of 4.)

Class Withdrawal’s constructor (defined in lines 13–20 of Fig. 26.33) has five parameters. It uses a base-class initializer in line 16 to pass parameters userAccountNumber, atmScreen and atmBankDatabase to base class Transaction’s constructor to set the data members that Withdrawal inherits from Transaction. The constructor also takes references atmKeypad and atmCashDispenser as parameters and assigns them to reference data members keypad and cashDispenser using member initializers (line 17).

Class Withdrawal overrides Transaction’s pure virtual function execute with a concrete implementation (lines 23–81) that performs the steps involved in a withdrawal. Line 25 declares and initializes a local bool variable cashDispensed. This variable indicates whether cash has been dispensed (i.e., whether the transaction has completed successfully) and is initially false. Line 26 declares and initializes to false a bool variable transactionCanceled that indicates whether the transaction has been canceled by the user. Lines 29–30 get references to the bank database and the ATM’s screen by invoking member functions inherited from base class Transaction.

Lines 33–80 contain a do...while statement that executes its body until cash is dispensed (i.e., until cashDispensed becomes true) or until the user chooses to cancel (i.e., until transactionCanceled becomes true). This loop continuously returns the user to the start of the transaction if an error occurs (i.e., the requested withdrawal amount is greater than the user’s available balance or greater than the amount of cash in the cash dispenser). Line 36 displays a menu of withdrawal amounts and obtains a user selection by calling private utility function displayMenuOfAmounts (defined in lines 85–129). This function displays the menu of amounts and returns either an int withdrawal amount or the int constant CANCELED to indicate that the user has chosen to cancel the transaction.

Member function displayMenuOfAmounts (lines 85–129) first declares local variable userChoice (initially 0) to store the value that the member function will return (in line 87).

## 26.4.1.1 Class Deposit

Class Deposit (Figs. 26.34–26.35) derives from Transaction and represents a deposit ATM transaction. Figure 26.34 contains the Deposit class definition. Like derived classes BalanceInquiry and Withdrawal, Deposit declares a constructor (line 13) and member function execute (line 14)—we discuss these momentarily. Recall from the class diagram of Fig. 26.11 that class Deposit has one attribute amount, which line 16 implements as an int data member. Lines 17–18 create reference data members keypad and depositSlot that implement the associations between class Deposit and classes Keypad and DepositSlot modeled in Fig. 26.10. Line 19 contains the function prototype for a private utility function promptForDepositAmount that we’ll discuss shortly.

```cpp
// Deposit.h
// Deposit class definition. Represents a deposit transaction.
#ifndef DEPOSIT_H
#define DEPOSIT_H

#include "Transaction.h" // Transaction class definition
class Keypad; // forward declaration of class Keypad
class DepositSlot; // forward declaration of class DepositSlot

class Deposit : public Transaction
{
public:
    Deposit( int, Screen &, BankDatabase &, Keypad &, DepositSlot & );
    virtual void execute(); // perform the transaction
private:
    double amount; // amount to deposit
    Keypad &keypad; // reference to ATM's keypad
    DepositSlot &depositSlot; // reference to ATM's deposit slot
    double promptForDepositAmount() const; // get deposit amount from user
}; // end class Deposit

#endif // DEPOSIT_H
```

Fig. 26.34  |  Deposit class definition.

### Deposit Class Member-Function Definitions

Figure 26.35 presents the Deposit class implementation. Line 3 #includes the Deposit class definition, and lines 4–7 #include the class definitions of the other classes used in Deposit's member functions. Line 9 declares a constant CANCELED that corresponds to the value a user enters to cancel a deposit. We’ll now discuss how the class uses this constant.

```cpp
// Deposit.cpp
// Member-function definitions for class Deposit.
#include "Deposit.h" // Deposit class definition
#include "Screen.h" // Screen class definition
#include "BankDatabase.h" // BankDatabase class definition
#include "Keypad.h" // Keypad class definition
#include "DepositSlot.h" // DepositSlot class definition

static const int CANCELED = 0; // constant representing cancel option

// Deposit constructor initializes class's data members
Deposit::Deposit( int userAccountNumber, Screen &atmScreen,
   BankDatabase &atmBankDatabase, Keypad &atmKeypad,
   DepositSlot &atmDepositSlot )
   : Transaction( userAccountNumber, atmScreen, atmBankDatabase ),
     keypad( atmKeypad ), depositSlot( atmDepositSlot )
{
   // empty body
} // end Deposit constructor

// performs transaction; overrides Transaction's pure virtual function
void Deposit::execute()
{
   BankDatabase &bankDatabase = getBankDatabase(); // get reference
   Screen &screen = getScreen(); // get reference

   amount = promptForDepositAmount(); // get deposit amount from user

   // check whether user entered a deposit amount or canceled
   if ( amount != CANCELED )
   {
      // request deposit envelope containing specified amount
      screen.displayMessage(
         "\nPlease insert a deposit envelope containing " );
      screen.displayDollarAmount( amount );
      screen.displayMessageLine( " in the deposit slot." );

      // receive deposit envelope
      bool envelopeReceived = depositSlot.isEnvelopeReceived();

      // check whether deposit envelope was received
      if ( envelopeReceived )
      {
         screen.displayMessageLine( "\nYour envelope has been received."
            "\nNOTE: The money deposited will not be available until we"
            "\nverify the amount of any enclosed cash, and any enclosed"
            "\nchecks clear." );

         // credit account to reflect the deposit
         bankDatabase.credit( getAccountNumber(), amount );
      } // end if
      else // deposit envelope not received
      {
         screen.displayMessageLine( "\nYou did not insert an "
            "envelope, so the ATM has canceled your transaction." );
      } // end else
   } // end if
   else // user canceled instead of entering amount
   {
```

Fig. 26.35 | Deposit class member-function definitions. (Part 1 of 3.)

Fig. 26.35 | Deposit class member-function definitions. (Part 2 of 3.)
