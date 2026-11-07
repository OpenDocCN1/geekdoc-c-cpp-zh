Screen, Keypad, CashDispenser, DepositSlot and BankDatabase so that the ATM can store objects of these classes.

Lines 28–30 and 33 contain function prototypes for private utility functions that the class uses to perform its tasks. We’ll see how these functions serve the class shortly. Member function createTransaction (line 33) returns a Transaction pointer. To include the class name Transaction in this file, we must at least include a forward declaration of class Transaction (line 11). Recall that a forward declaration tells the compiler that a class exists, but that the class is defined elsewhere. A forward declaration is sufficient here, as we are using a Transaction pointer as a return type—if we were creating or returning an actual Transaction object, we would need to #include the full Transaction header file.

# ATM Class Member-Function Definitions

Figure 26.15 contains the member-function definitions for class ATM. Lines 3–7 #include the header files required by the implementation file ATM.cpp. Including the ATM header file allows the compiler to ensure that the class’s member functions are defined correctly. This also allows the member functions to use the class’s data members.

```
```cpp
 1   // ATM.cpp
 2   // Member-function definitions for class ATM.
 3   #include "ATM.h" // ATM class definition
 4   #include "Transaction.h" // Transaction class definition
 5   #include "BalanceInquiry.h" // BalanceInquiry class definition
 6   #include "Withdrawal.h" // Withdrawal class definition
 7   #include "Deposit.h" // Deposit class definition
 8
 9   // enumeration constants represent main menu options
10   enum MenuOption { BALANCE_INQUIRY = 1, WITHDRAWAL, DEPOSIT, EXIT };
11
12   // ATM default constructor initializes data members
13   ATM::ATM()
14      : userAuthenticated( false ), // user is not authenticated to start
15        currentAccountNumber( 0 ) // current account number to start
16   {
17      // empty body
18   } // end ATM default constructor
19
20   // start ATM
21   void ATM::run()
22   {
23      // welcome and authenticate user; perform transactions
24      while ( true )
25      {
26         // loop while user is not yet authenticated
27         while ( !userAuthenticated )
28         {
29            screen.displayMessageLine( "\\nWelcome!" );
30            authenticateUser(); // authenticate user
31         } // end while
32   }
```
```

Fig. 26.15  |  ATM class member-function definitions. (Part 1 of 4.)