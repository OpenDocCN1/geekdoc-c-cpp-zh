# CHAPTER 7 Constructors and Other Tools

# 7.2  BankAccount Class (part 3 of 6)

```
51 cout << "account2 initialized as follows:\n"
52 account2.output();
```

```
53 account1 = BankAccount(999, 95, 5);
54 cout << "account1 reset to the following:\n"
55 account2.output();
```

```
56 cout << "Enter new data for account 2:\n"
57 account2.input();
58 cout << "account2 reset to the following:\n"
59 account2.output();
60 account2.update();
61 cout << "In one year account2 will grow to:\n"
62 account2.output();
```

```
63 return 0;
64 }
```

```
65 BankAccount::BankAccount(double balance, double rate)
66 : accountDollars(dollarsPart(balance))
67 accountCents(centsPart(balance))
```

```
68 {
69 setRate(rate);
70 }
```

```
71 BankAccount::BankAccount(int dollars, int cents, double rate)
72 {
73 setBalance(dollars, cents);
74 setRate(rate);
75 }
```

```
76 BankAccount::BankAccount(int dollars, double rate)
77 : accountDollars(dollars), accountCents(0);
```

```
78 {
79 setRate(rate);
80 }
```

```
81 BankAccount::BankAccount() : accountDollars(0),
82 accountCents(0), rate(0.0)
83 /*Body intentionally empty.*/
```

```
84 void BankAccount::update())
85 {
86 double balance = accountDollars + accountCents*0.01;
87 balance = balance + fraction(rate)*balance;
88 accountDollars = dollarsPart(balance);
89 accountCents = centsPart(balance);
90 }
```

![](bbox=[0.5, 0.153, 0.67, 0.203])

> an explicit call to the constructor
BankAccount::BankAccount

> These functions check
the data is appropriate.