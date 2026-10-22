```
```cpp
template<typename T>
class Base {
public:
    void bar();
};

template<typename T>
class Derived : Base<T> {
public:
    void foo() {
        bar(); // calls external bar() or error
    }
};
```
```

In this example, for resolving the symbol `bar` inside `foo()`, `bar()` defined in `Base` is *never* considered. Therefore, either you have an error, or another `bar()` (such as a global `bar()`) is called.

We discuss this issue in Section 13.4.2 on page 237 in detail. For the moment, as a rule of thumb, we recommend that you always qualify any symbol that is declared in a base that is somehow dependent on a template parameter with `this->` or `Base<T>::`.

# 5.4 Templates for Raw Arrays and String Literals

When passing raw arrays or string literals to templates, some care has to be taken. First, if the template parameters are declared as references, the arguments don’t decay. That is, a passed argument of `"hello"` has type `char const[6]`. This can become a problem if raw arrays or string arguments of different length are passed because the types differ. Only when passing the argument by value, the types decay, so that string literals are converted to type `char const*`. This is discussed in detail in Chapter 7.

Note that you can also provide templates that specifically deal with raw arrays or string literals. For example: [Click here to view code image](#)

```
```cpp
basics/lessarray.hpp

template<typename T,
         int N,
         int M> bool less (T(&a)[N], T(&b)[M])
{
    for (int i = 0; i<N && i<M; ++i)
    {
        if (a[i]<b[i]) return true; if (b[i]<a[i]) return false;
    }
    return N < M;
}
```
```