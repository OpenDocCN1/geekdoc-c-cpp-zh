# Display 7.2   BankAccount Class (part 6 of 6)

```
183
184  double BankAccount::fraction(double percent)
185  {
186      return (percent/100.0);
187  }
```

# Sample Dialogue

```
account1 initialized as follows:
Account balance: $1345.52
Rate: 2.3%
account2 initialized as follows:
Account balance: $0.00
Rate: 0%
account1 reset to the following:
Account balance: $999.99
Rate: 5.5%
Enter new data for account 2:
Enter account balance $100.00
Enter interest rate (NO percent sign): 10
account2 reset to the following:
Account balance: $100
Rate: 10%
In one year account2 will grow to:
Account balance: $110
Rate: 10%
```

# Self-Test Exercises

+   3. The function `BankAccount::input` in Display 7.2 reads the balance of the account as a value of type double. When the value is stored in the computer’s memory in binary form, this can create a slight error. It would normally not be noticed, and the function is good enough for the demonstration class `BankAccount`. Spending too much time on numerical analysis would detract from the message at hand. Still, this input function is not good enough for banking. Rewrite the function `BankAccount::input` so it reads an amount such as 78.96 as the `int` 76 and the three chars `'1'`, `'9'`, and `'6'`. You can assume the user always enters two digits for the cents in an amount, such as 99.00 instead of just 99 and nothing more. Hint: The following formula will convert a digit to the corresponding int value, such as `'6'` to 6:

```
static_cast<int>(digit) - static_cast<int>('0')
```