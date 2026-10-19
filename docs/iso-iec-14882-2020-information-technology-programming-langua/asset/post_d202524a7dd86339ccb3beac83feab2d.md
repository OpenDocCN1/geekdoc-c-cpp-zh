
# ISO/IEC 14882:2020(E)

```
template<class T, class A>
    shared_ptr<T> allocate_shared(const A& a, size_t N,
                                    const remove_extent_t<T>& u);    // T is U[]
```

Constraints: T is of the form U[].

Returns: A shared_ptr to an object of type U[N], where U is remove_extent_t<T> and each array element has an initial value of u.

```
[Example 4:
    shared_ptr<double[]> p = make_shared<double[]>(1024, 1.0);
    // shared_ptr to a double[1024], where each element is 1.0
    shared_ptr<double[] [2]> q = make_shared<double[] [2]>(6, {1.0, 0.0});
    // shared_ptr to a double[6] [2], where each double[2] element is {1.0, 0.0}
    shared_ptr<vector<int>[]> r = make_shared<vector<int>[]>(4, {1, 2});
    // shared_ptr to a vector<int>[4], where each vector has contents {1, 2}
    — end example]
```

```
template<class T>
    shared_ptr<T> make_shared(const remove_extent_t<T>& u);    // T is U[N]
template<class T, class A>
    shared_ptr<T> allocate_shared(const A& a,
                                  const remove_extent_t<T>& u);    // T is U[N]
```

Constraints: T is of the form U[N].

Returns: A shared_ptr to an object of type T, where each array element of type remove_extent_t<T> has an initial value of u.

```
[Example 5:
    shared_ptr<double[1024]> p = make_shared<double[1024]>(1.0);
    // shared_ptr to a double[1024], where each element is 1.0
    shared_ptr<double[6] [2]> q = make_shared<double[6] [2]>({1.0, 0.0});
    // shared_ptr to a double[6] [2], where each double[2] element is {1.0, 0.0}
    shared_ptr<vector<int>[4]> r = make_shared<vector<int>[4]>({1, 2});
    // shared_ptr to a vector<int>[4], where each vector has contents {1, 2}
    — end example]
```

```
template<class T>
    shared_ptr<T> make_shared_for_overwrite();
template<class T, class A>
    shared_ptr<T> allocate_shared_for_overwrite(const A& a);
```

Constraints: T is not an array of unknown bound.

Returns: A shared_ptr to an object of type T.

```
[Example 6:
    struct X { double data[1024]; };
    shared_ptr<X> p = make_shared_for_overwrite<X>();
    // shared_ptr to a default-initialized X, where each element in X::data has an indeterminate value
    shared_ptr<double[1024]> q = make_shared_for_overwrite<double[1024]>();
    // shared_ptr to a default-initialized double[1024], where each element has an indeterminate value
    — end example]
```

```
template<class T>
    shared_ptr<T> make_shared_for_overwrite(size_t N);
template<class T, class A>
    shared_ptr<T> allocate_shared_for_overwrite(const A& a, size_t N);
```

Constraints: T is an array of unknown bound.

Returns: A shared_ptr to an object of type U[N], where U is remove_extent_t<T>.

## 20.11.3.8 Comparison [util.smartptr.shared.cmp]

```
template<class T, class U>
    bool operator==(const shared_ptr<T>& a, const shared_ptr<U>& b) noexcept;
```

Returns: a.get() == b.get().

```
template<class T>
    bool operator==(const shared_ptr<T>& a, nullptr_t) noexcept;
```

Returns: !a.

```
template<class T, class U>
    strong_ordering operator<=>(const shared_ptr<T>& a, const shared_ptr<U>& b) noexcept;
```

Returns: compare_three_way()(a.get(), b.get()).

> [Note 1: Defining a comparison operator function allows shared_ptr objects to be used as keys in associative containers. — end note]

```
template<class T>
    strong_ordering operator<=>(const shared_ptr<T>& a, nullptr_t) noexcept;
```

Returns: compare_three_way()(a.get(), nullptr).

## 20.11.3.9 Specialized algorithms [util.smartptr.shared.spec]

```
template<class T>
    void swap(shared_ptr<T>& a, shared_ptr<T>& b) noexcept;
```

Effects: Equivalent to a.swap(b).

## 20.11.3.10 Casts [util.smartptr.shared.cast]

```
template<class T, class U>
    shared_ptr<T> static_pointer_cast(const shared_ptr<U>& r) noexcept;
template<class T, class U>
    shared_ptr<T> static_pointer_cast(shared_ptr<U>&& r) noexcept;
```

