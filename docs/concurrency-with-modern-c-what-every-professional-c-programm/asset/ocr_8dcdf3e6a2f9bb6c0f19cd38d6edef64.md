# ### 11.1.5 Use pure functions

Haskell is called a pure functional language because it is based on pure functions. A pure function is a function which always produces the same results when given the same arguments. It has no side effect and can, therefore, not change the state of the program.

Pure functions have a significant advantage from the concurrency perspective. They can be reordered or automatically run on another thread.

Functions in C++ are per default impure. The following three functions are all pure, but each function has a different characteristic.

```
```cpp
int powFunc(int m, int n){
    if (n == 0) return 1;
    return m * powFunc(m, n-1);
}
```
```

powFunc is an ordinary function that runs at runtime.

```
```cpp
template<int m, int n>
struct PowMeta{
    static int const value = m * PowMeta<m, n-1>::value;
};

template<int m>
struct PowMeta<m, 0>{
    static int const value = 1;
};
```
```

PowMeta is a so-called meta-function because it runs at compile time.

```
```cpp
constexpr int powConst(int m, int n){
    int r = 1;
    for(int k = 1; k <= n; ++k) r *= m;
    return r;
}
```
```

The function powConst can run at runtime and at compile time. It is a constexpr function.

# ### 11.1.6 Look for the Right Abstraction

There are various ways to initialize a Singleton in a multithreading environment. You can rely on the standard library using a `lock_guard` or `std::call_once`, rely on the core language using a static