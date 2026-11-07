
## Creating a Transaction

Member function `createTransaction` (lines 118–140) uses a `switch` statement (lines 123–137) to instantiate a new `Transaction` derived class object of the type indicated by the parameter type. Recall that member function `performTransactions` passes `mainMenuSelection` to this member function only when `mainMenuSelection` contains a value corresponding to one of the three transaction types. Therefore the type equals either `BALANCE_INQUIRY`, `WITHDRAWAL` or `DEPOSIT`. Each case in the `switch` statement aims the temporary pointer `tempPtr` at a newly created object of the appropriate `Transaction` derived class. Each constructor has a unique parameter list, based on the specific data required to initialize the derived class object. A `BalanceInquiry` requires only the account number of the current user and references to the ATM’s screen and the `bankDatabase`. In addition to these parameters, a `Withdrawal` requires references to the ATM’s keypad and `cashDispenser`, and a `Deposit` requires references to the ATM’s keypad and `depositSlot`. As you’ll soon see, the `BalanceInquiry`, `Withdrawal` and `Deposit` constructors each specify reference parameters to receive the objects representing the required parts of the ATM. Thus, when member function `createTransaction` passes objects in the ATM (e.g., screen and keypad) to the initializer for each newly created `Transaction` derived class object, the new object actually receives references to the ATM’s composite objects. We discuss the transaction classes in more detail in Sections 26.4.8–26.4.11.

## Exiting the Main Menu and Processing Invalid Selections

After executing a transaction (line 87 in `performTransactions`), `userExited` remains `false` and the `while` loop in lines 71–102 repeats, returning the user to the main menu. However, if a user does not perform a transaction and instead selects the main menu option to exit, line 95 sets `userExited` to `true`, causing the condition of the `while` loop (`!userExited`) to become `false`. This while is the final statement of member function `performTransactions`, so control returns to the calling function `run`. If the user enters an invalid main menu selection (i.e., not an integer from 1–4), lines 98–99 display an appropriate error message, `userExited` remains `false` and the user returns to the main menu to try again.

## Awaiting the Next ATM User

When `performTransactions` returns control to member function `run`, the user has chosen to exit the system, so lines 34–35 reset the ATM’s data members `userAuthenticated` and `currentAccountNumber` to prepare for the next ATM user. Line 36 displays a goodbye message before the ATM starts over and welcomes the next user.

## 26.4.2 Class Screen

Class Screen (Figs. 26.16–26.17) represents the screen of the ATM and encapsulates all aspects of displaying output to the user. Class Screen approximates a real ATM’s screen with a computer monitor and outputs text messages using `cout` and the stream insertion operator (`<<`). In this case study, we designed class Screen to have one operation—`displayMessage`. For greater flexibility in displaying messages to the Screen, we now declare three Screen member functions—`displayMessage`, `displayMessageLine` and `displayDollarAmount`. The prototypes for these member functions appear in lines 12–14 of Fig. 26.16.

```cpp
// Screen.h
// Screen class definition. Represents the screen of the ATM.
#ifndef SCREEN_H
#define SCREEN_H

#include <string>
using namespace std;

class Screen
{
public:
    void displayMessage( string ) const; // output a message
    void displayMessageLine( string ) const; // output message with newline
    void displayDollarAmount( double ) const; // output a dollar amount
}; // end class Screen

#endif // SCREEN_H
```

Fig. 26.16 | Screen class definition.

```cpp
// Screen.cpp
// Member-function definitions for class Screen.
#include <iostream>
#include <iomanip>
#include "Screen.h" // Screen class definition
using namespace std;

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
```

Fig. 26.17 | Screen class member-function definitions.

### Screen Class Member-Function Definitions

Figure 26.17 contains the member-function definitions for class Screen. Line 5 `#include`s the Screen class definition. Member function `displayMessage` (lines 9–12) takes a string as an argument and prints it to the console using `cout` and the stream insertion operator (`<<`). The cursor stays on the same line, making this member function appropriate for dis-

