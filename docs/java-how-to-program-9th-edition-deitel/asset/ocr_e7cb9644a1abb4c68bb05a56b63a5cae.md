```
// return reference to bank database
public BankDatabase getBankDatabase()
{
    return bankDatabase;
} // end method getBankDatabase

// perform the transaction (overridden by each subclass)
abstract public void execute();
} // end class Transaction
```

Fig. 13.20 | Abstract superclass Transaction represents an ATM transaction. (Part 2 of 2.)

Class Transaction has a constructor (lines 11–17) that takes as arguments the current user’s account number and references to the ATM’s screen and the bank’s database. Because Transaction is an abstract class, this constructor will be called only by the constructors of the Transaction subclasses.

The class has three public get methods—getAccountNumber (lines 20–23), getScreen (lines 26–29) and getBankDatabase (lines 32–35). These are inherited by Transaction subclasses and used to gain access to class Transaction’s private attributes.

Class Transaction also declares abstract method execute (line 38). It does not make sense to provide this method’s implementation, because a generic transaction cannot be executed. So, we declare this method abstract and force each Transaction subclass to provide a concrete implementation that executes that particular type of transaction.

# 13.4.9 Class BalanceInquiry

Class BalanceInquiry (Fig. 13.21) extends Transaction and represents a balance-inquiry ATM transaction. BalanceInquiry does not have any attributes of its own, but it inherits Transaction attributes accountNumber, screen and bankDatabase, which are accessible through Transaction’s public get methods. The BalanceInquiry constructor takes arguments corresponding to these attributes and simply forwards them to Transaction’s constructor using super (line 10).

```
// BalanceInquiry.java
// Represents a balance inquiry ATM transaction

public class BalanceInquiry extends Transaction
{
    // BalanceInquiry constructor
    public BalanceInquiry( int userAccountNumber, Screen atmScreen,
        BankDatabase atmBankDatabase )
    {
        super( userAccountNumber, atmScreen, atmBankDatabase );
    } // end BalanceInquiry constructor

    // performs the transaction
    @Override
    public void execute()
{
```

Fig. 13.21 | Class BalanceInquiry represents a balance-inquiry ATM transaction. (Part 1 of 2.)