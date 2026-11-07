```
```cpp
15
16    // pure virtual function to perform the transaction
17    virtual void execute() = 0; // overridden in derived classes
18  private:
19    int accountNumber; // indicates account involved
20    Screen &screen; // reference to the screen of the ATM
21    BankDatabase &bankDatabase; // reference to the account info database
22 }; // end class Transaction
23
24 #endif // TRANSACTION_H
```
```

Fig. 26.38 | Transaction class header file based on Fig. 26.10 and Fig. 26.11. (Part 2 of 2)