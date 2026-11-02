Alternatively, you can supply a second reference parameter for that purpose:

```
void withdraw(double& balance, double amount, double& success)
```

# sec09/account.cpp

```
```cpp
#include <iostream>
using namespace std;
/**
 * Withdraws the amount from the given balance, or withdraws
 * a penalty if the balance is insufficient.
 * @param balance the balance from which to make the withdrawal
 * @param amount the amount to withdraw
 */
void withdraw(double& balance, double amount)
{
    const double PENALTY = 10;
    if (balance >= amount)
    {
        balance = balance - amount;
    }
    else
    {
        balance = balance - PENALTY;
    }
}
int main()
{
    double harrys_account = 1000;
    double sallys_account = 500;
    withdraw(harrys_account, 100);
    // Now harrys_account is 900
    withdraw(harrys_account, 1000); // Insufficient funds
    // Now harrys_account is 890
    withdraw(sallys_account, 150);
    cout << "Harry's account: " << harrys_account << endl;
    cout << "Sally's account: " << sallys_account << endl;
    return 0;
}
```
```

# Program Run

Harry's account: 890
Sally's account: 350

![](bbox=[0.12, 0.85, 0.2, 0.92])

# Programming Tip 5.7

# Prefer Return Values to Reference Parameters

Some programmers use reference parameters as a mechanism for setting the result of a function. For example,

```
```cpp
void cube_volume(double side_length, double& volume)
{
    volume = side_length * side_length * side_length;
}
```
```