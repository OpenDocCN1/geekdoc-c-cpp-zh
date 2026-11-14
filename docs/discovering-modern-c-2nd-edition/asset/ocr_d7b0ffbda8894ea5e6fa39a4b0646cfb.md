feeling for it. The easiest syntactical case is the equality of `TPara` and `FPara`:

```
template <typename TPara>
void f1(TPara p);
```

This means the function parameter is a local copy of the argument. We call `f1` with an `int` literal, an `int` variable, and a mutable and constant `int` reference:

```
template <typename TPara>
void f1(TPara p) {}
```

```
int main ()
{
    int     i = 0;
    int&    j = i;
    const int& k = i;

    f1(3);
    f1(i);
    f1(j);
    f1(k);
    ...
}
```

In all four instantiations, `TPara` is replaced by `int` so that the type of the function parameter `p` is also `int`. So if the function parameter is a type parameter without a qualifier, `TPara` corresponds to the type of the argument after removing its qualifiers, e.g., an argument of type `const int&` leads to a function parameter of type `int`. This template function accepts all arguments as long as their types can be copied or moved in case of rvalues. As a counterexample, a `unique_ptr` with its deleted copy constructor can only be passed as a temporary object:

Click here to view code image

```
unique_ptr<int> up;
// f1(up);        // Error: no copy constructor
f1(move(up));    // Okay: use move constructor
```

# 3.1.2.2 Lvalue-Reference Parameters