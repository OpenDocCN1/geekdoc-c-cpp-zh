
- 1 头文件 `<varray>` 定义了五个类（`varray, slice_array, gslice_array, mask_array, and indirect_array`）、两个类（`slice` 和 `gslice`）以及一系列用于数值数组重塑和操作的相关函数模板。

- 2 `varray` 类被定义为不含别名（free of aliasing），允许对这些类的操作进行优化。

- 3 任何返回 `varray<T>` 的函数都允许返回另一种类型的对象，前提是 `varray<T>` 的 `const` 成员函数也适用于该类型。此返回类型相对于最深嵌套的参数类型，模板嵌套深度不应超过两层。²81

> 281) 18.3.2 建议递归嵌套模板实例化的最小数量。这一要求间接暗示了 varray 表达式的最小允许复杂度。

- 4 引入替换 `replace<T>` 的实现应提供额外的函数和运算符，如下：
  - (4.1) — 对于每个除 `begin` 和 `end` (26.6.10) 之外接收 `const valarray<T>` 的函数，应添加接受替换类型的相同函数：

  - (4.2) — 对于每个接受两个 `valarray<T>` 参数的函数，应添加接受 `const valarray<T>` 和替换类型各种组合的相同函数。

- 5 特别地，实现应该允许从此类替换类型构造 `valarray<T>`，并允许此类类型的赋值和计算赋值给 `valarray<T>`、`slice_array<T>`、`glslice_array<T>`、`mask_array<T>` 和 `indirect_array<T>` 对象。

- 6 如果没有足够的资源执行操作，这些库允许抛出 `bad_alloc` (18.6.2.1) 异常。注意，这并不是强制性的。

## 26.6.2 类 valarray [template.valarray]

### 26.6.2.1 类 valarray 概述 [template.valarray.overview]

```cpp
namespace std {
template<class T> class valarray {
public:
    typedef T value_type;
    // 构造/析构:
    valarray();
    explicit valarray(size_t);
    valarray(const T*, size_t);
    valarray(const T*, size_t);
    valarray(const valarray<T>&);
    valarray(const slice_array<T>&);
    valarray(const glslice_array<T>&);
    valarray(const mask_array<T>&);
    valarray(const indirect_array<T>&);
    valarray(const initializer_list<T>&);
    // 26.6.2.2 赋值:
    valarray<T>& operator=(const valarray<T>&);
    valarray<T>& operator=(const valarray<T>&) noexcept;
    valarray<T>& operator=(const initializer_list<T>&);
    valarray<T>& operator=(const T* const);
    valarray<T>& operator=(const slice_array<T>&);
    valarray<T>& operator=(const glslice_array<T>&);
    valarray<T>& operator=(const mask_array<T>&);
    valarray<T>& operator=(const indirect_array<T>&);
    // 26.6.2.3 元素访问:
    const T& operator[](size_t) const;
    const T& operator[](size_t);
    // 26.6.2.4 子集操作:
    valarray<T> operator[](slice) const;
    slice_array<T> operator[](slice);
    valarray<T> operator[](const glslice<T>&);
}
```

```cpp
glslice<T> operator[](const glslice&);
valarray<T> operator[](const valarray<bool>& const;
mask_array<T> operator[](const valarray<bool>& const;
valarray<T> operator[](const valarray<size_t>& const;
indirect_array<T> operator[](const valarray<size_t>& const);
// 26.6.2.6 一元运算符:
valarray<T> operator+() const;
valarray<T> operator-() const;
valarray<T> operator() const;
valarray<bool> operator!() const;
// 26.6.2.7 计算赋值:
valarray<T>& operator+=(const T);
valarray<T>& operator/=(const T);
valarray<T>& operator%=(const T);
valarray<T>& operator*=(const T);
valarray<T>& operator-=(const T);
valarray<T>& operator&=(const T);
valarray<T>& operator|=(const T);
valarray<T>& operator<<=(const T);
valarray<T>& operator>>=(const T);
// 26.6.2.8 成员函数:
void swap(valarray<T>&) noexcept;
size_t size() const;
T sum() const;
T min() const;
T max() const;
valarray<T> shift(int) const;
valarray<T> cshift(int) const;
valarray<T> apply(T func) const;
valarray<T> apply(T func, T const) const;
void resize(size_t sz, T c());
```

