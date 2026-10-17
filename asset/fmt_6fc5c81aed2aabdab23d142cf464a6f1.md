
# ISO/IEC 14882:2017(E)

`explicit valarray(size_t n);`

影响：构造一个长度为 `n` 的 `valarray`。数组的每个元素都经过值初始化（11.6）。

`valarray(const T& v, size_t n);`

影响：构造一个长度为 `n` 的 `valarray`。数组的每个元素都用 `v` 初始化。

`valarray(const T* p, size_t n);`

要求：`p` 指向一个至少包含 `n` 个元素的数组（11.3.4）。

影响：构造一个长度为 `n` 的 `valarray`。数组的每个元素都用第一个参数所指向的前 `n` 个值进行初始化。

`valarray(const valarray& v);`

影响：构造一个长度与 `v` 相同的 `valarray`。元素用 `v` 对应元素的值初始化。

`valarray(valarray&& v) noexcept;`

影响：构造一个长度与 `v` 相同的 `valarray`。元素用 `v` 对应元素的值初始化。

复杂度：常数级。

```cpp
valarray(initializer_list<T> il);
```

影响：等价于 `valarray(il.begin(), il.size())`。

```cpp
valarray(const slice_array<T>);
valarray(const gslice_array<T>);
valarray(const mask_array<T>);
valarray(const indirect_array<T>);
```

这些构造函数将四种引用模板中的一种转换为 `valarray`。

```cpp
~valarray();
```

影响：析构函数应用于每一个元素 `*this`; 实现可以返回所有分配的内存。

# 29.7.2.3 valarray 赋值 [valarray.assign]

```cpp
valarray& operator=(const valarray& v);
```

- 1 影响：`*this` 的每个元素都被赋值为 `v` 对应元素的值。如果 `v` 的长度不等于 `*this` 的长度，在执行赋值之前调用了 `resize(v.size())`，则会调整 `*this` 的大小以使两个数组长度相同。
- 2 后置条件：`size() == v.size()`。
- 3 返回：`*this`。

```cpp
valarray& operator=(valarray&& v) noexcept;
```

- 4 影响：`this` 获取了 `v` 的值。赋值后 `v` 的值未指定。
- 5 返回：`*this`。
- 6 复杂度：线性级。

> 278 此拷贝构造函数是将 C 数组转换为 `valarray` 的首选方法，而不是别名。允许数组共享存储的实现，但它们必须实现引用时复制（copy-on-reference）机制，以确保数组在概念上是独立的。

> 279 此拷贝构造函数创建一个独立的数组，而不是别名。

```cpp
valarray&& operator=(initializer_list<T> il);
```

- 7 影响：等价于 `return *this = valarray(il);`

```cpp
valarray&& operator=(const T& v);
```

- 8 影响：将 `v` 赋值给 `*this` 的每个元素。
- 9 返回：`*this`。

```cpp
valarray&& operator=(const slice_array<T>& s);
valarray&& operator=(const gslice_array<T>& g);
valarray&& operator=(const mask_array<T>& m);
```

- 10 要求：被赋值数组的长度等于 `size()`。`valarray` 赋值运算符左侧元素的值不依赖于该左侧中另一个元素的值。
- 11 运算符允许将广义赋值运算符的结果直接赋值给 `valarray`。

# 29.7.2.4 valarray 元素访问 [valarray.access]

```cpp
const T& operator[](size_t n) const;
T& operator[](size_t n);
```

- 1 要求：`n < size()`。
- 2 返回：数组中对应元素的引用。[注意：对于任何非常量的 `valarray<T>`、任何 `q` 以及任何取值小于 `a` 长度的 `size_t i`，表达式 `a[i] = q` 中 `a[i]` 的求值结果为真。— 备注结束]
- 3 备注：表达式 `a[i+j] = a[i] + b[j]` 对于所有满足 `i+j < a.size()` 的 `size_t i` 和 `size_t j`，其求值结果均为真。[注意：此属性表明不存在别名（aliasing），可以被优化编译器使用。内联、常量传播、从 `operator new` 获取的指针的追踪，以及其他生成高效 `valarrays` 的技术。— 备注结束]
- 4 表达式 `a[i] == &b[j]` 对于任何两个数组 `a` 和 `b` 以及满足 `i < a.size()` 和 `j < b.size()` 的 `size_t i` 和 `size_t j`，其求值结果均为真。这种别名的缺失可以被优化编译器利用。
- 5 返回：下标数组的引用，该引用有效直到为数组调用成员函数 `resize(size_t, T)` [29.7.2.8] 或数组的生命周期结束，以先发生者为准。

# 29.7.2.5 valarray 子集操作 [valarray.sub]

- 1 成员运算符 `operator[]` 被重载，以提供多种方法从 `*this` 约束的序列中选择元素序列。这些操作中的每一个都返回数组的一个子集。`const` 限定的版本将此子集作为新的 `valarray` 返回。`const` 模板对象持有原始数组的引用，与其他运算符结合，允许对受控序列进行选择性引用（切片）。在每种情况下，所选元素都应该存在。

