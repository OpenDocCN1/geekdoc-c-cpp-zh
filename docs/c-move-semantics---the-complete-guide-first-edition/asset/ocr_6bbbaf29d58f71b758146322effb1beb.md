# 15.3.1 Move Semantics for Pairs

std::pair<> is a good example of both the benefits of move semantics and the complexity it might introduce. In principle, we have only a generic data structure with two members (defined in namespace std):

```
template<typename T1, typename T2>
struct pair {
    T1 first;
    T2 second;
    ...
};
```

However, to support move semantics (and a couple of other tricky corner cases, such as reference members), we have the following declaration here. I show the C++14 version, which I made a bit more readable):

```
template<typename T1, typename T2>
struct pair {
    // types of each member:
    using first_type = T1;       // same as: typedef T1 first_type
    using second_type = T2;
    // the members:
    T1 first;
    T2 second;

    // constructors:
    constexpr pair();
    constexpr pair(const T1& x, const T2& y);
    template<typename U, typename V> constexpr pair(U&& x, V&& y);
    pair(const pair&) = default;
    pair(pair&&) = default;
    template<typename U, typename V> constexpr pair(const pair<U, V>& p);
    template<typename U, typename V> pair& operator=(const pair<U, V>& p);
    template<typename... Args1, typename... Args2>
      pair(piecewise_construct_t, tuple<Args1...> first_args,
           tuple<Args2...> second_args);

    // assignments:
    pair& operator=(const pair& p);
    pair& operator=(pair&& p) noexcept(...);
    template<typename U, typename V> pair& operator=(const pair<U, V>& p);
    template<typename U, typename V> pair& operator=(pair<U, V>&& p);

    // other:
    void swap(pair& p) noexcept(...);
};
```