- 1 类模板 `varray<T>` 是一个从零开始编号的一维标量数组。它是数值集合概念的表示。通过下标运算符提供的强大子集功能可以产生高维幻象。

- 2 实现允许将 `<valarray>` 中声明的函数标记为内联。

### 26.6.2.2 valarray 构造函数 [valarray.cons]

```cpp
valarray();
```

- 1 构造一个长度为零的 `valarray<T>` 对象²83²84。

```cpp
explicit valarray(size_t);
```

- 2 由此构造函数创建的数组长度等于参数的值。数组元素被值初始化（8.5）。

```cpp
valarray(const T*, size_t);
```

- 3 由此构造函数创建的数组长度等于第二个参数。数组的元素由第一个参数指向的值初始化。

```cpp
valarray(const T*, size_t);
```

- 4 由此构造函数创建的数组长度等于第二个参数 n。数组元素的值由第一个参数指向的前 n 个值初始化。²85 如果第二个参数的值大于第一个参数指向的值的数量，则行为是未定义的。

```cpp
valarray(const valarray&);
```

- 5 由此构造函数创建的数组与数组参数长度相同。元素用该数组对应的值初始化。²86

```cpp
valarray(const valarray&&& v) noexcept;
```

- 6 由此构造函数创建的数组与数组参数长度相同。元素用该数组对应的值初始化。

- 7 复杂度：常量。

```cpp
valarray(initializer_list<T> il);
```

- 8 效果：同于 `valarray(il.begin(), il.size())`。

```cpp
valarray(const slice_array<T>&);
valarray(const galice_array<T>&);
valarray(const mask_array<T>&);
valarray(const indirect_array<T>&);
```

- 9 这些构造函数将四个模板之一转换为 valarray。
- `valarray();`
- 10 析构函数用于清理一个具有消除歧义和处理临时变量增殖最小功能的数组模板。然后，valarray 模板既不是矩阵类也不是数组类。它是设计此类类非常有用的代码块。

## 26.6.2.3 vararray 赋值 [vararray.assign]

`vararray<T> operator=(const vararray<T>& v);`

+ 1 *this 数组的每个元素都被赋值为参数中对应元素的值。如果 v 的长度与 *this* 的长度不相等，则在执行赋值之前，调整 *this* 的大小使两个数组长度相同，就好像调用了 `resize(v.size())`。
2 后置条件：`size() == v.size()`。
3 影响：*this* 获得了 v 的值。赋值后的值未指定。
4 复杂度：线性。

`vararray<T>& operator=(vararray<T>& v) noexcept;`

+ 5 影响：*this = `vararray(v)`。
6 返回：*this。

`vararray& operator=(initializer_list<T> il);`
`vararray<T>& operator=(const T& t);`

标量赋值会导致 *this 数组的每个元素都赋值赋值为参数的值。

`vararray<T> operator=(const slice_array<T>& v);`
`vararray<T> operator=(const gice_array<T>& v);`
`vararray<T> operator=(const mask_array<T>& v);`
`vararray<T> operator=(const indirect_array<T>& v);`

+ 8 参数所引用数组的长度为 `size()`。
9 这些操作符允许将泛化下标操作的结果直接赋值给 vararray。

如果 vararray 赋值运算符左侧的元素取决于该左侧另一个元素的值，则其行为是未定义的。

## 26.6.2.4 vararray 元素访问 [vararray.access]

`const T& operator[](size_t t);`
`T& operator[]=(size_t t);`

+ 1 下标运算符返回数组中对应元素的引用。

+ 2 因此，对于任何非 const 的 `vararray<T> a`、任何 `T q`，以及满足值小于 a 长度的 size i，表达式 `(a[i] == q)` 的求值结果为真。
3 对于所有满足 i+j 小于 a 长度的 size_t i 和 size_t j，表达式 `a[i+j] == a[j]` 的求值结果为真。
4 同样，对于任何两个数组 a 和 b，只要 size_t i 小于 a 的长度且 j 小于 b 的长度，表达式 `a[i] != b[j]` 的求值结果即为真。这一属性表明不存在别名（aliasing），并可被优化编译器利用以获得优势。

