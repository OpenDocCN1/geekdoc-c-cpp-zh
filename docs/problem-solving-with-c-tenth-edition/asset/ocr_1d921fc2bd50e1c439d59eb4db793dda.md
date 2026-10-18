# DISPLAY 10.5 The BankAccount Class (part 3 of 3)

```
89
90 double BankAccount::getRate( )
91 {
92     return interestRate;
93 }
94
95 //Uses iostream:
96 void BankAccount::output(ostream& outs)
97 {
98     outs.setf(ios::fixed);
99     outs.setf(ios::showpoint);
100     outs.precision(2);
101     outs << "Account balance $" << balance << endl;
102     outs << "Interest rate " << interestRate << "%" << endl;
103 }
```

Stream parameter that can be replaced either with cout or with a file output stream

# Sample Dialogue

```
Start of Test:
account1 initial statement:
Account balance $123.99
Interest rate 3.00%
account1 with new setup:
Account balance $100.00
Interest rate 5.00%
account1 after update:
Account balance $105.00
Interest rate 5.00%
account2:
Account balance $105.00
Interest rate 5.00%
```

account1.update();

is the following:

```
{
    account1.balance = account1.balance +
    account1.fraction(account1.interestRate) * account1.balance;
}
```

Notice that the call to the member function fraction is handled in the same way in this regard as the references to the member variables.