```cpp
const valarray& operator[](slice) const;
```

- 2 返回：包含 `slice` 元素的 `valarray`。

```cpp
valarray& operator[](slice);
```

- 3 返回：包含 `slice` 元素的 `valarray`。

```cpp
const valarray& operator[](gslice) const;
```

- 4 返回：包含 `gslice` 元素的 `valarray`。

```cpp
valarray& operator[](gslice);
```

- 5 返回：包含 `gslice` 元素的 `valarray`。

```cpp
const valarray& operator[](mask) const;
```

- 6 返回：包含 `mask` 元素的 `valarray`。

```cpp
valarray& operator[](mask);
```

- 7 返回：包含 `mask` 元素的 `valarray`。

```cpp
const valarray& operator[](indirect) const;
```

- 8 返回：包含 `indirect` 元素的 `valarray`。

```cpp
valarray& operator[](indirect);
```

# ISO/IEC 14882:2017(E)

影响：这些操作符中的每一个对 `*this` 的每个元素以及 `*v` 对应的元素执行指示的操作。

返回值：`*this`。

备注：在复合赋值的左侧出现数组会导致引用或指针失效。

```cpp
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

要求：只有当指示的操作符可以应用于两个类型为 `T` 的操作符时，这些操作符中的每一个才可以被为类型 `T` 实例化。

影响：这些操作符中的每一个对 `*this` 和 `*v` 的每个元素应用指示的操作。

返回值：`*this`

备注：在复合赋值的左侧出现数组不会使指向数组的引用或指针失效。

## 29.7.2.8 vararray成员函数 [vararray.members]

```cpp
void swap(vararray v) noexcept;
```

- 影响：`*this` 获取 `v` 的值。获取 `*this` 的元素。
- 复杂度：常数级。

```cpp
size_t size const;
```

- 返回值：数组中元素的数量。
- 复杂度：常数时间。

```cpp
T sum() const;
```

- 要求：`size() > 0`。此函数仅可以被为一个可以应用 `operator+=` 的类型 `T` 实例化。
- 返回值：数组所有元素的和。如果数组长度为 1，则返回值 0。否则，返回值通过对数组中元素的拷贝以及数组中所有其他元素以未指定的顺序应用 `operator+=` 计算得出。

```cpp
T min() const;
```

- 要求：`size() > 0`。
- 返回值：`*this` 中的最小值。对于长度为 1 的数组，返回值 0。对于所有其他长度的数组，使用 `operator<` 进行确定。

```cpp
T max() const;
```

- 要求：`size() > 0`。
- 返回值：`*this` 中的最大值。对于长度为 1 的数组，返回值 0。对于所有长度的数组，使用 `operator<` 进行确定。

```cpp
valarray shift(int n) const;
```

- 返回值：一个长度为 `size()` 的 `varray`，其中每个元素 `I` 为 `(*this)[I + n]`，如果 `I + n` 非负且小于 `size()`，否则为 `T()`。[注：如果元素取的是最左侧的元素，`n` 的值会将元素左移，并用零填充。—注结束]
- [示例：如果数组值为 -2，结果的前两个元素将为值初始化(11.6）；结果的第三个元素将被赋值为参数第一个元素，依此类推。—示例结束]

```cpp
valarray shift(int n) const;
```

- 返回值：一个 `*this` 的循环移位，长度为 `size()`。如果取最左侧的元素，非负值 `n` 将元素向左移动 `n` 位，负值 `n` 则将元素向右移动 `-n` 位。

```cpp
valarray apply(T func(T)) const;
valarray apply(T func(const T&)) const;
```

```cpp
void resize(size_t sz, const T& c);
```

影响：将数组更改为 `sz`，然后分配第二个参数的每个值。调整大小会导致指向数组元素的的所有指针和引用失效。

## 29.7.3 vararray成员操作

## 29.7.3.1 vararray二元操作符

```cpp
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

- 只有当指示的操作符可以应用于两个类型为 `T` 的操作符时，这些操作符中的每一个才可以被为类型 `T` 实例化。
- 返回值：长度为 `size()` 的 `varray`，每个元素都用指示的操作符初始化。
- 两个参数的长度相同。

```cpp
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

- 只有当指示的操作符可以应用于两个类型为 `T` 的操作符时，这些操作符中的每一个才可以被为类型 `T` 实例化。
- 返回值：长度为 `size()` 的 `varray`，每个元素都用指示的操作符初始化。
- 两个参数的长度相同。

# ISO/IEC 14882:2017(E)

可以应用于且指示运算符返回的值类型为 `bool` 或可以无歧地隐式转换为 `bool` 类型。
返回：一个 `vararray<bool>`，其长度等于数组参数的长度。返回数组的每个元素都用将指示运算符应用于对应元素和非数组参数的结果进行初始化。

```cpp
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
```
