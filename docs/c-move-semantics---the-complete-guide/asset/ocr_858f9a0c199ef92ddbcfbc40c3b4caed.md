Note that you have to declare/define full specializations of member function templates outside the class definition:

```
template<typename T>
class Cont {
    ...
    // primary template:
    template<typename U>
    void insert(U&& v) {  // universal reference
        coll.push_back(std::forward<U>(v));
    }
    ...
};
```

// full specializations for Cont<T>::insert<>():
// - have to be outside the class
// - need specializations for rvalues and lvalues

```
template<>
template<>
void Cont<std::string>::insert<>(std::string&& v)
{
    coll.push_back(std::move(v));
}
```

```
template<>
template<>
void Cont<std::string>::insert<>(const std::string& v)
{
    coll.push_back(v);
}
```

# 10.3 How the Standard Specifies Perfect Forwarding

To finally understand all rules of perfect forwarding, let us see how the rules are formally specified in the C++ standard.

Again, consider you have the following declaration:

```
template<typename T>
void f(T&& arg)          // arg is universal/forwarding reference
{
    g(std::forward<T>(arg));  // perfectly forward (move() only for passed rvalues)
}
```

Normally, T would just have the type of the passed argument:

```
MyType v;
```