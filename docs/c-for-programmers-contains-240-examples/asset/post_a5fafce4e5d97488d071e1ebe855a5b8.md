
greater than the user’s available balance or greater than the amount of cash in the cash dispenser). Line 36 displays a menu of withdrawal amounts and obtains a user selection by calling private utility function `displayMenuOfAmounts` (defined in lines 85–129). This function displays the menu of amounts and returns either an `int` withdrawal amount or the `int` constant `CANCELED` to indicate that the user has chosen to cancel the transaction.

Member function `displayMenuOfAmounts` (lines 85–129) first declares local variable `userChoice` (initially 0) to store the value that the member function will return (line 87). Line 89 gets a reference to the screen by calling member function `getScreen` inherited from base class `Transaction`. Line 92 declares an integer array of withdrawal amounts that correspond to the amounts displayed in the withdrawal menu. We ignore the first element in the array (index 0) because the menu has no option 0. The while statement in lines 95–126 repeats until `userChoice` takes on a value other than 0. We’ll see shortly that this occurs when the user makes a valid selection from the menu. Lines 98–105 display the withdrawal menu on the screen and prompt the user to enter a choice. Line 107 obtains integer input through the keypad. The switch statement in lines 110–125 determines how to proceed based on the user’s input. If the user selects a number between 1 and 5, line 117 sets `userChoice` to the value of the element in `amounts` at index `input`. For example, if the user enters 3 to withdraw $60, line 117 sets `userChoice` to the value of `amounts[3]` (i.e., 60). Line 118 terminates the switch. Variable `userChoice` no longer equals 0, so the while in lines 95–126 terminates and line 128 returns `userChoice`. If the user selects the cancel menu option, lines 120–121 execute, setting `userChoice` to CANCELED and causing the member function to return this value. If the user does not enter a valid menu selection, lines 123–124 display an error message and the user is returned to the withdrawal menu.

The if statement in line 39 in member function `execute` determines whether the user has selected a withdrawal amount or chosen to cancel. If the user cancels, lines 77–78 execute to display an appropriate message to the user and set `transactionCanceled` to true. This causes the loop-continuation test in line 80 to fail and control to return to the calling member function (i.e., ATM member function `performTransactions`). If the user has chosen a withdrawal amount, line 41 assigns local variable `selection` to data member `amount`. Lines 44–45 retrieve the available balance of the current user’s Account and store it in a local `double` variable `availableBalance`. Next, the if statement in line 48 determines whether the selected amount is less than or equal to the user’s available balance. If it is not, lines 70–72 display an appropriate error message. Control then continues to the end of the `do...while`, and the loop repeats because both `cashDispensed` and `transactionCanceled` are still false. If the user’s balance is high enough, the if statement in line 51 determines whether the cash dispenser has enough money to satisfy the withdrawal request by invoking the cash dispenser’s `isSufficientCashAvailable` member function. If this member function returns false, lines 64–66 display an appropriate error message and the `do...while` repeats. If sufficient cash is available, then the requirements for the withdrawal are satisfied, and line 54 debits amount from the user’s account in the database. Lines 56–57 then instruct the cash dispenser to dispense the cash to the user and set `cashDispensed` to true. Finally, lines 60–61 display a message to the user that cash has been dispensed. Because `cashDispensed` is now true, control continues after the `do...while`. No additional statements appear below the loop, so the member function returns control to class ATM.

In the function calls in lines 64–66 and lines 70–72, we divide the argument to Screen member function `displayMessageLine` into two string literals, each placed on a separate line in the program. We do so because each argument is too long to fit on a single line. C++ concatenates (i.e., combines) string literals adjacent to each other, even if they are on separate lines. For example, if you write `"Happy" "Birthday"` in a program, C++ will view these two adjacent string literals as the single string literal `"Happy Birthday"`. As a result, when lines 64–66 execute, `displayMessageLine` receives a single string as a parameter, even though the argument in the function call appears as two string literals.

## E.12 Class Deposit

Class Deposit (Figs. E.21–E.22) derives from Transaction and represents a deposit ATM transaction. Figure E.21 contains the Deposit class definition. Like derived classes `BalanceInquiry` and `Withdrawal`, Deposit declares a constructor (line 13) and member function `execute` (line 14)—we discuss these momentarily. Recall from the class diagram of Fig. 13.29 that class Deposit has one attribute `amount`, which line 16 implements as a `double` data member. Lines 17–18 create reference data members `keypad` and `depositSlot` that implement the associations between class Deposit and classes `Keypad` and `DepositSlot` modeled in Fig. 13.28. Line 19 contains the function prototype for a private utility function `promptForDepositAmount` that we’ll discuss shortly.

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

**Fig. E.21**  |  Deposit class definition.

### Deposit Class Member-Function Definitions

Figure E.22 presents the Deposit class implementation. Line 3 #includes the Deposit class definition, and lines 4–7 #include the class definitions of the other classes used in Deposit’s member functions. Line 9 declares a constant `CANCELED` that corresponds to the value a user enters to cancel a deposit. We’ll soon discuss how the class uses this constant.

```cpp
// Deposit.cpp
// Member-function definitions for class Deposit.
#include "Deposit.h" // Deposit class definition
#include "Screen.h" // Screen class definition
#include "BankDatabase.h" // BankDatabase class definition
#include "Keypad.h" // Keypad class definition
#include "DepositSlot.h" // DepositSlot class definition

const static int CANCELED = 0; // constant representing cancel option

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
                "\nverify the amount of any enclosed cash, and any enclosed "
                "checks clear." );

            // credit account to reflect the deposit
            bankDatabase.credit( getAccountNumber(), amount );
        } // end if
        else // deposit envelope not received
        {
```
