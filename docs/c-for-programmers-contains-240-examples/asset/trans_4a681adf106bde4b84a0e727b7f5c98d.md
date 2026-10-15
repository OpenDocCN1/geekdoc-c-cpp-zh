

#include <iomanip>
using std::setprecision;

#include "Screen.h" // Screen class definition

// output a message without a newline
void Screen::displayMessage( string message ) const
{
    cout << message;
} // end function displayMessage

// output a message with a newline
void Screen::displayMessageLine( string message ) const
{
    cout << message << endl;
} // end function displayMessageLine

// output a dollar amount
void Screen::displayDollarAmount( double amount ) const
{
    cout << fixed << setprecision( 2 ) << "$" << amount;
} // end function displayDollarAmount

Fig. E.4 | Screen class member-function definitions. (Part 2 of 2.)

## E.4 Class Keypad

Class Keypad (Figs. E.5–E.6) represents the keypad of the ATM and is responsible for receiving all user input. Recall that we are simulating this hardware, so we use the computer’s keyboard to approximate the keypad. A computer keyboard contains many keys not found on the ATM’s keypad. However, we assume that the user presses only the keys on the computer keyboard that also appear on the keypad—the keys numbered 0–9 and the Enter key. Line 9 of Fig. E.5 contains the function prototype for class Keypad’s one member function getInput. This member function is declared const because it does not change the object.

```
// Keypad.h
// Keypad class definition. Represents the keypad of the ATM.
#ifndef KEYPAD_H
#define KEYPAD_H

class Keypad
{
public:
    int getInput() const; // return an integer value entered by user
}; // end class Keypad

#endif // KEYPAD_H
```

Fig. E.5 | Keypad class definition.

### Keypad Class Member-Function Definition

In the Keypad implementation file (Fig. E.6), member function getInput (defined in lines 9–14) uses the standard input stream cin and the stream extraction operator (>>) to obtain input from the user. Line 11 declares a local variable to store the user’s input. Line 12 reads input into local variable input, then line 13 returns this value. Recall that getInput obtains all the input used by the ATM. Keypad’s getInput member function simply returns the integer input by the user. If a client of class Keypad requires input that satisfies some particular criteria (i.e., a number corresponding to a valid menu option), the client must perform the appropriate error checking. [Note: Using the standard input stream cin and the stream extraction operator (>>) allows noninteger input to be read from the user. Because the real ATM’s keypad permits only integer input, however, we assume that the user enters an integer and do not attempt to fix problems caused by noninteger input.]

```
1  // Keypad.cpp
2  // Member-function definition for class Keypad (the ATM's keypad).
3  #include <iostream>
4  using std::cin;
5
6  #include "Keypad.h" // Keypad class definition
7
8  // return an integer value entered by user
9  int Keypad::getInput() const
10 { 
11     int input; // variable to store the input
12     cin >> input; // we assume that user enters an integer
13     return input; // return the value entered by user
14 } // end function getInput
```

Fig. E.6 | Keypad class member-function definition.

## E.5 Class CashDispenser

Class CashDispenser (Figs. E.7–E.8) represents the cash dispenser of the ATM. The class definition (Fig. E.7) contains the function prototype for a default constructor (line 9). Class CashDispenser declares two additional public member functions—dispenseCash (line 12) and isSufficientCashAvailable (line 15). The class trusts that a client (i.e., Withdrawal) calls dispenseCash only after establishing that sufficient cash is available by calling isSufficientCashAvailable. Thus, dispenseCash simply simulates dispensing the requested amount without checking whether sufficient cash is available. Line 17 declares private constant INITIAL_COUNT, which indicates the initial count of bills in the cash dispenser when the ATM starts (i.e., 500). Line 18 implements attribute count (modeled in Fig. 13.29), which keeps track of the number of bills remaining in the CashDispenser at any time.

### CashDispenser Class Member-Function Definitions

Figure E.8 contains the definitions of class CashDispenser’s member functions. The constructor (lines 6–9) sets count to the initial count (i.e., 500). Member function dispenseCash (lines 13–17) simulates cash dispensing. If our system were hooked up to a real hardware cash dispenser, this member function would interact with the hardware device
to physically dispense cash. Our simulated version of the member function simply decreases the count of bills remaining by the number required to dispense the specified amount (line 16). Note that line 15 calculates the number of $20 bills required to dispense the specified amount. The ATM allows the user to choose only withdrawal amounts that are multiples of $20, so we divide amount by 20 to obtain the number of billsRequired. Also note that it is the responsibility of the client of the class (i.e., Withdrawal) to inform the user that cash has been dispensed—CashDispenser cannot interact directly with Screen.

