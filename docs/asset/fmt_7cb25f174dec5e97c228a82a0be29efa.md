
返回：一个持有指向由 `indarr` 选择的控制序列元素引用对象。[示例]:

```cpp
valarray<char> v0("abcdefghijklmnop", 16);

valarray<char> v1("ABCDE", 5);

const size_t vi[] = {7, 5, 2, 3, 8};

v0[vi] = v1;

// v0 == valarray<char>("AbCBAEjghijklmnop", 16)
```

## 26.6.2.6 valarray 一元操作符 [valarray.unary.]

```cpp
valarray<T> operator+() const;
valarray<T> operator-() const;
valarray<T> operator~() const;
valarray<bool> operator!() const;
```

这些操作符中的每一个仅适用于类型 `T`，且该指示操作符返回类型为 `T` (`bool operator!`) 或可以转换为类型 `T` (`bool operator!`)。这些操作符中的每一个都返回一个与数组长度相同的数组。返回数组的每个元素都通过将指示操作符应用于对应元素来初始化。

## 26.6.2.7 valarray 计算赋值 [valarray.cassign]

```cpp
valarray<T> operator+=(const valarray<T>);
valarray<T> operator/=(const valarray<T>);
valarray<T> operator*=(const valarray<T>);
valarray<T> operator+=(const valarray<T>);
valarray<T> operator-==(const valarray<T>);
valarray<T> operator<=(const valarray<T>);
valarray<T> operator>=(const valarray<T>);
valarray<T> operator|==(const valarray<T>);
valarray<T> operator<<=(const valarray<T>);
valarray<T> operator>>=(const valarray<T>);
```

1. 这些操作符中的每一个仅适用于指示操作符可以应用的类型 `T`。这些操作符中的每一个都对其自身的元素和参数的对应元素执行指示操作。
2. 数组通过引用返回。
3. 如果数组和参数的长度不同，则其行为是未定义的。计算赋值左侧出现数组不会使引用或指针。
4. 如果 `valarray` 计算赋值左侧元素的值取决于该左侧另一个元素的值，则结果行为是未定义的。

```cpp
valarray<T> operator+=(const T);
valarray<T> operator/=(const T);
valarray<T> operator*=(const T);
valarray<T> operator+=(const T);
valarray<T> operator-==(const T);
valarray<T> operator<=(const T);
valarray<T> operator>=(const T);
valarray<T> operator|==(const T);
valarray<T> operator<<=(const T);
valarray<T> operator>>=(const T);
```

5. 这些操作符中的每一个仅适用于指示操作符可以应用的类型 `T`。
6. 这些操作符中的每一个都对数组的每个元素和非数组参数应用指示操作。

## 26.6.2.8 valarray 成员函数 [valarray.members]

```cpp
void swap(valarray<T>&) noexcept;
```

1. `*this` 获取 `v` 的值。`v` 获取 `*this` 的值。
2. 复杂度：常数级级。

```cpp
size_t size() const;
```

3. 返回：数组中元素的个数。
4. 复杂度：常数时间。

```cpp
T sum() const;
```

此函数仅可以对一个可以应用 `operator++` 的类型 `T` 进行实例化。此函数返回数组中所有元素的和。

5. 如果数组长度为 0，则行为是未定义的。如果数组长度为 1，`sum()` 返回元素 0 的值。否则，返回的值通过对数组的拷贝以及数组中的所有其他元素以不指定的顺序应用 `operator+=` 计算得出。

```cpp
T min() const;
```

6. 此函数返回 `*this` 中包含的最小值。对于长度为 0 的数组，返回的值未定义。对于长度为 1 的数组，返回元素 0。对于所有其他长度的数组，使用 `operator<` 进行确定。

```cpp
vararray<T> shift(int n) const;
```

