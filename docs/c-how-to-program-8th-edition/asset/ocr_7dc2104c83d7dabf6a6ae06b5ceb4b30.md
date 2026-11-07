the user enters a deposit amount, lines 33–36 instruct the user to insert a deposit envelope with the correct amount. Recall that Screen member function `displayDollarAmount` outputs a double formatted as a dollar amount.

Line 39 sets a local bool variable to the value returned by `depositSlot`’s `isEnvelopeReceived` member function, indicating whether a deposit envelope has been received. Recall that we coded `isEnvelopeReceived` (lines 7–10 of Fig. 26.23) to always return true, because we are simulating the functionality of the deposit slot and assume that the user always inserts an envelope. However, we code the member function execute of class Deposit to test for the possibility that the user does not insert an envelope—good software engineering demands that programs account for all possible return values. Thus, class Deposit is prepared for future versions of `isEnvelopeReceived` that could return false. Lines 44–50 execute if the deposit slot receives an envelope. Lines 44–47 display an appropriate message to the user. Line 50 then credits the deposit amount to the user’s account in the database. Lines 54–55 will execute if the deposit slot does not receive a deposit envelope. In this case, we display a message to the user stating that the ATM has canceled the transaction. The member function then returns without modifying the user’s account.

# 26.4.12 Test Program ATMCaseStudy.cpp

ATMCaseStudy.cpp (Fig. 26.36) is a simple C++ program that allows us to start, or “turn on,” the ATM and test the implementation of our ATM system model. The program’s main function (lines 6–11) does nothing more than instantiate a new ATM object named atm (line 8) and invoke its run member function (line 9) to start the ATM.

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
} // end main
```
```

Fig. 26.36 | ATMCaseStudy.cpp starts the ATM system.

# 26.5 Wrap-Up

In this chapter, you used inheritance to tune the design of the ATM software system, and you fully implemented the ATM in C++. Congratulations on completing the entire ATM case study! We hope you found this experience to be valuable and that it reinforced many of the object-oriented programming concepts that you’ve learned.

# Answers to Self-Review Exercises

**26.1** True. The minus sign (−) indicates private visibility. We’ve mentioned “friendship” as an exception to private visibility. Friendship is discussed in Chapter 10.