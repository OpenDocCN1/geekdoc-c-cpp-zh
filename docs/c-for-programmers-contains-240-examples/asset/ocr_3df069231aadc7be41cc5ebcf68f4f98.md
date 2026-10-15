dividing by 100. For example, if the user enters 125 as the number of cents, line 79 returns 125.0 divided by 100, or 1.25—125 cents is $1.25.

The if statement in lines 30–61 in member function execute determines whether the user has chosen to cancel the transaction instead of entering a deposit amount. If the user cancels, line 60 displays an appropriate message, and the member function returns. If the user enters a deposit amount, lines 33–36 instruct the user to insert a deposit envelope with the correct amount. Recall that Screen member function displayDollarAmount outputs a double formatted as a dollar amount.

Line 39 sets a local bool variable to the value returned by depositSlot’s isEnvelopeReceived member function, indicating whether a deposit envelope has been received. Recall that we coded isEnvelopeReceived (lines 7–10 of Fig. E.10) to always return true, because we are simulating the functionality of the deposit slot and assume that the user always inserts an envelope. However, we code member function execute of class Deposit to test for the possibility that the user does not insert an envelope—good software engineering demands that programs account for all possible return values. Thus, class Deposit is prepared for future versions of isEnvelopeReceived that could return false. Lines 44–50 execute if the deposit slot receives an envelope. Lines 44–47 display an appropriate message to the user. Line 50 then credits the deposit amount to the user’s account in the database. Lines 54–55 will execute if the deposit slot does not receive a deposit envelope. In this case, we display a message to the user stating that the ATM has canceled the transaction. The member function then returns without modifying the user’s account.

# E.13 Test Program ATMCaseStudy.cpp

ATMCaseStudy.cpp (Fig. E.23) is a simple C++ program that allows us to start, or “turn on,” the ATM and test the implementation of our ATM system model. The program’s main function (lines 6–11) does nothing more than instantiate a new ATM object named atm (line 8) and invoke its run member function (line 9) to start the ATM.

```
```cpp
// ATMCaseStudy.cpp
// Driver program for the ATM case study.
#include "ATM.h" // ATM class definition

// main function creates and runs the ATM
int main()
{
    ATM atm; // create an ATM object
    atm.run(); // tell the ATM to start
    return 0;
} // end main
```
```

**Fig. E.23** | ATMCaseStudy.cpp starts the ATM system.

# E.14 Wrap-Up

Congratulations on completing the entire Software Engineering ATM Case Study! We hope you found this experience to be valuable and that it reinforced many of the concepts that you learned in Chapters 1–13. We would sincerely appreciate your comments, criticisms and suggestions. You can reach us at deitel@deitel.com. We’ll respond promptly.