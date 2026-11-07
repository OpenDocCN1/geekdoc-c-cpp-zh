# ### min()

```
```cpp
template<class T> const T& min(const T& a, const T& b);

template<class T, class Compare>
const T& min(const T& a, const T& b, Compare comp);
```
```

These versions of the min() function return the lesser of two values. If the two values are equivalent, they return the first value. The first version uses < to determine the ordering, and the second version uses the comp comparison object.

```
```cpp
template<class T> T min(initializer_list<T> t);

template<class T, class Compare>
T min(initializer_list<T> t, Compare comp);
```
```

These versions of min() function (C++11) return the smallest value in the initializer list t. If the two or more values are equivalent, they return a copy of the first-occurring item having that value. The first version uses < to determine the ordering, and the second version uses the comp comparison object.

# ### max()

```
```cpp
template<class T> const T& max(const T& a, const T& b);

template<class T, class Compare>
const T& max(const T& a, const T& b, Compare comp);
```
```

These versions of the max() function return the greater of two values. If the two values are equivalent, they return the first value. The first version uses < to determine the ordering, and the second version uses the comp comparison object.

```
```cpp
template<class T> T max(initializer_list<T> t);

template<class T, class Compare>
T max(initializer_list<T> t, Compare comp);
```
```

These versions of max() function (C++11) return the largest value in the initializer list t. If the two or more values are equivalent, they return a copy of the first-occurring item having that value. The first version uses < to determine the ordering, and the second version uses the comp comparison object.

# ### minmax() (C++11)

```
```cpp
template<class T>
    pair<const T&,const T&> minmax(const T& a, const T& b);

template<class T, class Compare>
    pair<const T&,const T&> minmax(const T& a, const T& b,
                                   Compare comp);
```
```