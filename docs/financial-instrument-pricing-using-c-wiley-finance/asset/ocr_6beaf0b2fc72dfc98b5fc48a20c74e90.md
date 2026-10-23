+   Avoid the inherent cost of creating a new object in the standard way (e.g. using the 'new' keyword) when it is prohibitively expensive to do so.

Again, we can use std::enable_if to achieve the same results. We take an example from both Boost and C++ to create objects depending on a given data type:

```
// A. Boost version
template <typename T>
    typename boost::enable_if <std::is_same<T, int>, T>::type create()
{
    return 1;
}

template <typename T>
    typename boost::enable_if <std::is_same<T, std::string>,
T>::type create()
{
    return "A string is born";
}
```

```
// B. C++ version
template <typename T>
    typename std::enable_if <std::is_same<T, double>::value,
T>::type create()
{
    return 2.71;
}
```

```
struct C
{
    C() { }
    friend std::ostream& operator << (std::ostream& os,const C& c)
        { os << "A new C";  return os; }
};
```

```
template <typename T>
    typename std::enable_if <std::is_same<T, C>::value, T>::type create()
{
    return C();
}
```

An example of use is:

```
std::cout << create<std::string>() << '\n';
std::cout << create<double>() << '\n';
std::cout << create<C>() << '\n';
C myC = std::move(create<C>());
std::cout << myC << '\n';
```