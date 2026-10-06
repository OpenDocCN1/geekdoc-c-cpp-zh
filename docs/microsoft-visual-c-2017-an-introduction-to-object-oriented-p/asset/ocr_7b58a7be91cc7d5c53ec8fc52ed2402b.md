# CHAPTER 13 Handling Events

(continued)

+   4. Add two methods. One makes account deposits by adding the parameter to the account balance, and the other makes withdrawals by subtracting the parameter value from the bank balance. Each uses the OnBalanceAdjusted event handler that reacts to all deposit and withdrawal events by displaying the new balance.

```
public void MakeDeposit(double amt) {
    balance += amt;
    OnBalanceAdjusted(EventArgs.Empty);
}
public void MakeWithdrawal(double amt) {
    balance -= amt;
    OnBalanceAdjusted(EventArgs.Empty);
}
```

+   5. Add the OnBalanceAdjusted() method that accepts an EventArgs parameter and calls BalanceAdjusted(), passing references to the newly adjusted BankAccount object and the EventArgs object. (Earlier the chapter, you learned that calling a method such as OnBalanceAdjusted() is also known as invoking the event.) Include a closing brace for the class.

```
public void OnBalanceAdjusted(EventArgs e) {
    BalanceAdjusted(this, e);
}
```

+   6. Save the file.

Creating an Event Listener

+   1. When you write an application that declares a BankAccount, you might want the client program to listen for BankAccount events. To do so, you create an EventListener class.

+   2. After the closing brace of the BankAccount class, type the following EventListener class that contains a BankAccount object. When the EventListener constructor executes, the BankAccount field is initialized with the constructor parameter. Using the += operator, to add the BankAccountBalanceAdjusted() method to the event delegate. Next, write the BankAccountBalanceAdjusted() method to display a message and information about the BankAccount.

(continues)