To get the best of both worlds, we can build an **array** container that provides the benefits of arrays without the weaknesses. The **array** is now part of the standard defined in `<array>`, but let’s see how we might define it. The idea is simple and useful:

```
```
template <typename T, int N>
// requires Element<T>()
struct array {
// not quite the standard array
    using value_type = T;
    using iterator = T*;
    using const_iterator = const T*;
    using size_type = unsigned int;
// the type of a subscript
    T elems[N];
// no explicit construct/copy/destroy needed
    iterator begin() { return elems; }
    const_iterator begin() const { return elems; }
    iterator end() { return elems+N; }
    const_iterator end() const { return elems+N; }
    size_type size() const;
    T& operator[](int n) { return elems[n]; }
    const T& operator[](int n) const { return elems[n]; }
    const T& at(int n) const;
// range-checked access
    T& at(int n);
// range-checked access
    T * data() { return elems; }
    const T * data() const { return elems; }
};
```
```

This definition isn’t complete or completely standards-conforming, but it will give you the idea. It will also give you something to use if your implementation doesn’t yet provide the standard **array**. If available, it is in `<array>`. Note that because **array<T,N>** “knows” that its size is N, we can (and do) provide assignment, `==`, `!=`, etc., just as for **vector**.
As an example, let’s use an array with the STL version of **high()** from §20.4.2:

```
```
void f()
{
    array<double,6> a = { 0.0, 1.1, 2.2, 3.3, 4.4, 5.5 };
    array<double,6>::iterator p = high(a.begin(), a.end());
```
```