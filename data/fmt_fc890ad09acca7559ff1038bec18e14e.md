
`vararray& operator+=(const T&);`

`vararray& operator/=(const T&);`

`vararray& operator*=(const T&);`

`vararray& operator++=(const T&);`

`vararray& operator+=(const T&);`

`vararray& operator/=(const T&);`

`vararray& operator*=(const T&);`

`vararray& operator++=(const T&);`

`vararray& operator+=(const T&);`

`vararray& operator/=(const T&);`

`vararray& operator*=(const T&);`

`vararray& operator++=(const T&);`

`vararray& operator+=(const T&);`

`vararray& operator/=(const T&);`

`vararray& operator*=(const T&);`

`vararray& operator++=(const T&);`

`vararray& operator+=(const T&);`

`vararray& operator/=(const T&);`

`vararray& operator*=(const T&);`

`vararray& operator++=(const T&);`

`vararray& operator+=(const T&);`

`vararray& operator/=(const T&);`

`vararray& operator*=(const T&);`

`vararray& operator++=(const T&);`

`vararray& operator+=(const T&);`

`vararray& operator/=(const T&);`

`vararray& operator*=(const T&);`

`vararray& operator++=(const T&);`

// 26.7.2.8, 成员函数

`void swap(vararray&) noexcept;`

`size_t size() const;`

`T sum() const;`

`T min() const;`

`T max() const;`

`vararray shift(int) const;`

`vararray shift(int) const;`

`vararray apply(T func(T)) const;`

`vararray apply(T func(T)) const;`

`resize(size_t sz, T c = T(0));`

`template<class T, size_t cnt> vararray(const T&[cnt], size_t)`

该类模板是一个一维数组，元素从零开始顺序编号。它是数学概念中“有序值集”的表示。为了方便，`vararray<T>` 类型的对象被称为“数组”。高维的幻觉通过下标索引族产生，而强大的子集处理能力由泛义下标运算符提供。

## 26.7.2.2 构造函数 [vararray.cons]

```cpp
vararray();
```
- 1 效应：构造一个长度为 `n` 的 `vararray`。
`vararray(size_t n);`
- 2 效应：构造一个长度为 `n` 的 `vararray`。数组的每个元素初始化。
`vararray(const T& v, size_t n);`
- 3 效应：构造一个长度为 `n` 的 `vararray`。数组的每个元素用 `v` 初始化。
`vararray(const T* p, size_t n);`
- 4 前置条件：`p + n` 是有效范围。

目的是指定一个能够处理别名和模板扩散的数组模板。因此，`vararray` 既不是矩阵类也不是字段类。然而它是设计此类类非常有用的构建块。`vararray` 数组可以使用。在初始化后，空数组的长度可以通过 `resize` 函数增加。效应：构造一个长度为 `n` 的 `vararray`。数组的值由参数指向的内容初始化。

```cpp
vararray(const vararray& v);
```
- 效应：构造一个与 `v` 长度相同的 `vararray`。元素用 `v` 的对应元素的值初始化。

```cpp
vararray(vararray&& v) noexcept;
```
- 效应：构造一个与 `v` 长度相同的 `vararray`。元素用 `v` 的对应元素的值初始化。
- 复杂度：常数。

```cpp
vararray(initializer_list<T> il);
```
- 效应：等于 `vararray(il.begin(), il.size())`。

```cpp
vararray(const slice_array<T>&);
vararray(const gslice_array<T>&);
vararray(const mask_array<T>&);
vararray(const indirect_array<T>&);
```
- 这些转换构造函数将四个引用模板转换为 `vararray`。

```cpp
~vararray();
```
- 效应：析构函数应用于 `*this` 的每个元素；实现可能释放所有分配的内存。

## 26.7.2.3 赋值 [vararray.assign]

```cpp
vararray& operator=(const vararray& v);
```
- 效应：`*this` 的每个元素赋予 `v` 的对应元素。如果 `v` 的长度不等于 `*this` 的长度，则在执行赋值之前通过 `resize(v.size())` 将 `*this` 调整为与之一相同的长度。
- 前置条件：`size() == v.size()`。
- 返回：`*this`。

