```
bool ret = false;
if (account.balance >= amount) {
    account.balance -= amount;
    ret = true;
}
account.mtx.unlock(); // don't do this
return ret;
}
```

While this code works, you should not actually use the lock and unlock methods of a mutex directly. The reason for this is that if you lock a mutex you will need to ensure that unlock is called eventually no matter what happens. In particular, even if an error occurs, unlock should still be called.

A mutex is an example of a resource that must be released after it is acquired, even if an error is thrown. It is far from the only example. Memory is also a resource that should also be released eventually. The same is true for database connections and locks on the file system.

The solution for all problems of this type is to create a class that manages the resource and which makes sure that it is released by using a destructor. Destructors are called when a local variable is deleted even if an error has occurred.

In the case of a mutex, the class we need to manage the mutex already exists and is called a lock_guard<mutex>. (mutex is not the only lockable resource. You can create other types of lock_guard to manage other types of lockable resource. This is why lock_guard is a template.)

A lock_guard<mutex> calls lock on a mutex in its constructor and then calls unlock in its destructor. In particular, this means that if one uses a lock_guard<mutex> as shown below, the mutex will be unlocked even if an error occurs.

```
bool debitAccount(Account& account,
                  double amount) {
    lock_guard<mutex> lock(account.mtx);
    if (account.balance >= amount) {
        account.balance -= amount;
        return true;
    }
    return false;
}
```

# Tip: Resource acquisition is initialisation (RAII)

Whenever there is some clean-up that must occur at the end of your method,