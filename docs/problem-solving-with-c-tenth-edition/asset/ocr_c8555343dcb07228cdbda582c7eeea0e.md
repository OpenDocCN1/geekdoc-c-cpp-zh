# DISPLAY 10.6 Class with Constructors (part 2 of 3)

```
24   //Postcondition: One year of simple interest has been added
25   //to the account balance.
26   double getBalance();
27   //Returns the current account balance.
28   double getRate();
29   //Returns the current account interest rate as a percentage.
30   void output(ostream& outs);
31   //Precondition: If outs is a file output stream, then
32   //outs has already been connected to a file.
33   //Postcondition: Account balance and interest rate
34   //have been written to the stream outs.
35 private:
36     double balance;
37     double interestRate;
38     double fraction(double percent);
39     //Converts a percentage to a fraction. For example, fraction(50.3)
40     //returns 0.503.
41 };
42 int main()
43 {
44   BankAccount account1(100, 2.3), account2;
45   cout << "account1 initialized as follows:\n";
46   account1.output(cout);
47   cout << "account2 initialized as follows:\n";
48   account2.output(cout);
49   account1 = BankAccount(999, 99, 5.5);
50   cout << "account1 reset to the following:\n";
51   account1.output(cout);
52   return 0;
53 }
54 BankAccount::BankAccount(int dollars, int cents, double rate)
55 {
56   if ((dollars < 0) || (cents < 0) || (rate < 0))
57   {
58     cout << "Illegal values for money or interest rate.\n";
59     return;
60   }
61   balance = dollars + 0.01 * cents;
62   interestRate = rate;
63 }
64 BankAccount::BankAccount(int dollars, double rate)
65 {
```

> This declaration causes a call to the default constructor. Notice that there are no parentheses.

> An explicit call to the constructor BankAccount::BankAccount