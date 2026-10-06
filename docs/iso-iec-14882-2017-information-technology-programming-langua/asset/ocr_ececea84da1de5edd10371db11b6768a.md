# ISO/IEC 14882:2017(E)

10 For every promoted arithmetic type *T*, there exist candidate operator functions of the form

```
operator+=(T);
operator-(T);
```

11. For every promoted integral type *T*, there exist candidate operator functions of the form

```
operator-(T);
```

12 For every quintuple *C1, C2, T, cv1, cv2*, where *C2* is a class type, *C1* is the same type as *C2* or a derived class of *C2*, and *T* is an object type or a function type, there exist candidate operator functions of the form

```
cv2 T*->(cv1 C1*, C2 T::);
```

*cv2* is the result of *cv1* and *cv2*. The return type is shown for exposition only; see 8.5 for the determination of the operator's result.

13 For every promoted arithmetic types *L* and *R*, there exist candidate operator functions of the form

```
operator*(L, R);
operator/(L, R);
operator+(L, R);
```

```
operator<(L, R);
operator<=(L, R);
operator>=(L, R);
operator===(L, R);
operator=(L, R);
```

where *LR* is the result of the usual arithmetic conversions between *L* and *R*

14 For every cv-qualified or un-qualified object type *T* there exist candidate operator functions of the form

```
operator*(T*, std::ptrdiff_t);
operator/(T*, std::ptrdiff_t);
operator-(T*, std::ptrdiff_t);
operator+*(T*, std::ptrdiff_t, T*);
```

15 For *T*, where *T* is an enumeration type or a pointer type, there exist candidate operator functions of the form

```
std::ptrdiff_t operator-(T, T);
```

16 For *T*, where *T* is an enumeration type or a pointer type, there exist candidate operator functions of the form

```
operator<(T, T);
operator>(T, T);
operator<=(T, T);
operator>=(T, T);
operator===(T, T);
operator!=(T, T);
```

17 For pointer member type *T* or type *std::nullptr_t* there exist candidate operator functions of the form

```
operator==(T, T);
operator!=(T, T);
```

18 For pair of promoted integral types *L* and *R*, there exist candidate operator functions of the form

```
operator%(L, R);
operator&=(L, R);
operator*=(L, R);
```

§ 16.6

©ISO/IEC 2017 – All rights reserved