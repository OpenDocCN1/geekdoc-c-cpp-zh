You can invoke member function `setBalance` using the dot (`.`) and arrow (`->`) member selection operators as follows:

```
```cpp
{
    // call setBalance via the Account object
    account.setBalance(123.45);

    // call setBalance via a reference to the Account object
    accountRef.setBalance(123.45);

    // call setBalance via a pointer to the Account object
    accountPtr->setBalance(123.45);
```
```