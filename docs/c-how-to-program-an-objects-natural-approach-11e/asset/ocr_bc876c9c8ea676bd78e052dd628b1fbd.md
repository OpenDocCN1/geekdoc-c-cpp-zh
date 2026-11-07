+   - an object name,
+   - a reference to an object,
+   - a pointer to an object or
+   - a pointer to a specific class member (discussed briefly in Chapter 20).

We refer to these as handles on an object. The handle’s type helps the compiler determine the interface (that is, the member functions) accessible to the client via that handle. We’ll see in Section 9.19 that the compiler inserts an implicit handle called the `this` pointer each time you refer to a data member or member function from within an object.

# Dot (.) and Arrow (->) Member-Selection Operators

As you know, you can use an object’s name or a reference to an object followed by the dot member-selection operator (.) to access the object’s members. To reference an object’s members via a pointer to an object, follow the pointer name by the arrow member-selection operator (->) and the member name, as in *pointerName->memberName*.

# Accessing public Class Members Through Objects, References and Pointers

Consider an Account class that has a public deposit member function. Given the following declarations:

```
Account account{}; // an Account object
Account& ref{account}; // ref refers to an Account object
Account* ptr{&account}; // ptr points to an Account object
```

you can invoke member function deposit using the dot (.) and arrow (->) member-selection operators as follows:

```
account.deposit(123.45); // call deposit via account object’s name
ref.deposit(123.45); // call deposit via reference to account object
ptr->deposit(123.45); // call deposit via pointer to account object
```

Again, you should use references in preference to pointers whenever possible. We’ll continue to show pointers when required and to prepare you to work with them in the legacy code you’ll encounter in industry.

# Checkpoint

(Fill-in) To access an object’s members via a pointer to an object, use the ______ followed by the member name.
Answer: arrow member-selection operator (->).

2 (Code) Assume `timePtr` is a pointer to a `Time` object. Write a statement that uses `timePtr` to call the `Time` object’s `setTime` member function with the values 6, 45 and 0.
Answer: `timePtr->setTime(6, 45, 0);`

# 9.10 Access Functions and Utility Functions

# Access Functions

Access functions can read or display data but not modify it. Another use of access functions is to test whether a condition is true or false. Such functions are often called predicate