```
```csharp
_accountNumber = ++_nextAccountNumber;
_balance = initialBalance;
}
public decimal Balance
{
    get { return _balance; }
    // Protected setter lets subclass use Balance property to set.
    protected set { _balance = value; }
}
// Deposit -- Any positive deposit is allowed.
public void Deposit(decimal amount)
{
    if (amount > 0)
    {
        Balance += amount;
    }
}
// Withdraw -- You can withdraw any amount up to the
// balance.  return the amount withdrawn.
public decimal Withdraw(decimal withdrawal)
{
    if (Balance <= withdrawal)
    {
        withdrawal = Balance;
    }
    Balance -= withdrawal;
    return withdrawal;
}
// ToString -- Stringify the account.
public string ToBankAccountString()
{
    return String.Format("{0} - {1:C}",
        _accountNumber, Balance);
}
// SavingsAccount -- A bank account that draws interest
public class SavingsAccount : BankAccount
{
    public decimal _interestRate;
    // InitSavingAccount -- Input the rate expressed as a
    // rate between 0 and 100.
    public SavingsAccount(decimal interestRate) : this(interestRate, 0) { }
    public SavingsAccount(decimal interestRate, decimal initial) : base(initial)
    {
        this._interestRate = interestRate / 100;
    }
    // AccumulateInterest -- Invoke once per period.
    public void AccumulateInterest()
    {
        // Use protected setter and public getter via Balance property.
        Balance = Balance + (decimal)(Balance * _interestRate);
    }
    // ToString -- Stringify the account.
    public string ToSavingsAccountString()
    {
        return String.Format("{0} ({1}%)",
            ToBankAccountString(), interestRate * 100);
    }
}
public class Program
{
    // DirectDeposit -- Deposit my paycheck automatically.
```
```