# 3.2.5 Calling Class `Account`’s `setName` Member Function

The `Account` class’s `setName` member function stores an account name in a particular `Account` object. Line 19

```
```java
myAccount.setName(theName); // put theName in myAccount
```
```

calls `myAccount`’s `setName` member function. A member-function call can supply **arguments** that help the function perform its task. You place the arguments in the function call’s parentheses. Here, `theName`’s value (input by line 18) is the *argument* that’s passed to `setName`, which stores `theName`’s value in the object `myAccount`.

From `main`’s view, when `setName` is called:

+   1. The program transfers execution from line 19 in `main` to `setName` member function’s definition. The call passes to the function the *argument* value in the call’s parentheses—that is, the `theName` object’s value. Because `setName` was called via the