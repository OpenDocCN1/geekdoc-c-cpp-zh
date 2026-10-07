# 736 Chapter 13 Class Inheritance

Enter client's name: Brenda Birdherder
Enter client's account number: 212118
Enter opening balance: $5200
Enter 1 for Brass Account or 2 for BrassPlus Account: 2
Enter the overdraft limit: $800
Enter the interest rate as a decimal fraction: 0.10
Enter client's name: Tim Turtletop
Enter client's account number: 233255
ter opening balance: $688
Enter 1 for Brass Account or 2 for BrassPlus Account: 1

Client: Harry Fishshong
Account Number: 112233
Balance: $1500.00

Client: Dinah Otternose
Account Number: 121213
Balance: $1800.00
Maximum loan: $350.00
wed to bank: $0.00
Loan Rate: 10.00%

Client: Brenda Birdher
Account Number: 212118
Balance: $5200.00
Maximum loan: $800.00
wed to bank: $0.00
Loan Rate: 10.00%

Client: Tim Turtletop
Account Number: 233255
Balance: $688.00

Done.

The polymorphic aspect is provided by the following code:

```
for (i = 0; i < CLIENTS; i++)
{
p_clients[i]->ViewAcct();
out << endl;
}

```

If the array member points to a Brass object, Brass::ViewAcct() is invoked; if the array member points to a BrassPlus object, BrassPlus::ViewAcct() is invoked. If Brass::ViewAcct() were been declared as virtual, Brass::ViewAcct() would be invoked in all cases.