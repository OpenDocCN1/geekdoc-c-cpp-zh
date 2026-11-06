![](bbox=[0.124, 0.092, 0.196, 0.144])

# Performance Tip 6.4

For passing large objects, use a `const` reference parameter to simulate the appearance and security of pass-by-value and avoid the overhead of passing a copy of the large object.

Similarly, class `Account`’s `getName` member function was defined with the header

```
```cpp
std::string getName() const
```
```

which indicates that a `string` is returned by value. Changing this to

```
```cpp
const std::string& getName() const
```
```

indicates that the `string` should be returned by reference (eliminating the overhead of copying a `string`) and that the caller cannot modify the returned `string`.

# Returning a Reference to a Local Variable