Mandates: The expression static_cast<T*>((U*)nullptr) is well-formed.

Returns:
    shared_ptr<T>(R, static_cast<typename shared_ptr<T>::element_type*>(r.get()))
where R is r for the first overload, and std::move(r) for the second.

> [Note 1: The seemingly equivalent expression shared_ptr<T>(static_cast<T*>(r.get())) will eventually result in undefined behavior, attempting to delete the same object twice. — end note]

```
template<class T, class U>
    shared_ptr<T> dynamic_pointer_cast(const shared_ptr<U>& r) noexcept;
template<class T, class U>
    shared_ptr<T> dynamic_pointer_cast(shared_ptr<U>&& r) noexcept;
```

Mandates: The expression dynamic_cast<T*>((U*)nullptr) is well-formed. The expression dynamic_cast<typename shared_ptr<T>::element_type*>(r.get()) is well-formed.

Preconditions: The expression dynamic_cast<typename shared_ptr<T>::element_type*>(r.get()) has well-defined behavior.

Returns:

- When dynamic_cast<typename shared_ptr<T>::element_type*>(r.get()) returns a non-null value p, shared_ptr<T>(R, p), where R is r for the first overload, and std::move(r) for the second.
- Otherwise, shared_ptr<T>().

[Example 7:
    shared_ptr<double[]> p = make_shared_for_overwrite<double[]>(1024);
    // shared_ptr to a default-initialized double[1024], where each element has an indeterminate value
— end example]

# ISO/IEC 14882:2020(E)

> [Note 2: The seemingly equivalent expression shared_ptr<T>(dynamic_cast<T*>(r.get())) will eventually result in undefined behavior, attempting to delete the same object twice. — end note]

```
template<class T, class U>
  shared_ptr<T> const_pointer_cast(const shared_ptr<U>& r) noexcept;
template<class T, class U>
  shared_ptr<T> const_pointer_cast(shared_ptr<U>&& r) noexcept;
```

Mandates: The expression const_cast<T*>((U*)nullptr) is well-formed.

Returns:

  shared_ptr<T>(R, const_cast<typename shared_ptr<T>::element_type*>(r.get()))

where R is r for the first overload, and std::move(r) for the second.

> [Note 3: The seemingly equivalent expression shared_ptr<T>(const_cast<T*>(r.get())) will eventually result in undefined behavior, attempting to delete the same object twice. — end note]

```
template<class T, class U>
  shared_ptr<T> reinterpret_pointer_cast(const shared_ptr<U>& r) noexcept;
template<class T, class U>
  shared_ptr<T> reinterpret_pointer_cast(shared_ptr<U>&& r) noexcept;
```

Mandates: The expression reinterpret_cast<T*>((U*)nullptr) is well-formed.

Returns:

  shared_ptr<T>(R, reinterpret_cast<typename shared_ptr<T>::element_type*>(r.get()))

where R is r for the first overload, and std::move(r) for the second.

> [Note 4: The seemingly equivalent expression shared_ptr<T>(reinterpret_cast<T*>(r.get())) will eventually result in undefined behavior, attempting to delete the same object twice. — end note]

## 20.11.3.11 get_deleter

[util.smartptr.getdeleter]

```
template<class D, class T>
  D* get_deleter(const shared_ptr<T>& p) noexcept;
```

Returns: If p owns a deleter d of type cv-unqualified D, returns addressof(d); otherwise returns nullptr. The returned pointer remains valid as long as there exists a shared_ptr instance that owns d.

> [Note 1: It is unspecified whether the pointer remains valid longer than that. This can happen if the implementation doesn't destroy the deleter until all weak_ptr instances that share ownership with p have been destroyed. — end note]

## 20.11.3.12 I/O

[util.smartptr.shared.io]

```
template<class E, class T, class Y>
  basic_ostream<E, T>& operator<<(basic_ostream<E, T>& os, const shared_ptr<Y>& p);
```

Effects: As if by: os << p.get();

Returns: os.

## 20.11.4 Class template weak_ptr

[util.smartptr.weak]

### 20.11.4.1 General

[util.smartptr.weak.general]

The weak_ptr class template stores a weak reference to an object that is already managed by a shared_ptr. To access the object, a weak_ptr can be converted to a shared_ptr using the member function lock.

```
namespace std {
  template<class T> class weak_ptr {
  public:
    using element_type = remove_extent_t<T>;

    // 20.11.4.2, constructors
    constexpr weak_ptr() noexcept;
    template<class Y>
      weak_ptr(const shared_ptr<Y>& r) noexcept;
    weak_ptr(const weak_ptr& r) noexcept;
```
