```
```java
109    // determine how to proceed based on the input value
110    switch ( input )
111    {
112        case 1: // if the user chose a withdrawal amount
113        case 2: // (i.e., chose option 1, 2, 3, 4 or 5), return the
114        case 3: // corresponding amount from amounts array
115        case 4:
116        case 5:
117            userChoice = amounts[ input ]; // save user's choice
118            break;
119        case CANCELED: // the user chose to cancel
120            userChoice = CANCELED; // save user's choice
121            break;
122        default: // the user did not enter a value from 1-6
123            screen.displayMessageLine(
124                "\nInvalid selection. Try again. ");
125    } // end switch
126} // end while

128 return userChoice; // return withdrawal amount or CANCELED
129} // end function displayMenuOfAmounts
```
```

**Fig. 26.33** | Withdrawal class member-function definitions. (Part 4 of 4.)

Class Withdrawal’s constructor (defined in lines 13–20 of Fig. 26.33) has five parameters. It uses a base-class initializer in line 16 to pass parameters userAccountNumber, atmScreen and atmBankDatabase to base class Transaction’s constructor to set the data members that Withdrawal inherits from Transaction. The constructor also takes references atmKeypad and atmCashDispenser as parameters and assigns them to reference data members keypad and cashDispenser using member initializers (line 17).

Class Withdrawal overrides Transaction’s pure virtual function execute with a concrete implementation (lines 23–81) that performs the steps involved in a withdrawal. Line 25 declares and initializes a local bool variable cashDispensed. This variable indicates whether cash has been dispensed (i.e., whether the transaction has completed successfully) and is initially false. Line 26 declares and initializes to false a bool variable transactionCanceled that indicates whether the transaction has been canceled by the user. Lines 29–30 get references to the bank database and the ATM’s screen by invoking member functions inherited from base class Transaction.

Lines 33–80 contain a do...while statement that executes its body until cash is dispensed (i.e., until cashDispensed becomes true) or until the user chooses to cancel (i.e., until transactionCanceled becomes true). This loop continuously returns the user to the start of the transaction if an error occurs (i.e., the requested withdrawal amount is greater than the user’s available balance or greater than the amount of cash in the cash dispenser). Line 36 displays a menu of withdrawal amounts and obtains a user selection by calling private utility function displayMenuOfAmounts (defined in lines 85–129). This function displays the menu of amounts and returns either an int withdrawal amount or the int constant CANCELED to indicate that the user has chosen to cancel the transaction.

Member function displayMenuOfAmounts (lines 85–129) first declares local variable userChoice (initially 0) to store the value that the member function will return (in line 87).