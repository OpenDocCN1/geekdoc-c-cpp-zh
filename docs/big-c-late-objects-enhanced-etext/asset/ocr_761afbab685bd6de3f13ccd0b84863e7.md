The nullptr pointer does not point to any object.

There is a special value, nullptr, that you should use to indicate a pointer that doesn't point anywhere. If you define a pointer variable and are not ready to initialize it quite yet, set it to nullptr.

```
double* account_pointer = nullptr; // Will set later
```

You can later test whether the pointer is still nullptr. If it is, don't use it.

```
if (account_pointer != nullptr) { cout << *account_pointer; } // OK
```

Trying to access data through a nullptr pointer is illegal, and it will cause your program to terminate.

The reserved word nullptr was introduced in C++ 11. If you use an older version of C++, use the NULL constant instead.

The following program demonstrates the behavior of pointers. We execute the same withdrawal statement twice, but with different values for account_pointer. Each time, a different account is modified.

# sec01/accounts.cpp

```
```cpp
#include <iostream>
using namespace std;
int main()
{
    double harrys_account = 0;
    double joint_account = 2000;
    double* account_pointer = &harrys_account;
    *account_pointer = 1000; // Initial deposit
    *account_pointer = *account_pointer - 100; // Withdraw $100
    cout << "Balance: " << *account_pointer << endl; // Print balance
    // Change the pointer value
    account_pointer = &joint_account;
    // The same statements affect a different account
    *account_pointer = *account_pointer - 100; // Withdraw $100
    cout << "Balance: " << *account_pointer << endl; // Print balance
    return 0;
}
```
```

# Program Run

```
Balance: 900
Balance: 1900
```

![](bbox=[0.15, 0.85, 0.25, 0.98])

# Common Error 7.1

# Confusing Pointers with the Data to Which They Point

A pointer is a memory address—a number that tells where a value is located in memory. It is a common error to confuse the pointer with the variable to which it points:

```
double* account_pointer = &joint_account;
account_pointer = 1000; // Error
```