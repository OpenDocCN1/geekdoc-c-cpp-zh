
A circular #include occurs when the header file for a class A #includes the header file for a class B and vice versa. Some preprocessors are not able to resolve such #include directives, causing a compilation error. If class A, for example, uses only a reference to an object of class B, then the #include in class A’s header file can be replaced by a forward declaration of class B to prevent the circular include.

```cpp
// Fig. 26.6: Withdrawal.h
// Definition of class Withdrawal that represents a withdrawal transaction
#ifndef WITHDRAWAL_H
#define WITHDRAWAL_H

class Screen;        // forward declaration of class Screen
class Keypad;        // forward declaration of class Keypad
class CashDispenser; // forward declaration of class CashDispenser
class BankDatabase;  // forward declaration of class BankDatabase

class Withdrawal
{
private:
   // attributes
   int accountNumber; // account to withdraw funds from
   double amount;     // amount to withdraw

   // references to associated objects
   Screen &screen;             // reference to ATM’s screen
   Keypad &keypad;             // reference to ATM’s keypad
   CashDispenser &cashDispenser; // reference to ATM’s cash dispenser
   BankDatabase &bankDatabase; // reference to the account info database
}; // end class Withdrawal

#endif // WITHDRAWAL_H
```

**Fig. 26.6** | *Using forward declarations in place of #include directives.*

- 5. Use the operations located in the third compartment of Fig. 26.1 to write the function prototypes of the class’s member functions. If we’ve not yet specified a return type for an operation, we declare the member function with return type `void`. Refer to the class diagrams of Figs. 6.22–6.25 to declare any necessary parameters. For example, adding the public operation `execute` in class `Withdrawal`, which has an empty parameter list, yields the prototype in line 15 of Fig. 26.7. *[Note: We code the definitions of member functions in .cpp files when we implement the complete ATM system in Section 26.4.]*

![](img/bfd978e7e9b192bab46ec2a89e481263_1152_0.png)

## Software Engineering Observation 26.1

> *Several UML modeling tools can convert UML-based designs into C++ code, considerably speeding the implementation process. For more information on these “automatic” code generators, refer to our UML Resource Center at www.deitel.com/UML/.*

This concludes our discussion of the basics of generating class header files from UML diagrams. In Section 26.3, we demonstrate how to modify the header files to incorporate the object-oriented concept of inheritance.

An additional Transaction derived class that overrides the execute member function with a version appropriate for the new transaction type. We would need to make only minimal changes to the system code to allow users to choose the new transaction type from the main menu and for the ATM to instantiate and execute objects of the new derived class. The ATM could execute transactions of the new type using the current code, because it executes all transactions identically.

As you learned earlier in the chapter, an abstract class like Transaction is one for which you never intend to instantiate objects. An abstract class simply declares common attributes and behaviors for its derived classes in an inheritance hierarchy. Class Transaction defines the concept of what it means to be a transaction that has an account number and executes. You wonder why we bother to include private virtual member function execute in class Transaction if execute lacks a concrete implementation. Conceptually, we include this member function because it’s the defining behavior of all transactions—executing. Technically, we must include member function execute in base class Transaction so that the ATM (or any other class) can polymorphically invoke each derived class’s overridden version of this function through a Transaction pointer or reference.

## Additional Attribute of Classes Withdrawal and Deposit

Derived classes BalanceInquiry, Withdrawal and Deposit inherit attribute accountNumber from base class Transaction, but classes Withdrawal and Deposit contain the additional attribute amount that distinguishes them from class BalanceInquiry. Classes Withdrawal and Deposit require this additional attribute to store the amount of money that the user wishes to withdraw or deposit. Class BalanceInquiry has no need for such an attribute and requires only an account number to execute. Even though two of the three Transaction derived classes share this attribute, we do not place it in base class Transaction—we place only features common to all the derived classes in the base class, so derived classes do not inherit unnecessary attributes (and operations).

## Class Diagram with Transaction Hierarchy Incorporated

Figure 26.10 presents an updated class diagram of our model that incorporates inheritance and introduces class Transaction. We model an association between class ATM and class Transaction to show that the ATM, at any given moment, either is executing a transaction or is not (i.e., zero or one objects of type Transaction exist in the system at a time). Because a Withdrawal is a type of Transaction, we no longer draw an association line directly between class ATM and class Withdrawal—derived classes with Withdrawal inherits base class Transaction’s association with class ATM. Derived classes BalanceInquiry and Deposit also inherit this association, which replaces the previously omitted associations between classes BalanceInquiry and Deposit and class ATM. Note again the use of triangular hollow arrow-heads to indicate the specializations of class Transaction, as indicated in Fig. 26.9.

We also add an association between class Transaction and the BankDatabase (Fig. 26.10). All Transactions require a reference to the BankDatabase so they can access and modify account information. Each Transaction derived class inherits this reference, so we no longer model the association between class Withdrawal and the BankDatabase. The association between class Transaction and the BankDatabase replaces the previously omitted associations between classes BalanceInquiry and Deposit and the BankDatabase.

We include an association between class Transaction and the Screen because all Transactions display output to the user via the Screen. Each derived class inherits this

- 1. If a class A is a generalization of class B, then class B is derived from (and is a specialization of) class A. For example, abstract base class Transaction is a generalization of class Withdrawal. Thus, class Withdrawal is derived from (and is a specialization of) class Transaction. Figure 26.12 contains a portion of class Withdrawal’s header file, in which the class definition indicates the inheritance relationship between Withdrawal and Transaction (line 9).

```cpp
// Fig. 26.12: Withdrawal.h
// Definition of class Withdrawal that represents a withdrawal transaction
#ifndef WITHDRAWAL_H
#define WITHDRAWAL_H

#include "transaction.h" // Transaction class definition

// class Withdrawal derives from base class Transaction
class Withdrawal : public Transaction
{
}; // end class Withdrawal

#endif // WITHDRAWAL_H
```

**Fig. 26.12** | *Withdrawal class definition that derives from Transaction.*

- 2. If class A is an abstract class and class B is derived from class A, then class B must implement the pure virtual functions of class A if class B is to be a concrete class. For example, class Transaction contains pure virtual function execute, so class Withdrawal must implement this member function if we want to instantiate a Withdrawal object. Figure 26.13 contains the C++ header file for class Withdrawal from Fig. 26.10 and Fig. 26.11. Class Withdrawal inherits data member accountNumber from base class Transaction, so Withdrawal does not declare this data member. Class Withdrawal also inherits references to the Screen and the BankDatabase from its base class Transaction, so we do not include these references in our code. Figure 26.11 specifies attribute amount and operation execute for class Withdrawal. Line 19 of Fig. 26.13 declares a data member for attribute amount. Line 16 contains the function prototype for operation execute. Recall that, to be a concrete class, derived class Withdrawal must provide a concrete implementation of the pure virtual function execute in base class Transaction. The prototype in line 16 signals your intent to override the base class pure virtual function. You must provide this prototype if you’ll provide an implementation in the .cpp file. We present this implementation in Section 26.4. The keypad and cashDispenser references (lines 20–21) are data members derived from Withdrawal’s associations in Fig. 26.10. In the implementation of this class in Section 26.4, a constructor initializes these references to actual objects. Once again, to be able to compile the declarations of the references in lines 20–21, we include the forward declarations in lines 8–9.

## ATM Case Study Wrap-Up

This concludes our object-oriented design of the ATM system. A complete C++ implementation of the ATM system in 850 lines of code appears in Section 26.4. This working
