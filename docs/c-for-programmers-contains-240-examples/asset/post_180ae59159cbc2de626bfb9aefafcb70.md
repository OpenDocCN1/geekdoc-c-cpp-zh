
initial available balance and the initial total balance as arguments. Lines 8–11 assign these values to the class's data members using member initializers.

Member function validatePIN (lines 17–23) determines whether a user-specified PIN (i.e., parameter userPIN) matches the PIN associated with the account (i.e., data member pin). Recall that we modeled this member function's parameter userPIN in the UML class diagram of Fig. 6.35. If the two PINs match, the member function returns true (line 20); otherwise, it returns false (line 22).

Member functions getAvailableBalance (lines 26–29) and getTotalBalance (lines 32–35) are get functions that return the values of double data members availableBalance and totalBalance, respectively.

```
// Account.cpp
// Member-function definitions for class Account.
#include "Account.h" // Account class definition

// Account constructor initializes attributes
Account::Account( int theAccountNumber, int thePIN,
    double theAvailableBalance, double theTotalBalance )
  : accountNumber( theAccountNumber ),
    pin( thePIN ),
    availableBalance( theAvailableBalance ),
    totalBalance( theTotalBalance )
{
    // empty body
} // end Account constructor

// determines whether a user-specified PIN matches PIN in Account
bool Account::validatePIN( int userPIN ) const
{
    if ( userPIN == pin )
        return true;
    else
        return false;
} // end function validatePIN

// returns available balance
double Account::getAvailableBalance() const
{
    return availableBalance;
} // end function getAvailableBalance

// returns the total balance
double Account::getTotalBalance() const
{
    return totalBalance;
} // end function getTotalBalance

// credits an amount to the account
void Account::credit( double amount )
{
    totalBalance += amount; // add to total balance
} // end function credit
```

```
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

Fig. E.12 | Account class member-function definitions. (Part 2 of 2.)

Member function credit (lines 38–41) adds an amount of money (i.e., parameter amount) to an Account as part of a deposit transaction. Note that this member function adds the amount only to data member totalBalance (line 40). The money credited to an account during a deposit does not become available immediately, so we modify only the total balance. We assume that the bank updates the available balance appropriately at a later time. Our implementation of class Account includes only member functions required for carrying out ATM transactions. Therefore, we omit the member functions that some other bank system would invoke to add to data member availableBalance (to confirm a deposit) or subtract from data member totalBalance (to reject a deposit).

Member function debit (lines 44–48) subtracts an amount of money (i.e., parameter amount) from an Account as part of a withdrawal transaction. This member function subtracts the amount from both data member availableBalance (line 46) and data member totalBalance (line 47), because a withdrawal affects both measures of an account balance.

Member function getAccountNumber (lines 51–54) provides access to an Account’s accountNumber. We include this member function in our implementation so that a client of the class (i.e., BankDatabase) can identify a particular Account. For example, BankDatabase contains many Account objects, and it can invoke this member function on each of its Account objects to locate the one with a specific account number.

## E.8 Class BankDatabase

Class BankDatabase (Figs. E.13–E.14) models the bank’s database with which the ATM interacts to access and modify a user’s account information. The class definition (Fig. E.13) declares function prototypes for the class’s constructor and several member functions. We discuss these momentarily. The class definition also declares the BankDatabase’s data members. We determine one data member for class BankDatabase based on its composition relationship with class Account. Recall from Fig. 13.28 that a BankDatabase is composed of zero or more objects of class Account. Line 24 of Fig. E.13 implements data member accounts—a vector of Account objects—to implement this composition relationship. Lines 6–7 allow us to use vector in this file. Line 27 contains the function prototype for a private utility function getAccount that allows the member functions of the class to obtain a pointer to a specific Account in the accounts vector.

```
// BankDatabase.h
// BankDatabase class definition. Represents the bank's database.
#ifndef BANK_DATABASE_H
#define BANK_DATABASE_H

#include <vector> // class uses vector to store Account objects
using std::vector;

#include "Account.h" // Account class definition

class BankDatabase
{
public:
    BankDatabase(); // constructor initializes accounts

    // determine whether account number and PIN match those of an Account
    bool authenticateUser( int, int ); // returns true if Account authentic

    double getAvailableBalance( int ); // get an available balance
    double getTotalBalance( int ); // get an Account's total balance
    void credit( int, double ); // add amount to Account balance
    void debit( int, double ); // subtract amount from Account balance
private:
    vector< Account > accounts; // vector of the bank's Accounts

    // private utility function
    Account * getAccount( int ); // get pointer to Account object
}; // end class BankDatabase

#endif // BANK_DATABASE_H
```

Fig. E.13 | BankDatabase class definition.

## BankDatabase Class Member-Function Definitions

Figure E.14 contains the member-function definitions for class BankDatabase. We implement the class with a default constructor (lines 6–15) that adds Account objects to data member accounts. For the sake of testing the system, we create two new Account objects with test data (lines 9–10), then add them to the end of the vector (lines 13–14). Note

```
// BankDatabase.cpp
// Member-function definitions for class BankDatabase.
#include "BankDatabase.h" // BankDatabase class definition

// BankDatabase default constructor initializes accounts
BankDatabase::BankDatabase()
{
    // create two Account objects for testing
    Account account1( 12345, 54321, 1000.0, 1200.0 );
    Account account2( 98765, 56789, 200.0, 200.0 );
```

```
12    // add the Account objects to the vector accounts
13    accounts.push_back( account1 ); // add account1 to end of vector
14    accounts.push_back( account2 ); // add account2 to end of vector
15  } // end BankDatabase default constructor
16
17  // retrieve Account object containing specified account number
18  Account * BankDatabase::getAccount( int accountNumber )
19  {
20    // loop through accounts searching for matching account number
21    for ( size_t i = 0; i < accounts.size(); i++ )
22    {
23      // return current account if match found
24      if ( accounts[ i ].getAccountNumber() == accountNumber )
25        return &accounts[ i ];
26    } // end for
27
28    return NULL; // if no matching account was found, return NULL
29  } // end function getAccount
30
31  // determine whether user-specified account number and PIN match
32  // those of an account in the database
33  bool BankDatabase::authenticateUser( int userAccountNumber,
34      int userPIN )
35  {
36    // attempt to retrieve the account with the account number
37    Account * const userAccountPtr = getAccount( userAccountNumber );
38
39    // if account exists, return result of Account function validatePIN
40    if ( userAccountPtr != NULL )
41      return userAccountPtr->validatePIN( userPIN );
42    else
43      return false; // account number not found, so return false
44  } // end function authenticateUser
45
46  // return available balance of Account with specified account number
47  double BankDatabase::getAvailableBalance( int userAccountNumber )
48  {
49    Account * const userAccountPtr = getAccount( userAccountNumber );
50    return userAccountPtr->getAvailableBalance();
51  } // end function getAvailableBalance
52
53  // return total balance of Account with specified account number
54  double BankDatabase::getTotalBalance( int userAccountNumber )
55  {
56    Account * const userAccountPtr = getAccount( userAccountNumber );
57    return userAccountPtr->getTotalBalance();
58  } // end function getTotalBalance
59
60  // credit an amount to Account with specified account number
61  void BankDatabase::credit( int userAccountNumber, double amount )
62  {
```

Fig. E.14 | BankDatabase class member-function definitions. (Part I of 3.)
