
```cpp
template<class T> valarray<T>operator+=(const valarray<T>&);

template<class T> valarray<T>operator+=(const typename valarray<T>::value_type&);

template<class T> valarray<T>operator+(const typename valarray<T>::value_type&);

template<class T> valarray<T>operator+=(const valarray_type&);

template<class T> valarray<T>operator+=(const typename valarray<T>::value_type&);

template<class T> valarray<T>operator-(const valarray<T>&, const valarray<T>&);

template<class T> valarray<T>operator-=(const valarray<T>&);

template<class T> valarray<T>operator-=(const typename valarray<T>::value_type&);
```

```cpp
template<class T> valarray<T> operator=(const valarray<T>&, const valarray<T>&);

template<class T> valarray<T> operator=(const valarray<T>&);

template<class T> valarray<T> operator=(const typename valarray<T>::value_type);

template<class T> valarray<T> operator&(const valarray<T>&, const valarray<T>&);

template<class T> valarray<T> operator&(const valarray<T>&);

template<class T> valarray<T> operator&(const typename valarray<T>::value_type);

template<class T> valarray<T> operator|((const valarray<T>&, const valarray<T>&);

template<class T> valarray<T> operator|(const valarray<T>&);

template<class T> valarray<T> operator|(const typename valarray<T>::value_type);

template<class T> valarray<T> operator<<=(const valarray<T>&, const valarray<T>&);

template<class T> valarray<T> operator<<=(const valarray<T>&);

template<class T> valarray<T> operator<<=(const typename valarray<T>::value_type);

template<class T> valarray<T> operator>>=(const valarray<T>&, const valarray<T>&);

template<class T> valarray<T> operator>>=(const valarray<T>&);

template<class T> valarray<T> operator>>=(const typename valarray<T>::value_type);

template<class T> valarray<T> operator&&(const valarray<T>&, const valarray<T>&);

template<class T> valarray<T> operator&&(const valarray<T>&);

template<class T> valarray<T> operator&&(const typename valarray<T>::value_type);

template<class T> valarray<T> operator||(const valarray<T>&, const valarray<T>&);

template<class T> valarray<T> operator||(const valarray<T>&);

template<class T> valarray<T> operator||(const typename valarray<T>::value_type);

template<class T> valarray<T> operator===(const valarray<T>&, const valarray<T>&);

template<class T> valarray<T> operator===(const valarray<T>&);

template<class T> valarray<T> operator===(const typename valarray<T>::value_type);

template<class T> valarray<T> operator!==(const valarray<T>&, const valarray<T>&);

template<class T> valarray<T> operator!==(const valarray<T>&);

template<class T> valarray<T> operator!==(const typename valarray<T>::value_type);

template<class T> valarray<T> operator<=(const valarray<T>&, const valarray<T>&);

template<class T> valarray<T> operator<=(const valarray<T>&);

template<class T> valarray<T> operator<=(const typename valarray<T>::value_type);

template<class T> valarray<T> operator>=(const valarray<T>&, const valarray<T>&);

template<class T> valarray<T> operator>=(const valarray<T>&);

template<class T> valarray<T> operator>=(const typename valarray<T>::value_type);

template<class T> valarray<bool> operator>(const valarray<T>&, const valarray<T>&);

template<class T> valarray<bool> operator>(const valarray<T>&);

template<class T> valarray<bool> operator>(const typename valarray<T>::value_type);

template<class T> valarray<bool> operator<(const valarray<T>&, const valarray<T>&);

template<class T> valarray<bool> operator<(const valarray<T>&);

template<class T> valarray<bool> operator<(const typename valarray<T>::value_type);
```

```cpp
template<class T> valarray<bool> operator<=(const typename valarray<T>::value_type);

template<class T> valarray<bool> operator>=(const typename valarray<T>::value_type);

const valarray<T>;

template<class T> valarray<bool> operator>(const valarray<T>&);

template<class T> valarray<bool> operator>(const typename valarray<T>::value_type);

const valarray<T>;

template<class T> valarray<bool> operator>(const typename valarray<T>::value_type);

const valarray<T>;
```

```cpp
template<class T> valarray<T> abs (const valarray<T>&);

template<class T> valarray<T> acos (const valarray<T>&);

template<class T> valarray<T> asin (const valarray<T>&);

template<class T> valarray<T> atan (const valarray<T>&);
```

