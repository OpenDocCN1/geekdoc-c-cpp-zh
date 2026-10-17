
除了用于模拟二维数组外，切片还可以描述许多其他序列。它是一种指定非常简单序列的相当通用的方法。此概念在 §40.5.6 中进一步探讨。

可以将切片看作是一种奇特的迭代器：切片允许我们描述 `valarray` 的一组索引。我们可以基于此构建 STL 风格的迭代器：

```cpp
template<typename T>
class Slice_iter {
    valarray<T>* v;
    slice s;
    size_t curr; // 当前元素的索引

    T& ref(size_t i) const { return (*v)[s.start() + i * s.stride()]; }
public:
    Slice_iter(valarray<T>* vv, slice ss, size_t pos = 0) : v{vv}, s{ss}, curr{0} { }

    Slice_iter end() const { return {this, s, s.size()}; }
    Slice_iter& operator++() { ++curr; return *this; }
    Slice_iter operator++(int) { Slice_iter t = *this; ++curr; return t; }

    T& operator[](size_t i) { return ref(i); }       // C 风格下标
    T& operator()(size_t i) { return ref(i); }       // Fortran 风格下标
    T& operator*() { return ref(curr); }             // 当前元素

    bool operator==(const Slice_iter& q) const {
        return curr == q.curr && s.stride() == q.s.stride() && s.start() == q.s.start();
    }
    bool operator!=(const Slice_iter& q) const {
        return !(*this == q);
    }
    bool operator<(const Slice_iter& q) const {
        return curr < q.curr && s.stride() == q.s.stride() && s.start() == q.s.start();
    }
};
```

由于切片具有大小，我们甚至可以提供范围检查。这里，我利用了 `slice::size()` 来提供 `end()` 操作，以为切片的一过去末尾元素提供迭代器。

由于切片可以描述行或列，`Slice_iter` 允许我们按行或按列遍历 `valarray`。

## 40.5.5 `slice_array`

从 `valarray` 和切片，我们可以构建一个看起来和感觉像 `valarray` 的东西，但实际上只是引用由切片描述的数组子集的方式。

`slice_array<T>`（§iso.26.6.5）

- `slice_array sa {sa2};` 拷贝构造函数：`sa` 引用与 `sa2` 相同的元素；`sa = sa2` 将 `sa[i]` 引用的每个元素赋给 `sa2[i]` 引用的对应元素。
- `sa = va` 将 `va[i]` 赋给 `sa[i]` 引用的每个对应元素；`sa = v` 将 `v` 赋给 `sa` 引用的每个元素。
- `sa @= va` 表示对 `sa` 的每个元素执行 `sa[i] @= va[i]`；`@` 可以是 `/`, `%`, `+`, `-`, `^`, `&`, `|`, `<<`, `>>`。

用户不能直接创建 `slice_array`。相反，用户对 `valarray` 进行下标以创建给定切片的 `slice_array`。一旦 `slice_array` 初始化，对它的所有引用都会间接指向为其创建的 `valarray`。例如，我们可以像这样创建表示数组中每第二个元素的对象：

```cpp
void f(valarray<double>& d)
{
    slice_array<double>& v_even = d[slice(0, d.size() / 2 + d.size() % 2, 2)];
    slice_array<double>& v_odd = d[slice(1, d.size() / 2, 2)];

    v_even *= v_odd; // 乘以元素对并将结果存储在偶数元素中
    v_odd = 0;
    // 将 0 赋给 d 的每个奇数元素
}
```

`slice_array` 可以被拷贝。例如：

```cpp
slice_array<double> row(valarray<double>& d, int i) {
  slice_array<double> v = d[slice(0, 2, d.size() / 2)]; // ...
  return d[slice(i % 2, i, d.size() / 2)];
}
```

## 40.5.6 广义切片

`slice`（§29.2.2、§40.5.4）可以描述 `n` 维数组的行或列。然而，有时我们需要提取的不是行或列的子数组。例如，我们可能想从 4×3 矩阵的左上角提取 3×2 矩阵：

```
00 01 02
10 11 12
20 21 22
30 31 32
```

不幸的是，这些元素不是以可以用单个 `slice` 描述的方式分配的：

```
子数组: 0 1 2 3 4 5
00 01 02 10 11 12 20 21 22 30 31 32
```

`gslice` 是一个“广义切片”，它包含（几乎）来自 `n` 个切片的信息：

