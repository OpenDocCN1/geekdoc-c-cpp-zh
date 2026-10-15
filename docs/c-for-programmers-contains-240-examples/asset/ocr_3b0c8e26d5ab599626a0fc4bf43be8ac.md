```
106
107     int input = keypad.getInput(); // get user input through keypad
108
109     // determine how to proceed based on the input value
110     switch ( input )
111     {
112         case 1: // if the user chose a withdrawal amount
113         case 2: // (i.e., chose option 1, 2, 3, 4 or 5), return the
114         case 3: // corresponding amount from amounts array
115         case 4:
116         case 5:
117             userChoice = amounts[ input ]; // save user's choice
118             break;
119         case CANCELED: // the user chose to cancel
120             userChoice = CANCELED; // save user's choice
121             break;
122         default: // the user did not enter a value from 1-6
123             screen.displayMessageLine(
124                 "\nInvalid selection. Try again.");
125     } // end switch
126 } // end while
127
128     return userChoice; // return withdrawal amount or CANCELED
129 } // end function displayMenuOfAmounts
```

Fig. E.20 | Withdrawal class member-function definitions. (Part 3 of 3.)

# Withdrawal Class Member-Function Definitions

Figure E.20 contains the member-function definitions for class Withdrawal. Line 3 #includes the class’s definition, and lines 4–7 #include the definitions of the other classes used in Withdrawal’s member functions. Line 11 declares a global constant corresponding to the cancel option on the withdrawal menu. We’ll soon discuss how the class uses this constant.

Class Withdrawal’s constructor (defined in lines 13–20 of Fig. E.20) has five parameters. It uses a base-class initializer in line 16 to pass parameters userAccountNumber, atmScreen and atmBankDatabase to base class Transaction’s constructor to set the data members that Withdrawal inherits from Transaction. The constructor also takes references atmKeypad and atmCashDispenser as parameters and assigns them to reference data members keypad and cashDispenser using member initializers (line 17).

Class Withdrawal overrides Transaction’s pure virtual function execute with a concrete implementation (lines 23–81) that performs the steps involved in a withdrawal. Line 25 declares and initializes a local bool variable cashDispensed. This variable indicates whether cash has been dispensed (i.e., whether the transaction has completed successfully) and is initially false. Line 26 declares and initializes to false a bool variable transactionCanceled that indicates whether the transaction has been canceled by the user. Lines 29–30 get references to the bank database and the ATM’s screen by invoking member functions inherited from base class Transaction.

Lines 33–80 contain a do...while statement that executes its body until cash is dispensed (i.e., until cashDispensed becomes true) or until the user chooses to cancel (i.e., until transactionCanceled becomes true). This loop continuously returns the user to the start of the transaction if an error occurs (i.e., the requested withdrawal amount is