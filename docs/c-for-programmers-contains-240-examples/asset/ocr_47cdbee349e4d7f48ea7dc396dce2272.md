# Software Engineering Case Study Self-Review Exercises

13.1 The UML uses an arrow with a ________ to indicate a generalization relationship.

+   a) solid filled arrowhead
+   b) triangular hollow arrowhead
+   c) diamond-shaped hollow arrowhead
+   d) stick arrowhead

13.2 State whether the following statement is true or false, and if false, explain why: The UML requires that we underline abstract class names and operation names.

13.3 Write a C++ header file to begin implementing the design for class Transaction specified in Fig. 13.28 and Fig. 13.29. Be sure to include private references based on class Transaction’s associations. Also be sure to include public get functions for any of the private data members that the derived classes must access to perform their tasks.

# Answers to Software Engineering Case Study Self-Review Exercises

13.1 b.

13.2 False. The UML requires that we italicize abstract class names and operation names.

13.3 The design for class Transaction yields the header file in Fig. 13.32. In the implementation in Appendix E, a constructor initializes private reference attributes screen and bankDatabase to actual objects, and member functions getScreen and getBankDatabase access these attributes. These member functions allow classes derived from Transaction to access the ATM’s screen and interact with the bank’s database.

```
// Fig. 13.32: Transaction.h
// Transaction abstract base class definition.
#ifndef TRANSACTION_H
#define TRANSACTION_H

class Screen; // forward declaration of class Screen
class BankDatabase; // forward declaration of class BankDatabase

class Transaction
{
public:
    int getAccountNumber(); // return account number
    Screen &getScreen(); // return reference to screen
    BankDatabase &getBankDatabase(); // return reference to bank database

    // pure virtual function to perform the transaction
    virtual void execute() = 0; // overridden in derived classes
private:
    int accountNumber; // indicates account involved
    Screen &screen; // reference to the screen of the ATM
    BankDatabase &bankDatabase; // reference to the account info database
}; // end class Transaction

#endif // TRANSACTION_H
```

Fig. 13.32 | Transaction class header file based on Fig. 13.28 and Fig. 13.29.