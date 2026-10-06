# ISO/IEC 14882:2017(E)

```
template<class T valarray<T>> operator-(const valarray<T>&, const T&);
template<class T valarray<T>> operator-(const T&, const valarray<T>&);
template<class T valarray<T>> operator=(const valarray<T>&, const T&);
template<class T valarray<T>> operator*(const valarray<T>&, const T&);
template<class T valarray<T>> operator*(const T&, const valarray<T>&);
template<class T valarray<T>> operator=(const valarray<T>&, const T&);
template<class T valarray<T>> operator|(const T&, const valarray<T>&);
template<class T valarray<T>> operator<(const valarray<T>&, const T&);
template<class T valarray<T>> operator/=(const valarray<T>&, const T&);
template<class T valarray<T>> operator/=(const T&, const valarray<T>&);
```

+   3 Each of these may only be instantiated for a type T which the indicated operator can be applied and for which the indicated operator returns a value which is of type T or can be unambiguously implicitly converted to type T.

+   4 Returns a valarray whose length is equal to the length of the array argument. Each element of the returned array is initialized with the result of applying the indicated operator to the corresponding element of the array and the non-array argument.

# 29.7.3.2 valarray logical operators [comparison]

```
template<class T valarray<bool>> operator==(const valarray<T>&, const T&);
template<class T valarray<bool>> operator=(const T&, const valarray<T>&);
template<class T valarray<bool>> operator<(const valarray<T>&, const T&);
template<class T valarray<bool>> operator>(const T&, const valarray<T>&);
template<class T valarray<bool>> operator<=(const valarray<T>&, const T&);
template<class T valarray<bool>> operator>=(const T&, const valarray<T>&);
template<class T valarray<bool>> operator&&(const valarray<T>&, const T&);
template<class T valarray<bool>> operator||(const valarray<T>&, const T&);
```

Each of these may only be instantiated for a type T to which the indicated operator returns a value which is of type bool or can be unambiguously implicitly converted to type bool. Both array arguments have the same length.

+   2 Returns a valarray whose length is equal to the length of the array argument. Each element of the returned array is initialized with the result of applying the indicated operator to the corresponding elements of the array.

```
template<class T valarray<bool>> operator==(const valarray<T>&, const T&);
template<class T valarray<bool>> operator=(const T&, const valarray<T>&);
template<class T valarray<bool>> operator<(const valarray<T>&, const T&);
template<class T valarray<bool>> operator>(const T&, const valarray<T>&);
template<class T valarray<bool>> operator<=(const valarray<T>&, const T&);
template<class T valarray<bool>> operator>=(const T&, const valarray<T>&);
template<class T valarray<bool>> operator*=(const valarray<T>&, const T&);
template<class T valarray<bool>> operator/=(const T&, const valarray<T>&);
template<class T valarray<bool>> operator<=(const valarray<T>&, const T&);
template<class T valarray<bool>> operator/=(const T&, const valarray<T>&);
template<class T valarray<bool>> operator&&=(const valarray<T>&, const T&);
template<class T valarray<bool>> operator&&=(const T&, const valarray<T>&);
template<class T valarray<bool>> operator||=(const valarray<T>&, const T&);
template<class T valarray<bool>> operator||=(const T&, const valarray<T>&);
```

+   3 Each of these may only be instantiated for a type T to which the indicated operator

§ 29.7.3.2 ©ISO/IEC 14882:2017 – All rights reserved 1113

* Nie