```cpp
vararray& operator=(vararray&& v) noexcept;
```
- 效应：获取 `v` 的值。赋值后 `v` 的值未指定。
- 返回：`*this`。

```cpp
vararray& operator=(initializer_list<T> il);
```

```cpp
vararray& operator=(const T& v);
```
- 效应：将 `v` 赋值给 `*this` 的每个元素。

```cpp
vararray& operator=(const slice_array<T>&);
vararray& operator=(const gslice_array<T>&);
vararray& operator=(const mask_array<T>&);
vararray& operator=(const indirect_array<T>&);
```
- 数组下标运算符返回的引用在成员结束数组生命周期之前都是有效的。

## 26.7.2.4 元素访问

```cpp
const T& operator[](size_t n);
T& operator[](size_t n);
```
- 效应：`n < size()`。
- 返回：数组对应元素的引用。
- 注意 1：对于两个数组 `a` 和 `b`，对于任何满足 `i < size(a)` 的 `size_t i` 和 `j`，表达式 `(a[i] == b[j])` 为真。
- 注意 2：这防止优化编译器未使用索引、循环融合和指针追踪。

## 26.7.2.5 子集操作

成员运算符 `[]` 被重载，以提供从 `*this` 控制的元素中选择各种序列。这些操作中的每一个都返回一个子集。`const` 限定的版本将此子集作为一个带有原始对象引用的 `const` 对象返回，结合 `operator=` 的各种重载和其他操作，允许对控制序列进行选择替换（切片）。在每种，所选元素应当存在。

```cpp
vararray operator[](slice slice) const;
```
- 返回：一个包含由 `slice` 指定的控制序列元素的 `vararray`。
- 示例 1：
  `const vararray<char> v0("abcdefghijklmnop", 16);`
  `// v0(slice(2, 5, 3)) 返回 vararray<char>("cilo", 5)`

```cpp
vararray operator[](slice slice);
```
- 返回：一个持有由 `slice` 选择的控制序列元素引用的对象。
- 示例 2：
  `vararray<char> v0("abcdefghijklmnop", 16);`
  `vararray<char> v1("ABCDE", 5);`
  `v0(2, 5, 3) = v1;`
  `// v0 = vararray<char>("AdeBghCjkDmnep", 16)`

```cpp
vararray operator()(const gslice& gslicearr) const;
```
- 返回：一个包含由 `slicearr` 指定的控制序列元素的 `vararray`。
- 示例 3：
  `const vararray<char> v0("abcdefghijklmnop", 16);`
  `const size_t iv[] = {2, 3};`
  `const size_t dv[] = {7, 2};`
  `const vararray<size_t> len(iv, 2), str(dv, 2);`
  `// v0[slice(3, len, str)] 返回 vararray<char>("dfhkmo", 6)`

# ISO/IEC 14882:2020(E)

`glslice_array<T> operator[](const glslice& glslicearr);`

返回：一个包含由 `glslicearr` 所选的受控序列元素引用的对象。
示例：4：

```
valarray<char> v0("abcdefghijklmnop", 16);
valarray<char> vi("ABC", 6);
const size_t lv[] = {2, 3};
const size_t dv[] = {7, 2};
const valarray<size_t> len(iv, 2), str(dv, 2);
v0[glslice(3, str)];
// v0 = valarray<char>("abcBegcD1Enfp", 16);
// end example;
```

`valarray operator[](const valarray<bool>& boolarr) const;`

返回：一个 `valarray`，其中包含由 `boolarr` 指定的受控序列的元素。
示例：5：

```
const valarray<char> v0("abcdefghijklmnop", 16);
const bool vb[] = {false, false, true, true, false};
v0[valarray<bool>(vb, 6)] = vi;
// valarray<char>("abc", 3)
// end example;
```

`mask_array<T> operator[](const valarray<bool>& boolarr);`

返回：一个包含由 `boolarr` 所选的受控序列元素引用的对象。
示例：6：