Member function isSufficientCashAvailable (lines 20–28) has a parameter amount that specifies the amount of cash in question. Lines 24–27 return true if the CashDispenser’s count is greater than or equal to billsRequired (i.e., enough bills are available) and false otherwise (i.e., not enough bills). For example, if a user wishes to withdraw $80 (i.e., billsRequired is 4), but only three bills remain (i.e., count is 3), the member function returns false.

## E.6 Class DepositSlot

Class DepositSlot (Figs. E.9–E.10) represents the deposit slot of the ATM. Like the version of class CashDispenser presented here, this version of class DepositSlot merely simulates the functionality of a real hardware deposit slot. DepositSlot has no data members and only one member function—isEnvelopeReceived (declared in line 9 of Fig. E.9 and defined in lines 7–10 of Fig. E.10)—that indicates whether a deposit envelope was received.

```
// DepositSlot.h
// DepositSlot class definition. Represents the ATM's deposit slot.
#ifndef DEPOSIT_SLOT_H
#define DEPOSIT_SLOT_H

class DepositSlot
{
public:
    bool isEnvelopeReceived() const; // tells whether envelope was received
}; // end class DepositSlot

#endif // DEPOSIT_SLOT_H
```

Fig. E.9 | DepositSlot class definition.

```
// DepositSlot.cpp
// Member-function definition for class DepositSlot.
#include "DepositSlot.h" // DepositSlot class definiton

// indicates whether envelope was received (always returns true,
// because this is only a software simulation of a real deposit slot)
bool DepositSlot::isEnvelopeReceived() const
{
    return true; // deposit envelope was received
} // end function isEnvelopeReceived
```

Fig. E.10 | DepositSlot class member-function definition.

Recall from the requirements specification that the ATM allows the user up to two minutes to insert an envelope. The current version of member function isEnvelopeReceived simply returns true immediately (line 9 of Fig. E.10), because this is only a software simulation, and we assume that the user has inserted an envelope within the required time frame. If an actual hardware deposit slot were connected to our system, member function isEnvelopeReceived might be implemented to wait for a maximum of two minutes to receive a signal from the hardware deposit slot indicating that the user has indeed inserted a deposit envelope. If isEnvelopeReceived were to receive such a signal within two minutes, the member function would return true. If two minutes elapsed and the member function still had not received a signal, then the member function would return false.

## E.7 Class Account

Class Account (Figs. E.11–E.12) represents a bank account. Lines 9–15 in the class definition (Fig. E.11) contain function prototypes for the class’s constructor and six member functions, which we discuss shortly. Each Account has four attributes (modeled in Fig. 13.29)—accountNumber, pin, availableBalance and totalBalance. Lines 17–20 implement these attributes as private data members. Data member availableBalance represents the amount of funds available for withdrawal. Data member totalBalance represents the amount of funds available, plus the amount of deposited funds still pending confirmation or clearance.

### Account Class Member-Function Definitions

Figure E.12 presents the definitions of class Account’s member functions. The class’s constructor (lines 6–14) takes an account number, the PIN established for the account, the

```
1  // Account.h
2  // Account class definition. Represents a bank account.
3  #ifndef ACCOUNT_H
4  #define ACCOUNT_H
5
6  class Account
7  {
8  public:
9      Account( int, int, double, double ); // constructor sets attributes
10     bool validatePIN( int ) const; // is user-specified PIN correct?
11     double getAvailableBalance() const; // returns available balance
12     double getTotalBalance() const; // returns total balance
13     void credit( double ); // adds an amount to the Account balance
14     void debit( double ); // subtracts an amount from the Account balance
15     int getAccountNumber() const; // returns account number
16  private:
17     int accountNumber; // account number
18     int pin; // PIN for authentication
19     double availableBalance; // funds available for withdrawal
20     double totalBalance; // funds available + funds waiting to clear
21  }; // end class Account
22
23  #endif // ACCOUNT_H
```

Fig. E.11 | Account class definition.

