Declare the Overdrawn event itself.

1. Use code similar to the following:

```
// Declare the Overdrawn event.
public event OverdrawnEventHandler Overdrawn;
```

Make the Debit method raise the event when necessary.

1. Modify the initial version of the method so it raises the event when necessary.
Use code similar to the following:

```
// Remove money from the account.
public void Debit (decimal amount)
{
    // See if there is enough money.
    if (Balance < amount)
    {
        // Not enough money. Raise the Overdrawn event.
        if (Overdrawn != null)
        {
            OverdrawnEventArgs args = new OverdrawnEventArgs();
            args.currentBalance = Balance;
            args.invalidBalance = Balance - amount;
            Overdrawn(this, args);
        }
    }
    else
    {
        // There's enough money.
        Balance -= amount;
    }
}
```

In the main program, register to receive the Overdrawn event so it can display a message box.

1. Use code similar to the following:

```
// Declare an account.
BankAccount MyAccount;

// Initialize the account.
private void Form1_Load(object sender, EventArgs e)
{
    // Initialize the account.
    MyAccount = new BankAccount();
    MyAccount.Balance = 100M;

    // Register to receive the Overdrawn event.
    MyAccount.Overdrawn += MyAccount_Overdrawn;

    // Display the current balance.
    balanceTextBox.Text = MyAccount.Balance.ToString("C");
}
```