```cpp
using namespace std;
#include "Keypad.h" // Keypad class definition

// return an integer value entered by user
int Keypad::getInput() const
{
    int input; // variable to store the input
    cin >> input; // we assume that user enters an integer
    return input; // return the value entered by user
} // end function getInput
```

Fig. 26.19 | Keypad class member-function definition. (Part 2 of 2.)

## 26.6.4 Class CashDispenser

Class CashDispenser (Figs. 26.20–26.21) represents the cash dispenser. Figure 26.20 contains the function prototype for a default constructor (line 9). Class CashDispenser declares two additional public member functions—`dispenseCash` (line 12) and `isSufficientCashAvailable` (line 15). The class trusts that a client (i.e., withdrawal) calls `dispenseCash` only after establishing that sufficient cash is available by calling `isSufficientCashAvailable`. Thus, `dispenseCash` simply simulates dispensing the requested amount without checking whether sufficient cash is available. Line 17 declares private constant `INITIAL_COUNT`, which indicates the initial count of bills in the cash dispenser when the ATM starts (i.e., 500). Line 18 implements attribute `count` (modeled in Fig. 26.11), which keeps track of the number of bills remaining in the `CashDispenser` at any time.

```cpp
// CashDispenser.h
// CashDispenser class definition. Represents the ATM's cash dispenser.
#ifndef CASH_DISPENSER_H
#define CASH_DISPENSER_H

class CashDispenser
{
public:
    CashDispenser(); // constructor initializes bill count to 500

    // simulates dispensing of specified amount of cash
    void dispenseCash( int );

    // indicates whether cash dispenser can dispense desired amount
    bool isSufficientCashAvailable( int ) const;
private:
    static const int INITIAL_COUNT = 500;
    int count; // number of $20 bills remaining
}; // end class CashDispenser

#endif // CASH_DISPENSER_H
```

Fig. 26.20 | CashDispenser class definition.

### CashDispenser Class Member-Function Definitions

Figure 26.21 contains the definitions of class CashDispenser’s member functions. The constructor (lines 6–9) sets `count` to the initial count (i.e., 500). Member function `dispenseCash` (lines 13–17) simulates cash dispensing. If our system were hooked up to a real hardware cash dispenser, this member function would interact with the hardware device to physically dispense cash. Our simulated version of the member function simply decreases the count of bills remaining by the number required to dispense the specified amount (line 16). Line 15 calculates the number of $20 bills required to dispense the specified amount. The ATM allows the user to choose only withdrawal amounts that are multiples of $20, so we divide `amount` by 20 to obtain the number of `billsRequired`. Also, it’s the responsibility of the class’s client (i.e., withdrawal) to inform the user that cash has been dispensed—`CashDispenser` cannot interact directly with `Screen`.

```cpp
// CashDispenser.cpp
// Member-function definitions for class CashDispenser.
#include "CashDispenser.h" // CashDispenser class definition

// CashDispenser default constructor initializes count to default
CashDispenser::CashDispenser()
{
    count = INITIAL_COUNT; // set count attribute to default
} // end CashDispenser default constructor

// simulates dispensing of specified amount of cash; assumes enough cash
// is available (previous call to isSufficientCashAvailable returned true)
void CashDispenser::dispenseCash( int amount )
{
    int billsRequired = amount / 20; // number of $20 bills required
    count -= billsRequired; // update the count of bills
} // end function dispenseCash

// indicates whether cash dispenser can dispense desired amount
bool CashDispenser::isSufficientCashAvailable( int amount ) const
{
    int billsRequired = amount / 20; // number of $20 bills required

    if ( count >= billsRequired )
        return true; // enough bills are available
    else
        return false; // not enough bills are available
} // end function isSufficientCashAvailable
```

**Fig. 26.21** | *CashDispenser class member-function definitions.*

Member function `isSufficientCashAvailable` (lines 20–28) has a parameter `amount` that specifies the amount of cash in question. Lines 24–27 return `true` if the `CashDispenser`’s `count` is greater than or equal to `billsRequired` (i.e., enough bills are available) and `false` otherwise (i.e., not enough bills). For example, if a user wishes to withdraw $80 (i.e., `billsRequired` is 4), but only three bills remain (i.e., `count` is 3), the member function returns `false`.