```
valarray<char> v0("abcdefghijklmnop", 16);
valarray<char> vi("ABC", 6);
const bool vb[] = {false, false, true, true, false};
v0[valarray<bool>(vb, 6)] = vi;
// valarray<char>("abcBegAEjklmnop", 16)
// end example;
```

`valarray operator[](const valarray<size_t>& indarr) const;`

返回：一个 `valarray`，其中包含由 `indarr` 指定的受控序列的元素。
示例：7：

```
valarray<char> v0("abcdefghijklmnop", 16);
const size_t vi[] = {7, 5, 2, 3, 8};
// valarray<size_t>(vi, 5) returns
valarray<char>("hfcdi", 5)
// end example;
```

`indirect_array<T> operator[](const valarray<size_t>& indarr);`

返回：一个包含由 `indarr` 所选的受控序列元素引用的对象。
示例：8：

```
valarray<char> v0("abcdefghijklmnop", 16);
valarray<char> vi("ABCD", 6);
const size_t vi[] = {7, 5, 2, 3, 8};
v0[valarray<size_t>(vi, 5)] = vi;
// valarray<char>("abcBegAEjklmnop", 16)
// end example;
```

## 26.7.2.6 一元运算符

[valarray.unary]

`valarray operator+() const;`

`valarray operator-() const;`

`valarray operator-() const;`

# ISO/IEC 14882:2020(E)

强制：指定的运算符可以应用于类型 `T` 的操作数，并返回类型 `T` 的值（对于 `operator!` 为 `bool`），或者可以无地隐式转换为类型 `T`（对于 `operator!` 为 `bool`）。

返回：一个长度为 `size()` 的数组。返回数组的每个元素都通过将指定的运算符应用于数组对应的元素的结果进行初始化。

## 26.7.2.7 复合赋值 [valarray.cassign]

```
valarray&operator*=(const valarray& v);
valarray&operator/=(const valarray& v);
valarray&operator*=(const valarray& v);
valarray&operator+=(const valarray& v);
valarray&operator==(const valarray& v);
valarray&operator*=(const valarray& v);
valarray&operator+=(const valarray& v);
valarray&operator<<=(const valarray& v);
valarray&operator>>=(const valarray& v);
```

强制：指定的运算符可以应用于类型 `T` 的操作数。
条件：`size() == size()`。
复合赋值左侧的值取决于左侧的其他元素。
影响：这些运算符对 `*this` 的每个元素和 `v` 的相应元素执行指定的操作。
返回：`*this`。
备注：复合赋值左侧数组的出现会导致引用失效。

```
valarray&operator*=(const T& v);
valarray&operator/=(const T& v);
valarray&operator*=(const T& v);
valarray&operator+=(const T& v);
valarray&operator==(const T& v);
valarray&operator*=(const T& v);
valarray&operator+=(const T& v);
valarray&operator<<=(const T& v);
valarray&operator>>=(const T& v);
```

强制：指定的运算符可以应用于类型 `T` 的操作数。
影响：这些运算符应用于 `*this` 的每个元素。
返回：`*this`。
备注：复合赋值左侧的出现会导致指向数组的指针失效。

## 26.7.2.8 成员函数 [valarray.members]

```
void swap(valarray& v) noexcept;
```

影响：`*this` 获取 `v` 的值。
复杂度：常级。

```
size_t size() const;
```

返回：数组中的元素个数。
复杂度：常级。

```
T sum() const;
```

强制：`operator==` 可以应用于类型 `T` 的操作数。
条件：`size() > 0`。
返回：数组所有元素的和。如果数组长度为 1，返回元素 0 的值。否则，通过对数组的副本和其他元素应用运算符计算返回的值。

```
T min() const;
```

强制：`size() > 0`。
返回：`*this` 中的最小值。对于长度为 1 的数组，返回元素 0 的值。对于其他长度，使用 `operator<` 进行确定。

```
valarray shift(int n) const;
```

强制：`size() > 0`。
返回：`*this` 中的最大值。对于长度为 1 的数组，返回元素 0 的值。对于其他长度，使用 `operator<` 进行确定。

```
valarray shift(int n) const;
```
