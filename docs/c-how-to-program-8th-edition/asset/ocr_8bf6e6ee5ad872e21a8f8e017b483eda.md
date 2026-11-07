**26.2**　b.

**26.3**　The design for class Account yields the header file in Fig. 26.37.

```
```cpp
// Fig. 26.37: Account.h
// Account class definition. Represents a bank account.
#ifndef ACCOUNT_H
#define ACCOUNT_H

class Account
{
public:
   bool validatePIN( int ); // is user-specified PIN correct?
   double getAvailableBalance(); // returns available balance
   double getTotalBalance(); // returns total balance
   void credit( double ); // adds an amount to the Account
   void debit( double ); // subtracts an amount from the Account
private:
   int accountNumber; // account number
   int pin; // PIN for authentication
   double availableBalance; // funds available for withdrawal
   double totalBalance; // funds available + funds waiting to clear
}; // end class Account

#endif // ACCOUNT_H
```
```

**Fig. 26.37**　Account class header file based on Fig. 26.1 and Fig. 26.2.

**26.4**　b.

**26.5**　False. The UML requires that we italicize abstract class names and operation names.

**26.6**　The design for class Transaction yields the header file in Fig. 26.38. In the implementation, a constructor initializes private reference attributes screen and bankDatabase to actual objects, and member functions getScreen and getBankDatabase access these attributes. These member functions allow classes derived from Transaction to access the ATM’s screen and interact with the bank’s database.

```
```cpp
// Fig. 26.38: Transaction.h
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
```
```

**Fig. 26.38**　Transaction class header file based on Fig. 26.10 and Fig. 26.11. (Part 1 of 2.)