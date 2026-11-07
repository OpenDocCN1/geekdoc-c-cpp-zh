Now let us look at what happens when we initialize an object of this class with two string literals:

```
Person p{"Ben", "Cook"};
```

The compiler finds out that the provided constructor can perform the initialization. However, the types of the parameters do not fit. Therefore, the compiler generates code to first create two temporary `std::strings`, which are initialized by the values of the two string literals, and binds the parameters `f` and `l` to them:

![](bbox=[0.115, 0.209, 0.51, 0.403])

In general (if the *small string optimization (SSO)* is not available or the strings are too long), this means that code is generated that allocates memory for the value of each `std::string`.

However, the temporary strings created are not used directly as members `first` or `last`. Instead, they are used to initialize these members. Unfortunately, move semantics is not used here for two reasons:

+   - The parameters `f` and `l` are objects with names that exist for a longer period than the initialization of the members (you can still use them in the body of the constructor).
+   - The parameters are declared to be `const`, which disables move semantics even if we use `std::move()`.

As a consequence, the copy constructor for strings is called on each member initialization, again allocating memory for the values:

![](bbox=[0.115, 0.609, 0.51, 0.802])