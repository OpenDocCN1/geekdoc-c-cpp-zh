```
{ // Round off the double to the nearest cent before depositing.
decimal temp = (decimal)amount;
temp = Decimal.Round(temp, 2);
_balance += temp;
}
}
// Withdraw -- You can withdraw any amount up to the
// balance; return the amount withdrawn.
public double Withdraw(double withdrawal)
{
// Convert to decimal and work with the decimal version.
decimal decWithdrawal = (decimal)withdrawal;
if (_balance <= decWithdrawal)
{
decWithdrawal = _balance;
}
_balance -= decWithdrawal;
return (double)decWithdrawal; // Return a double.
}
// GetString -- Return the account data as a string.
public string GetString()
{
string s = String.Format("#{0} = {1:C}",
GetAccountNumber(), GetBalance());
return s;
}
}
```

I've converted all internal representations to decimal values, a type better adapted to handling bank account balances than double in any case. The Deposit() method now uses the Decimal.Round() method to round the deposit amount to the nearest cent before making the deposit. The output from the program is now as expected:

```
Create a bank account object
Depositing $123.45
Account = #1001 = $123.45
Adding $0.00
Resulting account = #1001 = $123.45
Press Enter to terminate...
```

# So what?

You could argue that I should have written the BankAccount program using decimal input arguments to begin with, and I probably would agree. But the point is that I didn't. Other applications were written using double as the form of storage. A problem arose. The BankAccount class was able to fix the problem internally and make no changes to the application software. (Notice that the class's public interface didn't change: Balance() and Withdraw() still return doubles, and Deposit() and Withdraw() still take a double parameter.)

I repeat: Applications using class BankAccount didn't have to change.

![](bbox=[0.1, 0.88, 0.18, 0.97])