c. In a class, such a section is by default a private: section.
d. In a struct, such a section is by default a public: section.

19. A possible correct answer is as follows:

```
double difference(BankAccount account1, BankAccount account2)
{
    return (account1.getBalance() - account2.getBalance());
}
```

Note that the following is not correct, because balance is a private member.

```
double difference(BankAccount account1, BankAccount account2)
{
    return (account1.balance - account2.balance); // ILLEGAL
}
```

20. void double update(BankAccount& theAccount)

```
{
    theAccount.update();
    theAccount.update();
}
```

Note that since this is not a member function, you must give the object name and dot operator when you call update.

21. BankAccount newAccount(BankAccount oldAccount)

```
{
    BankAccount temp;
    temp.set(0, oldAccount.getRate());
    return temp;
}
```

22. YourClass anObject(42, 'A'); // LEGAL
YourClass anotherObject; // LEGAL
YourClass yetAnotherObject(); // PROBLEM
anObject = YourClass(99, 'B'); // LEGAL
anObject = YourClass(); // LEGAL
anObject = YourClass; // ILLEGAL

The statement marked // PROBLEM is not, strictly speaking, illegal, but it does not mean what you might think it means. If you mean this to be a declaration of an object called yetAnotherObject, then it is wrong. It is a correct function declaration for a function called yetAnotherObject that takes zero arguments and that returns a value of type YourClass, but that is not the intended meaning. As a practical matter, you can