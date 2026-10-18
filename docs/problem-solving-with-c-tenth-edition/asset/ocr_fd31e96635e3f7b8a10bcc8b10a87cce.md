# DISPLAY 10.9 A SavingsAccount Derived Class (part 2 of 2)

```
39     set(newDollars, newCents, getRate());
40   }
41   void SavingsAccount::withdraw(int dollars, int cents)
42   {
43     double balance = getBalance();
44     balance -= dollars;
45     balance -= (static_cast<double>(cents) / 100);
46     int newDollars = static_cast<int>(balance);
47     int newCents = static_cast<int>((balance - newDollars) * 100);
48     set(newDollars, newCents, getRate());
49   }
```

The withdraw function subtracts the amount from the balance and changes the member variables via the set function

# Screen Output

```
Account balance $100.50
Interest rate 5.50%
Depositing $10.25.
Account balance $110.75
Interest rate 5.50%
Withdrawing $11.80.
Account balance $98.95
Interest rate 5.50%
```

```
//Create a new CD with $1000, 6% interest, 180 days to maturity
CDAccount newCD(1000, 0, 6.0, 180);
newCD.deposit(100,50);
daysToMaturity = newCD.getDaysToMaturity();
//Returns 180
balance = newCD.getBalance();
//Returns 1100.50
```

Invoking a function in SavingsAccount

Invoking a function in CDAccount

Invoking a function in BankAccount

This short example has only scratched the surface of what is possible using inheritance. Additional details are described in Chapter 15. While it does take some effort to learn how to effectively design classes using inheritance, the effort will pay off in the long run. You will end up writing less code that is easier to understand and maintain than code that does not use inheritance.