```cpp
class std::gslice {
// 而不是像 slice 那样的 1 个步长和一个大小，gslice 保存 n 个步长和 n 个大小
public:
  gslice();
  gslice(size_t sz, const valarray<size_t>& lengths, const valarray<size_t>& strides);
  size_t start() const; // 第一个元素的索引
  valarray<size_t> size() const; // 维度中的元素数
  valarray<size_t> stride() const; // index[0], index[1], ... 的步长
};
```

额外的值允许 `gslice` 指定 `n` 个整数与用于寻址数组元素的索引之间的映射。例如，我们可以用一对 `(length,stride)` 对来描述 3×2 矩阵的布局：

```cpp
size_t gslice_index(const gslice& s, size_t i, size_t j) // max (i,j) 到它们对应的索引
{
    return s.start() + i * s.stride()[0] + j * s.stride()[1];
}

valarray<size_t> lengths {2,3}; // 第一个维度中有 2 个元素
// 第二个维度中有 3 个元素
valarray<size_t> strides {3,1}; // 3 是第一个索引的步长
// 第一个索引的步长
// 1 是第二个索引的步长
```

```cpp
void f() {
    gslice s(0, lengths, strides);
    for (int i = 0; i < 3; ++i) // 遍历每一行
        for (int j = 0; j < 2; ++j) // 遍历行中的每个元素
            cout << "(" << i << "," << j << ")->" << gslice_index(s, i, j) << ";"; // 打印映射
}
```

这会打印：

```
(0,0)->0; (0,1)->1; (1,0)->3; (1,1)->4; (2,0)->6; (2,1)->7
```

以这种方式，具有两个 `(length,stride)` 对的 `gslice` 描述二维数组的子数组，具有三个 `(length,stride)` 对的 `gslice` 描述三维数组的子数组，等等。使用 `gslice` 作为 `valarray` 的索引会产生由 `gslice` 描述的元素组成的 `gslice_array`。例如：

```cpp
void f(valarray<float>& v)
{
    gslice m(0, lengths, strides);
    v[m] = 0; // 将 0 赋给 v[0],v[1],v[3],v[4],v[6],v[7]
}
```

`gslice_array` 提供与 `slice_array`（§40.5.5）相同的成员集。`gslice_array` 是使用 `gslice` 作为 `valarray` 的下标的结果（§40.5.2）。

## 40.6 广义数值算法

在 `<numeric>` 中，标准库提供了一些广义数值算法，其风格类似于 `<algorithm>` 中的非数值算法（第 32 章）。这些算法提供了对数值序列的常见操作的通用版本：

### 数值算法 (§iso.26.7) （继续）

这些算法接受输入迭代器：

```
x = accumulate(b, e, i)                // x 是 i 和 [b:e) 元素的和
x = accumulate(b, e, i, f)             // 使用 f 而不是 + 进行 accumulate
x = inner_product(b, e, b2, i)         // x 是 [b:e) 和 [b2:b2+(e-b)) 的内积，
                                       // 即 i 和 (*p1)*(*p2) 的和，对每个 p1 在 [b:e) 中和对应的 p2 在 [b2:b2+(e-b)) 中
x = inner_product(b, e, b2, i, f, f2)  // 使用 f 和 f2 而不是 + 和 * 的 inner_product
```

第 40.6 节 广义数值算法 1177

### 数值算法（续） (§iso.26.7)

这些算法接受输入迭代器：

```
p = partial_sum(b, e, out)           // [out:p) 的第 i 个元素是 [b:b+i] 元素的和
p = partial_sum(b, e, out, f)        // 使用 f 而不是 + 的 partial_sum
p = adjacent_difference(b, e, out)   // [out:p) 的第 i 个元素是 (*b+i)-*(b+i-1)，i>0 时；
                                     // 如果 e-b>0，则 *out 是 *b
p = adjacent_difference(b, e, out, f)
iota(b, e, v)
```

`adjacent_difference` 使用 `f` 代替 `-`，对于 `[b:e)` 中的每个元素赋值 `++v`；因此序列变为 `v+1`, `v+2`, ...

这些算法将诸如求和之类的常见操作泛化，使它们能够适用于各种序列，并将应用于这些序列元素的操作作为参数。对于每个算法，通用版本都附带一个使用该算法最常见运算符的版本。

### 40.6.1 `accumulate()`

`accumulate()` 的简单版本使用序列元素的 `+` 运算符进行相加：

