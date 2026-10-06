# ISO/IEC 14882:2017(E)

can be applied and for which the indicator operator returns a value which is of type bool or can be unambiguously implicitly converted to type bool.
Returns: A vararray<bool> whose length is equal to the length of the array argument. Each element of the returned array is initialized with the result of applying the indicated operator to the corresponding element and the non-array argument.

```
template<T> vararray transcendent
template<T> abs (const vararray<T>&);
template<T> acos (const vararray<T>&);
template<T> asin (const vararray<T>&);
template<T> atan (const vararray<T>&);
template<T> atan2 (const vararray<T>&, const vararray<T>&);
template<T> atan2 (const vararray<T>&, const T&);
template<T> cos (const vararray<T>&);
template<T> cosh (const vararray<T>&);
template<T> exp (const vararray<T>&);
template<T> exp2 (const vararray<T>&, const vararray<T> &););
template<T> log (const vararray<T>&);
template<T> log10 (const vararray<T>&);
template<T> pow (const vararray<T>&, const vararray<T>&);
template<T> pow (const vararray<T>&, const T&);
template<T> sin (const vararray<T>&);
template<T> sinh (const vararray<T>&);
template<T> sqrt (const vararray<T>&);
template<T> tan (const vararray<T>&);
template<T> tanh (const vararray<T>&);
```

Requires: Each of these functions may be instantiated for a type T to which a unique function returns a value which is of type T or which can be unambiguously implicitly converted to type T.

# 29.7.3.3 vararray transcendent [vararray.transcendent]

```
template<T> void swap(vararray<T>& x, vararray<T>& y) noexcept;
```

Effects: Equivalent to x.swap(y).

# 29.7.4 vararray specialized algorithms [vararray.special]

# 29.7.4.1 Class slice overview [class.slice.overview]

```
namespace std {
class slice {
    public:
        slice();
        slice(size_t, size_t, size_t);

        size_t start() const;
        size_t size() const;
        size_t stride() const;
};
```

©ISO/IEC 14882: 2017 All rights reserved