+ 5 数组下标运算符返回的引用有效，直到为该数组调用成员函数 `resize(size_t, T)` (26.6.2.8) 或该数组的生命周期结束，以先发生者为准。

+ 6 如果使用一个值不小于数组长度的 size_t 参数来调用操作符，则其行为是未定义的。

> 287 编译器可以利用内联、常量传播、循环融合、跟踪从 `operator new` 获取的指针以及其他技术来生成高效的 vararrays。

## 26.6.2.5 valarray 子集操作

成员运算符`[]` 被重载，用以提供多种方法从 *this 控制的元素中选择元素序列。这些操作中的每一个都返回数组的一个子集。带有 const 限定符的版本将此返回为一个新的 valarray。非 const 版本返回一个类模板对象，该对象拥有指向原始数组的引用，结合 `operator=` 的各种重载和其他赋值操作符工作，允许对控制序列进行选择性替换（切片）。在每情况下，选定的元素必须存在。

```cpp
valarray<T> operator[](slice slicearr) const;
```

返回：一个类 `valarray<T>` 的对象，包含由 `slicearr` 指定的控制序列的元素。[示例]:

const `valarray<char> v0("abcdefghijklmnop", 16);`
// `slice(2, 5, 3)` 返回 `valarray<char>("cilo", 5)`

end example

```cpp
slice_array<T> operator[](slice slicearr);
```

```
返回：一个持有指向由 slicearr 选择的控制序列元素引用对象。[示例]:

valarray<char> v0("abcdefghijklmnop", 16);
valarray<char> v1("ABCDE", 5);
v0[slice(2, 5, 3)] = v1;
// v0 == valarray<char>("AbdeBgCijdEnfp", 16)

end example
```

```cpp
valarray<T> operator[](const gslice & gslice) const;
```

```
返回：一个类 valarray<T> 的对象，包含由 gslice 指定的控制序列的元素。[示例]:

const valarray<char> v0("abcdefghijklmnop", 16);
const size_t len[] = { 2, 3 };
const size_t dv[] = { 7, 2 };
const valarray<size_t> len(len, 2), str(dv, 2);
// gslice(3, len, str) 返回
valarray<char>("dfhkmo", 6)

end example
```

```cpp
slice_array<T> operator[](const gslice & gslice);
```

```
返回：一个持有指向由 gslice 选择的控制序列元素引用对象。[示例]:

valarray<char> v0("abcdefghijklmnop", 16);
valarray<char> v1("ABCDE", 5);
const size_t len[] = { 2, 3 };
const size_t dv[] = { 7, 2 };
const valarray<size_t> len(len, 2), str(dv, 2);
v0[gslice(3, len, str)] = v1;
// v0 == valarray<char>("AbdeBgCijdEnfp", 16)

end example
```

```cpp
valarray<T> operator[](const valarray<bool>& boolarr) const;
```

```
返回：一个类 valarray<T> 的对象，包含由 boolarr 指定的控制序列元素。[示例]:

const valarray<char> v0("abcdefghijklmnop", 16);
const bool vb[] = {false, false, true, false, true};
// v0[vb] 返回 valarray<char>("cdf", 3)
```

```slice_array<T> operator[](const valarray<bool>& boolarr) const;
```

```

返回：一个持有指向由 boolarr 选择的控制序列元素引用对象。[示例]:

valarray<char> v0("abcdefghijklmnop", 16);

valarray<char> v1("ABCDE", 5);

const bool vb[] = {false, false, true, false, true};

v0[vb] = v1;

// v0 == valarray<char>("AbdeBgCijdEnfp", 16)

```

```cpp
valarray<T> operator[](const valarray<size_t>& indarr) const;
```

```
返回：一个类 valarray<T> 的对象，包含由 indarr 指定的控制序列元素。[示例]:

valarray<char> v0("abcdefghijklmnop", 16);

const size_t vi[] = {7, 5, 2, 3, 8};

// v0[vi] 返回 valarray<char>("hfcdi", 5)
```

```cpp
indirect_array<T> operator[](const valarray<size_t>& indarr) const;
```
