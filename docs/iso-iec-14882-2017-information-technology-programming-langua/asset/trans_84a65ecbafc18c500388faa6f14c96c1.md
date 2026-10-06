

# ISO/IEC 14882:2017(E)

影响：这些操作符中的每一个对 *this* 的每个元素以及 *v* 对应的元素执行指示的操作。

返回值：*this*。

备注：在复合赋值的左侧出现数组会导致引用或指针失效。

```
vararrayoperator**=(const T& v);
vararrayoperator/=(const T& v);
vararrayoperator*=(const T& v);
vararrayoperator++=(const T& v);
vararrayoperator-=(const T& v);
vararrayoperator*=(const T& v);
vararrayoperator*+=(const T& v);
vararrayoperator<<=(const T& v);
vararrayoperator>>=(const T& v);
```

要求：只有当指示的操作符可以应用于两个类型为 T 的操作符时，这些操作符中的每一个才可以被为类型 T 实例化。

影响：这些操作符中的每一个对 *this* 和 *v* 的每个元素应用指示的操作。

返回值：*this*

备注：在复合赋值的左侧出现数组不会使指向数组的引用或指针失效。

## 29.7.2.8 vararray成员函数 [vararray.members]

```
void swap(vararray v) noexcept;
```

- 影响：*this* 获取 v 的值。获取 *this* 的元素。
- 复杂度：常数级。

```
size_t size const;
```

- 返回值：数组中元素的数量。
- 复杂度：常数时间。

```
T sum() const;
```

- 要求：size() > 0。此函数仅可以被为一个可以应用 operator+= 的类型 T 实例化。
- 返回值：数组所有元素的和。如果数组长度为 1，则返回值 0。否则，返回值通过对数组中元素的拷贝以及数组中所有其他元素以未指定的顺序应用 operator+= 计算得出。

```
T min() const;
```

- 要求：size() > 0。
- 返回值：*this* 中的最小值。对于长度为 1 的数组，返回值 0。对于所有其他长度的数组，使用 operator< 进行确定。

```
T max() const;
```

- 要求：size() > 0。
- 返回值：*this* 中的最大值。对于长度为 1 的数组，返回值 0。对于所有长度的数组，使用 operator< 进行确定。

```
valarray shift(int n) const;
```

- 返回值：一个长度为 size() 的 varray，其中每个元素 I 为 (*this)[I + n]，如果 I + n 非负且小于 size()，否则为 T()。[注：如果元素取的是最左侧的元素，n 的值会将元素左移，并用零填充。—注结束]
- [示例：如果数组值为 -2，结果的前两个元素将为值初始化(11.6）；结果的第三个元素将被赋值为参数第一个元素，依此类推。—示例结束]

```
valarray shift(int n) const;
```

- 返回值：一个 *this* 的循环移位，长度为 size()。如果取最左侧的元素，非负值 n 将元素向左移动 n 位，负值 n 则将元素向右移动 -n 位。

```
valarray apply(T func(T)) const;
valarray apply(T func(const T&)) const;
```

```
void resize(size_t sz, const T& c);
```

影响：将数组更改为 sz，然后分配第二个参数的每个值。调整大小会导致指向数组元素的的所有指针和引用失效。

## 29.7.3 vararray成员操作

## 29.7.3.1 vararray二元操作符

```
template<class T> vararray<T> operator+(const vararray<T>&, const vararray<T>&);
template<class T> vararray<T> operator+(const vararray<T>&, const vararray<T>&);
template<class T> vararray<T> operator-(const vararray<T>&, const vararray<T>&);
template<class T> vararray<T> operator*(const vararray<T>&, const vararray<T>&);
template<class T> vararray<T> operator/(const vararray<T>&, const vararray<T>&);
template<class T> vararray<T> operator[](const vararray<T>&, const vararray<T>&);
template<class T> vararray<T> operator[](const vararray<T>&, const vararray<T>&);
template<class T> vararray<T> operator+=(const vararray<T>&, const vararray<T>&);
template<class T> vararray<T> operator-=(const vararray<T>&, const vararray<T>&);
template<class T> vararray<T> operator*=(const vararray<T>&, const vararray<T>&);
template<class T> vararray<T> operator/=(const vararray<T>&, const vararray<T>&);
template<class T> vararray<T> operator<<=(const vararray<T>&, const vararray<T>&);
template<class T> vararray<T> operator>>=(const vararray<T>&, const vararray<T>&);
```

- 只有当指示的操作符可以应用于两个类型为 T 的操作符时，这些操作符中的每一个才可以被为类型 T 实例化。
- 返回值：长度为 size() 的 varray，每个元素都用指示的操作符初始化。
- 两个参数的长度相同。

```
template<class T> vararray<T> operator+(const vararray<T>&, const vararray<T>&);
template<class T> vararray<T> operator-(const vararray<T>&, const vararray<T>&);
template<class T> vararray<T> operator*(const vararray<T>&, const vararray<T>&);
template<class T> vararray<T> operator/(const vararray<T>&, const vararray<T>&);
template<class T> vararray<T> operator[]=(const vararray<T>&, const vararray<T>&);
template<class T> vararray<T> operator+=(const vararray<T>&, const vararray<T>&);
template<class T> vararray<T> operator-=(const vararray<T>&, const vararray<T>&);
template<class T> vararray<T> operator*=(const vararray<T>&, const vararray<T>&);
template<class T> vararray<T> operator/=(const vararray<T>&, const vararray<T>&);
template<class T> vararray<T> operator<<=(const vararray<T>&, const vararray<T>&);
template<class T> vararray<T> operator>>=(const vararray<T>&, const vararray<T>&);
```

- 只有当指示的操作符可以应用于两个类型为 T 的操作符时，这些操作符中的每一个才可以被为类型 T 实例化。
- 返回值：长度为 size() 的 varray，每个元素都用指示的操作符初始化。
- 两个参数的长度相同。

