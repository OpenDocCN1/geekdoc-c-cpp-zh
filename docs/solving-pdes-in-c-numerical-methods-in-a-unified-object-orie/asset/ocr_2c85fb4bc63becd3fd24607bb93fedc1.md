```
template<class T>
const difference<T>&
difference<T>::operator+=(const difference<T>&d) {
    for(int i=0; i<number; i++)
        *item[i] += d[i];
    return *this;
} // adding another "difference" to the current one
```

```
template<class T>
const difference<T>&
difference<T>::operator-=(const difference<T>&d) {
    for(int i=0; i<number; i++)
        *item[i] -= d[i];
    return *this;
} // subtracting a "difference" from the current one
```

So far, we have implemented addition and subtraction of another difference operator to or from the current one. Next, we define multiplication by a scalar:

```
template<class T>
const difference<T>&
difference<T>::operator*=(const T&t) {
    for(int i=0; i<size(); i++)
        *item[i] *= t;
    return *this;
} // multiplying the current "difference" by a scalar T
```

Next, we implement the above arithmetic operations as (nonmember) binary operators:

```
template<class T>
const difference<T>
operator+(const difference<T>&d1,
    const difference<T>&d2) {
    return difference<T>(d1) += d2;
} // adding two "difference" objects
```

```
template<class T>
const difference<T>
operator-(const difference<T>&d1,
    const difference<T>&d2) {
    return difference<T>(d1) -= d2;
} // subtracting two "difference" objects
```

```
template<class T>
const difference<T>
operator*(const T&t, const difference<T>&d) {
    return difference<T>(d) *= t;
} // scalar times "difference"
```