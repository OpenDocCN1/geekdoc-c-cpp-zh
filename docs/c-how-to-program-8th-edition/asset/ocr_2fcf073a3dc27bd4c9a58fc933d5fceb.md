```
```cpp
// debits an amount from the account
void Account::debit( double amount )
{
    availableBalance -= amount; // subtract from available balance
    totalBalance -= amount; // subtract from total balance
} // end function debit

// returns account number
int Account::getAccountNumber() const
{
    return accountNumber;
} // end function getAccountNumber
```
```

Fig. 26.25 | Account class member-function definitions. (Part 2 of 2.)

Member function debit (lines 44–48) subtracts an amount of money (i.e., parameter amount) from an Account as part of a withdrawal transaction. This member function subtracts the amount from both data member availableBalance (line 46) and data member totalBalance (line 47), because a withdrawal affects both measures of an account balance.

Member function getAccountNumber (lines 51–54) provides access to an Account’s accountNumber. We include this member function in our implementation so that a client of the class (i.e., BankDatabase) can identify a particular Account. For example, BankDatabase contains many Account objects, and it can invoke this member function on each of its Account objects to locate the one with a specific account number.

# 26.4.7 Class BankDatabase

Class BankDatabase (Figs. 26.26–26.27) models the bank’s database with which the ATM interacts to access and modify a user’s account information. The class definition (Fig. 26.26) declares function prototypes for the class’s constructor and several member functions. We discuss these momentarily. The class definition also declares the BankDatabase’s data members. We determine one data member for class BankDatabase based on its composition relationship with class Account. Recall from Fig. 26.10 that a BankDatabase is composed of zero or more objects of class Account. Line 24 of Fig. 26.26 implements data member accounts—a vector of Account objects—to implement this composition relationship. Lines 6–7 allow us to use vector in this file. Line 27 contains the function prototype for a private utility function getAccount that allows the member functions of the class to obtain a pointer to a specific Account in the accounts vector.

```
```cpp
// BankDatabase.h
// BankDatabase class definition. Represents the bank's database.
#ifndef BANK_DATABASE_H
#define BANK_DATABASE_H

#include <vector> // class uses vector to store Account objects
using namespace std;
```
```

Fig. 26.26 | BankDatabase class definition. (Part 1 of 2.)