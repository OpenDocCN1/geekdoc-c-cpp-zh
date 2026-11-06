*parameter* `accountName`. The constructor will then use `accountName` to initialize the *data member* `name`.

The constructor uses a **member-initializer list** (line 9)

```
```cpp
: name{accountName}
```
```

to initialize the `name` data member with the value of the parameter `accountName`. *Member initializers* appear between a constructor’s parameter list and the left brace that begins the constructor’s body. The member initializer list is separated from the parameter list with a colon (`:`). Each member initializer consists of a data member’s *variable name* followed by parentheses containing the member’s *initial value*. In this example, `name` is initialized with the parameter `accountName`’s value. If a class contains more than one data member, each member initializer is separated from the next by a comma. The member initializer list executes *before* the constructor’s body executes.

![](bbox=[0.122, 0.725, 0.196, 0.779])

# Performance Tip 3.1

> *You can perform initialization in the constructor’s body, but you’ll learn in **Chapter 9** that it’s more efficient to do it with member initializers, and some types of data members must be initialized this way.*