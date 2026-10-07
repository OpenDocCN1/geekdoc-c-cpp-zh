# noexcept (C++11)

The noexcept keyword is used to indicate that a function doesn’t throw an exception. It also can be used as an operator that determines whether its operand (an expression) potentially could throw an exception. It returns false if the operand could throw an exception and true otherwise. For example, consider the following declarations:

```
int hilt(int);
int halt(int) noexcept;
```

The expression noexcept(hilt) would evaluate as false, as the declaration of hilt() doesn’t guarantee that an exception won’t be thrown. But noexcept(halt) will evaluate as true.