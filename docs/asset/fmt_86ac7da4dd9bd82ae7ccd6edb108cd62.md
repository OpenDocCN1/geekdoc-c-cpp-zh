
`typedef T value_type;`

`void& operator=(const val_array<T>& const);`

`void& operator*=(const val_array<T>& const);`

`void& operator/=(const val_array<T>& const);`

`void& operator+=(const val_array<T>& const);`

`void& operator++=(const val_array<T>& const);`

`void& operator-=(const val_array<T>& const);`

`void& operator*=(const val_array<T>& const);`

`void& operator|=(const val_array<T>& const);`

`void& operator<<=(const val_array<T>& const);`

`void& operator>>=(const val_array<T>& const);`

```cpp
slice_array(const slice_array&);
slice_array();
const slice_array& operator=(const slice_array&) const;
void operator=(const T&) const;
slice_array() = delete; // 通过声明拷贝构造函数来
};
```

`slice_array` 模板是一个辅助模板，供 `slice` 下标运算符 `slice_array<T>::operator[](slice)` 使用。

它拥有对 `slice` 对象指定的数组子集的引用。

> [示例：表达式 `slice[1, 5, 3] = b;` 的效果是将 `b` 的元素赋值给 `a` 中元素的 `slice` 切片。对于所示的 `slice`，从 `a` 中选择的元素是 1, 4, ..., 13。-- 示例]

### 26.6.5.2 slice_array 赋值 [slice.arr.assign]

§ 26.6.5.2

# ISO/IEC N4296

```
void operator= (const valarray<T>&) const;
slice_array& operator=(const slice_array&) const;
```

- 1 这些赋值运算符具有引用语义，将参数元素元素的值赋值给 `slice_array` 对象所引用的 `valarray<T>` 对象。

### 26.6.5 slice_array 计算赋值

> [slice.array.comp.assign]

```
void operator++ (const valarray<T>&) const;
void operator/ (const valarray<T>&) const;
void operator* (const valarray<T>&) const;
void operator++ (const valarray<T>&) const;
void operator-= (const valarray<T>&) const;
void operator*= (const valarray<T>&) const;
void operator*= (const valarray<T>&) const;
void operator<< (const valarray<T>&) const;
void operator>> (const valarray<T>&) const;
```

- 1 这些计算赋值具有引用语义，将指示的操作应用于参数的元素以及 `slice_array` 对象所引用的 `valarray<T>` 对象的选元素。

### 26.6.5.4 slice_array fill 函数

> [slice.arr.fill]

```
void operator= (const T&) const;
```

- 1 该函数具有引用语义，将其参数的值赋值给 `slice_array` 对象所引用的 `valarray<T>` 对象。

### 26.6.6 gslice 类

> [class.gslice]

#### 26.6.6.1 gslice 类概述

> [class.gslice.overview]

```
namespace std {
  gslice {
  public:
    gslice();
    gslice(size_t s, const valarray<size_t>& l, const valarray<size_t>& d);
    size_t
    valarray<size_t> size() const;
    valarray<size_t> stride() const;
  };
}
```

- 1 类表示数组的广义 `slice`。`gslice` 由一个起始偏移量 `s`、一组长度集合 `l` 和一组步长集合 `d` 定义。长度的数量应等于步长的数量。

- 2 一个 `gslice` 表示从索引集 `ij`（其数量与步长的数量相等）到单个索引 `k` 的映射。它对于使用 `valarray` 模板构建多维数组类很有用，`valarray` 是一维。`gslice` 指定的多维索引值集为

```
k = s + \sum_{ij} ij_j
```

多维索引 `i_j` 的范围从 0 到 `l_{ij} - 1`。

