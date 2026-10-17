
```cpp
out << setw(10) << record.getAccountNumber()
    << setw(16) << record.getLastName()
    << setw(11) << record.getFirstName() << right
    << setw(10) << setprecision(2) << fixed << record.getBalance() << endl;
```

// 从用户获取账户号码

```cpp
int getAccount(const char* prompt) {
    int accountNumber;
    // 获取账户号码
    do {
        cout << prompt << " (1 - 100): \n";
        cin >> accountNumber;
    } while (accountNumber < 1 || accountNumber > 100);
    return accountNumber;
}
```
