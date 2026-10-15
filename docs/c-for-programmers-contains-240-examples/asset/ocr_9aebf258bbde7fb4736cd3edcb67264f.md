```
13 public:
14     // operations
15     void execute(); // perform the transaction
16 private:
17     // attributes
18     int accountNumber; // account to withdraw funds from
19     double amount; // amount to withdraw
20 
21     // references to associated objects
22     Screen &screen; // reference to ATM's screen
23     Keypad &keypad; // reference to ATM's keypad
24     CashDispenser &cashDispenser; // reference to ATM's cash dispenser
25     BankDatabase &bankDatabase; // reference to the account info database
26 }; // end class Withdrawal
27 
28 #endif // WITHDRAWAL_H
```

Fig. 9.26 | Adding operations to the Withdrawal class header file. (Part 2 of 2.)

# Software Engineering Observation 9.11

> Several UML modeling tools can convert UML-based designs into C++ code, considerably speeding the implementation process. For more information on these “automatic” code generators, refer to the Internet and web resources listed at the end of Section 2.7.

This concludes our discussion of the basics of generating class header files from UML diagrams. In Section 13.10, we demonstrate how to modify the header files to incorporate the object-oriented concept of inheritance.

# Software Engineering Case Study Self-Review Exercises

+   9.1 State whether the following statement is true or false, and if false, explain why: If an attribute of a class is marked with a minus sign (-) in a class diagram, the attribute is not directly accessible outside of the class.
+   9.2 In Fig. 9.21, the association between the ATM and the Screen indicates that:
+   a) we can navigate from the Screen to the ATM
+   b) we can navigate from the ATM to the Screen
+   c) Both a and b; the association is bidirectional
+   d) None of the above
+   9.3 Write C++ code to begin implementing the design for class Account.

# Answers to Software Engineering Case Study Self-Review Exercises

+   9.1 True. The minus sign (-) indicates private visibility. We’ve mentioned “friendship” as an exception to private visibility. Friendship is discussed in Chapter 10.
+   9.2 b.
+   9.3 The design for class Account yields the header file in Fig. 9.27.

```
1 // Fig. 9.27: Account.h
2 // Account class definition. Represents a bank account.
```

Fig. 9.27 | Account class header file based on Fig. 9.20 and Fig. 9.21. (Part 1 of 2.)