7. 此函数返回一个长度为 `size()` 的 `vararray<T>` 类对象，其元素 `$i$` 在 `$i$` 为非负且小于 `size()` 时为 `*this[i + n]`，否则为 `T()`。因此，如果将该元素视为最左侧的元素，正值 `$n$` 将元素移动 `$n$` 位，并用零填充。

> [示例：如果参数值为 -2，结果的前两个元素将进行值初始化 (8.5)：结果的第三个元素将被赋值数组第一个元素的值；等等。--示例结束]

```cpp
vararray<T> shift() const;
```

8. 此函数返回一个长度为 `size()` 的 `vararray<>` 类对象，该对象是 `*this` 的循环移动。如果将元素视为最左侧的元素，非负值 `$n$` 将元素循环移动 `-$n$` 位，而负值 `$n$` 将将元素循环移动 `$n$` 位。

```cpp
vararray<T> apply(T func(T)) const;
vararray<T> apply(T func(const T&)) const;
```

9. 此函数返回一个长度等于原数组的数组。返回数组的每个元素都是通过将参数函数应用于数组的对应元素而获得的值。

```cpp
void resize(size_t sz, T c = T());
```

此成员函数更改 `*this` 数组 的长度为 `sz`，然后为每个元素分配第二个参数的值。调整大小会初始化指向数组中元素的指针和引用。

§ 26.6.2.8 990

## vararray 非成员操作

## 26.6.3 vararray 二元运算符

```cpp
template<class T> vararray<T> operator*(const vararray<T>&, const vararray<T>&);
template<class T> vararray<T> operator/(const vararray<T>&, const vararray<T>&);
template<class T> vararray<T> operator%(const vararray<T>&, const vararray<T>&);
template<class T> vararray<T> operator+=(const vararray<T>&, const vararray<T>&);
template<class T> vararray<T> operator-=(const vararray<T>&, const vararray<T>&);
template<class T> vararray<T> operator*(const vararray<T>&, const vararray<T>&);
template<class T> vararray<T> operator/(const vararray<T>&, const vararray<T>&);
template<class T> vararray<T> operator<<(const vararray<T>&, const vararray<T>&);
template<class T> vararray<T> operator>>(const vararray<T>&, const vararray<T>&);
```

1. 这些运算符中的每一个都只能对一个类型 `T` 进行实例化，其中指示的返回返回的值类型为 `T`，或者可以无歧义地隐式转换为类型 `T`。
2. 这些运算符中的每一个都返回一个长度等于参数数组长度的数组。返回数组的每个元素通过将指示运算符应用于参数数组的对应元素的结果来初始化。
3. 如果参数长度不相同，则行为是未定义的。

```cpp
template<class T> vararray<T> operator*(const vararray<T>&, const T&);
template<class T> vararray<T> operator/=(const vararray<T>&, const T&);
template<class T> vararray<T> operator*=(const vararray<T>&, const vararray<T>&);
template<class T> vararray<T> operator%=(const vararray<T>&, const vararray<T>&);
template<class T> vararray<T> operator+=(const vararray<T>&, const T&);
template<class T> vararray<T> operator-=(const vararray<T>&, const T&);
template<class T> vararray<T> operator*=(const vararray<T>&, const T&);
template<class T> vararray<T> operator/=(const vararray<T>&, const T&);
template<class T> vararray<T> operator+=(const vararray<T>&, const T&);
template<class T> vararray<T> operator-=(const vararray<T>&, const T&);
template<class T> vararray<T> operator<<=(const vararray<T>&, const T&);
template<class T> vararray<T> operator>>=(const vararray<T>&, const T&);
template<class T> vararray<T> operator>>=(const vararray<T>&, const T&);
```

4. 这些运算符中的每一个都只能对一个类型 `T` 进行实例化，其中指示的运算符返回的值类型为 `T`，或者可以无歧义地隐式转换为类型 `T`。

这些运算符中的每一个都返回一个长度等于数组参数长度的数组。返回数组的元素通过将指示的运算符应用于数组的对应元素和非数组参数的结果来初始化。