```cpp
template<typename In, typename T>
T accumulate(In first, In last, T init)
{
    for (; first != last; ++first) // forall elements in [first:last)
        init = init + *first;      // plus
    return init;
}
```

可以这样使用：

```cpp
void f(vector<int>& price, list<float>& incr)
{
    int i = accumulate(price.begin(), price.end(), 0); // accumulate in int
    double d = 0;
    d = accumulate(incr.begin(), incr.end(), d);       // accumulate in double
    int prod = accumulate(price.begin(), price.end(), 1, [](int a, int b) { return a * b; }); // ...
}
```

传入的初始值类型决定了返回类型。

我们可以将初始值和“组合元素”的操作作为参数提供给 `accumulate()`，因此 `accumulate()` 并不只关乎加法。

从数据结构中提取值是 `accumulate()` 的常见操作。例如：

```cpp
struct Record {
    // ...
    int unit_price;
    int number_of_units;
};

long price(long val, const Record& r) {
    return val + r.unit_price * r.number_of_units;
}

void f(const vector<Record>& v)
{
    cout << "Total value: " << accumulate(v.begin(), v.end(), 0, price) << '\n';
}
```

与 `accumulate` 类似的操作在某些社区中被称为 `reduce`、`reduction` 和 `fold`。

### 40.6.2 `inner_product()`

从单个序列进行累积非常常见，而从一对序列进行累积也并不少见：

```cpp
template<typename In, typename In2, typename T>
T inner_product(In first, In last, In2 first2, T init)
{
    while (first != last)
        init = init + *first++ * *first2++;
    return init;
}
```

```cpp
template<typename In, typename In2, typename T, typename BinOp, typename BinOp2>
T inner_product(In first, In last, In2 first2, T init, BinOp op, BinOp2 op2)
{
    while (first != last)
        init = op(init, op2(*first++, *first2++));
    return init;
}
```

与往常一样，只传入第二个输入序列的起始位置作为参数。第二个输入序列被假定为至少与第一个序列一样长。

将 `Matrix` 乘以 `valarray` 的关键操作就是 `inner_product`：

```cpp
valarray<double> operator*(const Matrix& m, valarray<double>& v)
{
    valarray<double> res(m.dim2());

    for (size_t i = 0; i < m.dim2(); i++) {
        auto& ri = m.row(i);
        res[i] = inner_product(ri, ri.end(), &v[0], double(0));
    }
    return res;
}
```

```cpp
valarray<double> operator*(valarray<double>& v, const Matrix& m)
{
    valarray<double> res(m.dim1());

    for (size_t i = 0; i < m.dim1(); i++) {
        auto& ci = m.column(i);
        res[i] = inner_product(ci, ci.end(), &v[0], double(0));
    }
    return res;
}
```

某些形式的 `inner_product` 被称为“点积”。

### 40.6.3 `partial_sum()` 和 `adjacent_difference()`

`partial_sum()` 和 `adjacent_difference()` 算法互为逆运算，处理增量变化的概念。

给定序列 `a`, `b`, `c`, `d` 等，`adjacent_difference()` 生成 `a`, `b−a`, `c−b`, `d−c` 等。

考虑一个温度读数的向量。我们可以像这样将它转换为温度变化向量：

```cpp
vector<double> temps;
void f()
{
    adjacent_difference(temps.begin(), temps.end(), temps.begin());
}
```

例如，17, 19, 20, 20, 17 变为 17, 2, 1, 0, −3。

反过来，`partial_sum()` 允许我们计算一组增量变化的最终结果：

```cpp
template<typename In, typename Out, typename BinOp>
Out partial_sum(In first, In last, Out res, BinOp op)
{
    if (first == last) return res;
    *res = *first;
    Tval = *first;
    while (++first != last) {
        val = op(val, *first);
        *++res = val;
    }
    return ++res;
}

template<typename In, typename Out>
Out partial_sum(In first, In last, Out res)
{
    return partial_sum(first, last, res, plus); // use std::plus (§33.4)
}
```

给定序列 `a`, `b`, `c`, `d` 等，`partial_sum()` 生成 `a`, `a+b`, `a+b+c`, `a+b+c+d` 等。

例如：

```cpp
void f()
{
    partial_sum(temps.begin(), temps.end(), temps.begin());
}
```

注意 `partial_sum()` 在通过 `res` 赋新值之前先递增 `res` 的方式。这允许 `res` 与输入序列相同；`adjacent_difference()` 的行为类似。
