# Modern C++: Return Type Deduction (C++14)

# Return type deduction for functions

C++14 implements automatic type deduction for function return values:

```
auto square(int n)
{
    return n * n;
}
```

The type of the return value of *square* is deduced to be an *int* by the compiler.