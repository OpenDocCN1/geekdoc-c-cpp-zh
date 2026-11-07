```
```cpp
// Fig. 9.6: AccountTest.cpp
// Displaying and updating Account balances.
#include <format>
#include <iostream>
#include "Account.h"

int main() {
    Account account1{"Mia Gonzalez", 50.00};
    Account account2{"Asahi Suzuki", -7.00};

    // display initial balance of each object
    std::cout << std::format("account1: {} balance is ${:.2f}\n",
        account1.getName(), account1.getBalance());
    std::cout << std::format("account2: {} balance is ${:.2f}\n",
        account2.getName(), account2.getBalance());
}
```
```

```
```text
account1: Mia Gonzalez balance is $50.00
account2: Asahi Suzuki balance is $0.00
```
```

**Fig. 9.6** | Displaying and updating Account balances.

# Reading a Deposit Amount from the User and Making a Deposit

Lines 17–21 prompt for, input and display the account1 deposit amount. Line 22 calls object account1’s deposit member function, passing the amount to add to account1’s balance. Lines 25–28 output both Accounts’ names and balances again to show that only account1’s balance changed.

```
```cpp
std::cout << "Enter deposit amount for account1: "; // prompt
double amount;
std::cin >> amount; // obtain user input
std::cout << std::format(
    "adding ${:.2f} to account1 balance\n", amount);
account1.deposit(amount); // add to account1's balance

// display balances
std::cout << std::format("account1: {} balance is ${:.2f}\n",
    account1.getName(), account1.getBalance());
std::cout << std::format("account2: {} balance is ${:.2f}\n",
    account2.getName(), account2.getBalance());
```
```

```
```text
Enter deposit amount for account1: 25.37
adding $25.37 to account1 balance

account1: Mia Gonzalez balance is $75.37
account2: Asahi Suzuki balance is $0.00
```
```

Lines 30–33 prompt for, input and display account2’s deposit amount. Line 34 calls object account2’s deposit member function with the argument amount to add that value to account2’s balance. Finally, lines 37–40 output both Accounts’ names and balances again to show that only account2’s balance changed.