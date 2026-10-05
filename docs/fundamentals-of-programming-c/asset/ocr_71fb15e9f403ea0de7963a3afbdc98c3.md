# 14.2. FIELDS

```
// The simple database of bank accounts
vector<Account> customers;

// User command
char cmd;

// Are we done yet?
bool done = false;

do {
    cout << " [A]dd [N]ame [I]D [B]alance [Q]uit => ";
    cin >> cmd;
    switch (cmd) {
        case 'A':
        case 'a':
            // Add an account
            add_account(customers);
            break;
        case 'P':
        case 'p':
            // Print customer database
            print_accounts(customers);
            break;
        case 'N':
        case 'n':
            // Sort database by name
            sort(customers, less_than_by_name);
            print_accounts(customers);
            break;
        case 'I':
        case 'i':
            // Sort database by ID (account number)
            sort(customers, less_than_by_id);
            print_accounts(customers);
            break;
        case 'B':
        case 'b':
            // Sort database by account balance
            sort(customers, less_than_by_balance);
            print_accounts(customers);
            break;
        case 'Q':
            done = true;
            break;
    }
} while (!done);
```

Listing 14.2 (bankaccount.cpp) stores bank account objects in a vector (see Section 11.1). Also, a bank account object contains a **string** object as a field. This shows that objects can contain other objects and implies that objects can have arbitrarily complex structures.

A sample run of Listing 14.2 (bankaccount.cpp) prints