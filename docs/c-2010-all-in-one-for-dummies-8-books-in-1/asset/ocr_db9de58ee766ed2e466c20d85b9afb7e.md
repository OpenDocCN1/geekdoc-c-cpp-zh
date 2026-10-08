# Inheriting from a BankAccount Class (A More Complex Example) 289

```
// BankAccount -- Simulate a bank account, each of which
// carries an ID (which is assigned)
// on creation) and a balance,
// The base class
```

```
public class BankAccount {
    // Bank accounts starts at 1000 and increase sequentially.
    public static int _nextAccountNumber = 1000;
    // Maintain the account number and balance for each object.
    private int _accountNumber;
    private decimal _balance;
    // Initialize a bank account with the next account ID and the
    // specified initial balance (default to zero).
    public void InitBankAccount() {}
    public void InitBankAccount(decimal initialBalance) {
        _accountNumber = ++_nextAccountNumber;
        _balance = initialBalance;
    }
```

```
// Balance property.
    public decimal Balance {
        get { return _balance; }
    }
```

```
// Deposit -- any positive deposit is allowed.
    public void Deposit(decimal amount) {
        if (amount > 0) {
            _balance += amount;
        }
    }
```

```
// Withdraw -- You can withdraw any amount up to the
// balance; return the account withdrawal.
    public decimal Withdraw(decimal withdrawal) {
        if (Balance <= withdrawal) // Use balance
            withdrawal = Balance;
        _balance -= withdrawal;
        return withdrawal;
    }
```

```
// Stringify the account.
    public string ToString() {
        return String.Format("{0} - {1:C}",
            _accountNumber, Balance);
    }
```

```
// SavingsAccount -- A bank account that draws interest
    public class SavingsAccount : BankAccount {
    private decimal _interestRate;
    // SavingsAccount -- Input the interest rate between 0 and 100.
    public void InitSavingsAccount(decimal interestRate) {
        _interestRate = interestRate;
    }
```

![](bbox=[0.888, 0.323, 0.966, 0.477])