- 3 [示例：`gslice` 规范
§ 26.6.6.1

© ISO/IEC N4296

```
start = 3
length = {2, 4, 3}
stride = {19, 4, 1}
```

产生一维索引序列

```
k = 3 + (0, 1) * 19 + (0, 2, 3) * 4 + (0, 1, 2) * 1
```

其排序所示：

| i0, i1, i2 | k |
| :--- | :--- |
| (0, 0, 0) | 3 |
| (0, 0, 1) | 4 |
| (0, 0, 2) | 5 |
| (0, 1, 0) | 7 |
| (0, 1, 1) | 8 |
| (0, 1, 2) | 9 |
| (0, 2, 0) | 11 |
| (0, 2, 1) | 12 |
| (0, 2, 2) | 13 |
| (0, 3, 0) | 15 |
| (0, 3, 1) | 16 |
| (0, 3, 2) | 17 |
| (1, 0, 0) | 22 |
| (1, 0, 1) | 23 |
| (1, 0, 2) | ... | ... |
| (1, 3, 2) | 36 |

也就是说，最高阶索引变化最快。 [示例：如果将示例中的 `stride` 参数更改为 `{1, 1, 1}`，结果序列的前几个元素将是
(0, 0, 0), 3,
(0, 0, 1), 4,
(0, 0, 2), 5,
(0, 1, 0), 7,
(0, 1, 1), 8,
(0, 1, 2), 9... 示例]

如果将退化 `slice` 作为 `operator[](gslice)` 的非 `const` 参数，结果行为是未定义的。

### 26.6.6.2 gslice 构造函数

```
gslice();
gslice(size_t start, const valarray<size_t>& lengths, const valarray<size_t>& strides);
gslice(const gslice&);
```

§ 26.6.6.2

默认构造函数等于 `gslice(0, valarray<size_t>(), valarray<size_t>())`。带参数的构造函数根据上一节说明的起始、长度和步长构建 `gslice`。

### 26.6.6.3 gslice 访问函数

```
size_t start() const;
valarray<size_t> size() const;
valarray<size_t> stride() const;
```

- 返回：`gslice` 的起始、长度或步长。复杂度：`start()` 为常数时间，`size()` 和 `stride()` 与步长数量线性。

### 26.6.7 gslice_array

#### 26.6.7.1 gslice_array 概述

```cpp
namespace std {
template <class T> class gslice_array {
public:
    typedef T value_type;
    void operator=(const valarray<T>& const;
    void operator*=(const valarray<T>& const);
    void operator/=(const valarray<T>& const;
    void operator+=(const valarray<T>& const;
    void operator-=(const valarray<T>& const);
    void operator*=(const valarray<T>& const;
    void operator/=(const valarray<T>& const;
    void operator*=(const valarray<T>& const;
    void operator/=(const valarray<T>& const;
    void operator<<=(const valarray<T>& const;
    void operator>>=(const valarray<T>& const;
    gslice_array(const gslice_array&);
    ~gslice_array();
    gslice_array& operator=(const gslice_array&) const;
    void operator=(const T&) const;
    gslice_array() = delete; // 如上方声明拷贝构造函数所暗示
};
```

这是一个辅助模板，供 `gslice` 下标运算符 `gslice_array<T>::operator[](const gslice&)` 使用。

它拥有对 `gslice` 对象指定的数组子集的引用。

因此，表达式 `a[gslice(length, stride)] = b` 的效果是将元素 `b` 赋值给 `a` 中元素的广义切片。

### 26.6.7.2 gslice_array 赋值

```
void operator=(const valarray<T>&) const;
const gslice_array& operator=(const gslice_array&) const;
```

这些赋值运算符具有引用语义，将参数的值赋值给 `gslice_array` 所引用的 `valarray<T>` 对象。

### 26.6.7.3 gslice_array

```
void operator*=(const valarray<T>&) const;
void operator/=(const valarray<T>&) const;
void operator*=(const valarray<T>&) const;
void operator+=(const valarray<T>&) const;
void operator-=(const valarray<T>&) const;
void operator*=(const valarray<T>&) const;
void operator==(const valarray<T>&) const;
void operator<<=(const valarray<T>& const;
void operator>>=(const valarray<T>& const;
```

> [slice.array.comp.assign]

- 这些计算赋值具有引用语义，将指示的操作应用于参数的元素以及 `gslice_array` 对象所引用的 `valarray<T>` 对象的选元素。

### 26.6.7.4 gslice_array fill 函数

> [slice.arr.fill]

```
void operator=(const T&) const;
```

- 该函数具有引用语义，将其参数的值赋值给 `gslice_array` 对象所引用的 `valarray<T>` 对象。

### 26.6.8 类模板 mask_array

> [template.mask_array]

#### 26.6.8.1 类模板 mask_array 概述

> [template.mask_array.overview]

```cpp
namespace std {
    template <class T> class mask_array {
public:
        typedef T value_type;
        void operator=(const valarray<T>& const;
        void operator*=(const valarray<T>& const);
        void operator/=(const valarray<T>& const;
        void operator+=(const valarray<T>& const;
        void operator-=(const valarray<T>& const);
        void operator*=(const valarray<T>& const;
        void operator==(const valarray<T>&) const;
        void operator<<=(const valarray<T>& const;
        void operator>>=(const valarray<T>& const;
```

# © ISO/IEC

# N4296

它对由布尔掩码指定的数组子集具有引用语义。因此，表达式 `a[mask] = b;` 的效果是将 `b` 的元素赋值给 `a` 中被掩码的元素（对应 `mask` 中相应元素为 `true` 的元素）。

### 26.6.8.2 mask_array 赋值

```
void operator=(const valarray<T>& const;
const mask_array& operator=(const mask_array&) const;
```

这些赋值具有引用语义，将参数数组的值赋值给它所引用的 `valarray<T>` 对象的选定元素。

### 26.6.8.3 mask_array 计算赋值

```
void operator*(const valarray<T>& const);
void operator=(const valarray<T>& const);
void operator/=(const valarray<T>& const);
void operator**(const valarray<T>& const);
void operator-(const valarray<T>& const);
void operator*=(const valarray<T>& const);
void operator&=(const valarray<T>& const);
void operator|=(const valarray<T>& const);
void operator<<=(const valarray<T>& const);
void operator>>=(const valarray<T>& const;
```

这些计算赋值具有引用语义，将指定的运算应用于参数元素以及 `mask` 对象所引用的 `valarray<T>` 对象的选定元素。

### 26.6.8.4 mask_array fill 函数

```
void operator=(const T& const) const;
```

此函数具有引用语义，将其值赋值给 `mask_array` 对象所引用的 `valarray<T>` 对象的元素。

### 26.6.9 类模板 indirect_array

#### 26.6.9.1 类模板 indirect_array 概述

```
namespace std {
template <class T> class indirect_array {
public:
    typedef T value_type;
    void operator=(const valarray<T>& const) const;
    void operator*(const valarray<T>& const) const;
    void operator/=(const valarray<T>& const) const;
    void operator/=(const valarray<T>& const) const;
    void operator**(const valarray<T>& const) const;
    void operator-(const valarray<T>& const) const;
    void operator*=(const valarray<T>& const) const;
    void operator+=(const valarray<T>& const) const;
    void operator&=(const valarray<T>& const) const;
```