```cpp
template<class T> valarray<T> atan2 (const valarray<T>&, const valarray<T>&);

template<class T> valarray<T> atan2 (const typename valarray<T>::value_type);

template<class T> valarray<T> atan (const typename valarray<T>::value_type);

const valarray<T>;
```

```cpp
template<class T> valarray<T> cos (const valarray<T>&);

template<class T> valarray<T> cosh (const valarray<T>&);

template<class T> valarray<T> exp (const valarray<T>&);

template<class T> valarray<T> log (const valarray<T>&);
```

```cpp
template<class T> valarray<T> log10 (const valarray<T>&);

template<class T> valarray<T> pow(const valarray<T>&, const valarray<T>&);

template<class T> valarray<T> pow(const typename valarray<T>::value_type, const valarray<T>&);
```

```cpp
template<class T> valarray<T> sin (const valarray<T>&);

template<class T> valarray<T> sqrt (const valarray<T>&);

template<class T> valarray<T> tan (const valarray<T>&);

template<class T> valarray<T> tanh (const valarray<T>&);
```

```cpp
template<class T> begin(const valarray<T>& v);

template<class T> begin(const valarray<T>& v);

template<class T> end(const valarray<T>& v);

}
```

1 头文件 `<valarray>` 定义了五个类 `{slice_array, gslice_array, mask_array, 和 indirect_array}`以及一组用于表示和处理数组的函数模板。

2 `valarray` 类被定义为不包含某些别名，从而允许对这些操作进行优化。

3 任何返回 `valarray<T>` 的函数都允许返回另一种对象，只要 `valarray<T>` 的所有 `const` 成员函数都适用于该类型。该函数类型的模板嵌套深度对于最深层参数不应超过两层。

4 使用此类替换类型的实现提供了额外的函数和运算符，如下：

- (4.1) 对于每个接受 `const valarray<T>&` 的函数（除 `end (26.7.10)` 之外），应添加接受替换类型的相同函数；
- (4.2) 对于每个接受两个 `const valarray<T>&` 的函数，应添加接受 `const valarray<T>&` 和替换类型的所有组合的函数。

> 254 附录 B 建议了最小模板实例数量。这间接暗示了 varlay 表达式的最小允许复杂度。

# ISO/IEC 14882:2020(E)

5 特别地，实现应允许从此类替换类型构造 `vararray<T>`，并允许将此类类型赋值 `valarray<T>`、`slice_array<T>`、`gslice_array<T>`、`mask_array<T>` 和 `indirect_array<T>` 对象进行复合赋值。

6 如果没有足够的资源执行操作，这些库允许抛出 `bad_alloc` (17.6.4.1) 异常。注意，该异常并非强制。

## 26.7.2 类 vararray [template.vararray]

### 26.7.2.1 概述 [template.vararray.overview]

```cpp
namespace std {

template<T> class vararray {

public:

    using value_type = T;

    // 26.7.2.2, 构造/析构

    vararray(size_t);

    vararray(const T&, size_t);

    vararray(const T&, size_t);

    vararray(const vararray&&) noexcept;

    vararray(const slice_array<T>&);

    vararray(const gslice_array<T>&);

    vararray(const mask_array<T>&);

    vararray(const indirect_array<T>&);

    vararray(initializer_list<T>);

    ~vararray();

    // 26.7.2.3, 赋值

    vararray&operator=(const vararray&);

    vararray&operator=(const vararray&&) noexcept;

    vararray&operator=(initializer_list<T>&);

    vararray&operator=(const T&);

    vararray&operator=(const slice_array<T>&);

    vararray&operator=(const gslice_array<T>&);

    vararray&operator=(const mask_array<T>&);

    vararray&operator=(const indirect_array<T>&);

    // 26.7.2.4, 元素访问

    const T& operator[](size_t);

    T& operator[](size_t);

    // 26.7.2.5, 子集操作

    vararray operator[](slice) const;

    vararray operator[](slice) const;

    vararray operator[](const gslice_array<T>&) const;

    vararray operator[](const gslice<T>&) const;

    vararray operator[](const bool&) const;

    vararray operator[](const bool&&) const;

    vararray operator[](const slice_array<size_t>&) const;

    vararray operator[](const vararray<size_t>&) const;

    // 26.7.2.6, 一元运算符

    vararray operator++() const;

    vararray operator--() const;

    vararray operator-() const;

    vararray operator!() const;

    // 26.7.2.7, 复合赋值

    vararray& operator+=(const T&);

    vararray& operator/=(const T&);

    vararray& operator*=(const T&);

    vararray& operator++=(const T&);
```
