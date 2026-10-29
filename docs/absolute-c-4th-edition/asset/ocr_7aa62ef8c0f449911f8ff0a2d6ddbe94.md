# Display 7.2 BankAccount Class (part 2 of 3)

```
40  int dollarsPart(double amount);
41  int centsPart(double amount);
42  int round(double number);
43
44  double fraction(double percent);
45  //Converts a percentage to a fraction. For example, fraction(50.3) returns 0.503.
46 }
```

```
46 int main()
47 {
48     BankAccount account1(1345.52, 2.3), account2;
49     cout << "account1 initialized as follows:\n";
50     account1.output();
51     cout << "account2 initialized as follows:\n";
52     account2.output();
53
54     account1 = BankAccount(999, 99, 5.5);
55     cout << "account1 reset to the following:\n";
56     account1.output();
57
58     cout << "Enter new data for account 2:\n";
59     account2.input();
60     cout << "account2 reset to the following:\n";
61     account2.output();
62
63     account2.update();
64     cout << "In one year account2 will grow to:\n";
65     account2.output();
66
67     return 0;
68 }
```

```
65 BankAccount::BankAccount(double balance, double rate)
66   : accountDollars(dollarsPart(balance)), accountCents(centsPart(balance))
67 {
68     setRate(rate);
69 }
70
71 BankAccount::BankAccount(int dollars, int cents, double rate)
72 {
73     setBalance(dollars, cents);
74     setRate(rate);
75 }
76
77 BankAccount::BankAccount(int dollars, double rate)
78   : accountDollars(dollars), accountCents(0)
79 {
80     setRate(rate);
81 }
```

> This declaration causes a call to the default constructor. Notice that there are no parentheses.

> an explicit call to the constructor BankAccount::BankAccount

> These functions check that the data is appropriate.