## 26.6.3.2 varray 逻辑运算符 [varray.comparison]

```cpp
template<class T> varray operator==(const varray<T>&, const varray<T>&);
template<class T> varray operator!=(const varray<T>&, const varray<T>&);
template<class T> varray operator<(const varray<T>&, const varray<T>&);
template<class T> varray operator>(const varray<T>&, const varray<T>&);
template<class T> varray operator<=(const varray<T>&, const varray<T>&);
template<class T> varray operator>=(const varray<T>&, const varray<T>&);
template<class T> varray operator<<(const varray<T>&, const varray<T>&);
template<class T> varray operator>>(const varray<T>&, const varray<T>&);
template<class T> varray operator||(const varray<T>&, const varray<T>&);
```

这些运算符中的每一个都只能对一个类型 `T` 进行实例化，其中指示的运算符可以应用，且返回类型为 `bool` 的值。

这些运算符中的每一个都返回一个长度等于数组长度的数组。返回数组的元素通过将指示的运算符应用于数组的对应元素来初始化。如果两个数组长度相同，行为是定义的。

§ 26.6.3.2 992

## 26.6.3.3 vararray 超越函数 [vararray.transcend]

```cpp
template<class T> vararray abs(const vararray<T>);
template<class T> vararray acos(const vararray<T>);
template<class T> vararray asin(const vararray<T>);
template<class T> vararray atan(const vararray<T>);
template<class T> vararray atand(const vararray<T>&, const T&);
template<class T> vararray at2(const vararray<T>&, const T&);
template<class T> vararray cos(const vararray<T>);
template<class T> vararray exp(const vararray<T>);
template<class T> vararray log(const vararray<T>);
template<class T> vararray log10(const vararray<T>);
template<class T> vararray pow(const vararray<T>&, const vararray<T>&);
```

这些函数只能对一个可以应用唯一函数（无限定）的类型 `T` 进行实例化。此函数应返回类型 `T` 或可以转换为类型 `T`。

## 26.6.3.4 vararray 特殊化算法

```cpp
template<class T> void swap(vararray<T>& x, vararray<T>& y) noexcept;
```

影响：`x.swap(y)`。

## 26.6.4 slice 类 [class.slice]

## 26.6.4.1 slice 类概述 [class.slice.overview]

```cpp
namespace std {
class slice {
public:
    slice(size_t, size_t, size_t);
    size_t start() const;
    size_t size() const;
    size_t stride() const;
};
}
```

`slice` 表示数组中的一个 BLAS 切片。此类切片由起始索引、长度和步长指定。^{288}

## 26.6.4.2 slice 构造函数 [class.slice]

288 BLAS 代表基本代数子程序。C++ 程序可以实例化此类。请参 Dongarra, Duço, Duff 和 Hamling：A set of Level 3 Basic Linear Algebra Subprograms，Technical Report MCS-P1-0888, Argonne National Laboratory (USA); Mathematics and Computer Science Division, August, 1988.

```cpp
slice();
slice(size_t start, size_t length, size_t stride);
slice(const slice&);
```

默认构造函数等同于 `slice(0, 0, 0)`。提供默认构造函数仅用于允许声明 `slice` 数组。带参数的构造函数接收起始位置、长度和步长。

> [示例：`slice(3, 8, 2)` 构造了一个 `slice`，它从数组中选择元素 3, 5, 7, ... 17。-- 示例]

## 26.6.4.3 slice 访问函数 [slice.access]

```cpp
size_t start() const;
size_t size() const;
size_t stride() const;
```

返回：`slice` 对象指定的起始位置、长度或步长。复杂度：常数时间。

## 26.6.5 类模板 slice_array [template.slice.array]

## 26.6.5.1 类模板 slice_array 概述 [template.slice_array.overview]

```cpp
namespace std {
template <class T> class slice_array {
public:
```

# ©ISO/IEC N4296

# ISO/IEC
# N4296
