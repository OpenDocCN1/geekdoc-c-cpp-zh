```
~~~~~~~~~~        ^
operators.cpp:7:5: note: 'operator+' declared here
    void operator + (B);

1 error generated.
```

The lookup rules for operators in expressions are different than the lookup rules for operator function names in a function call.

Here *operator+ (a,a)* is in error because global operator is hidden by the member operator. When the expression *a + a* is ok as it calls the global *operator+*.