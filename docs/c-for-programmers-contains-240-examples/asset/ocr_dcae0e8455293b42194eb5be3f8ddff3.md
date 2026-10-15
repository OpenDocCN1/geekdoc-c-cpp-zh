```
// Fig. 13.30: Withdrawal.h
// Definition of class Withdrawal that represents a withdrawal transaction
#ifndef WITHDRAWAL_H
#define WITHDRAWAL_H

#include "Transaction.h" // Transaction class definition

// class Withdrawal derives from base class Transaction
class Withdrawal : public Transaction
{
}; // end class Withdrawal

#endif // WITHDRAWAL_H
```

Fig. 13.30 | Withdrawal class definition that derives from Transaction.

```
// Fig. 13.31: Withdrawal.h
// Definition of class Withdrawal that represents a withdrawal transaction
#ifndef WITHDRAWAL_H
#define WITHDRAWAL_H

#include "Transaction.h" // Transaction class definition

class Keypad; // forward declaration of class Keypad
class CashDispenser; // forward declaration of class CashDispenser

// class Withdrawal derives from base class Transaction
class Withdrawal : public Transaction
{
public:
    // member function overriding execute in base class Transaction
    virtual void execute(); // perform the transaction
private:
    // attributes
    double amount; // amount to withdraw
    Keypad &keypad; // reference to ATM's keypad
    CashDispenser &cashDispenser; // reference to ATM's cash dispenser
}; // end class Withdrawal

#endif // WITHDRAWAL_H
```

Fig. 13.31 | Withdrawal class header file based on Fig. 13.28 and Fig. 13.29.

# ATM Case Study Wrap-Up

This concludes our object-oriented design of the ATM system. A complete C++ implementation of the ATM system in 877 lines of code appears in Appendix E. This working implementation uses key programming notions, including classes, objects, encapsulation, visibility, composition, inheritance and polymorphism. The code is abundantly commented and conforms to the coding practices you’ve learned. Mastering this code is a wonderful capstone experience for you after studying Chapters 1–13.