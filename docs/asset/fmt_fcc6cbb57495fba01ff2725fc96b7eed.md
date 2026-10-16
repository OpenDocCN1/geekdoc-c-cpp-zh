
`va=a` 从 `a` 赋值；`a.size()` 必须等于 `va.size()`；`a` 可以是 `slice_array`、`gslice_array`、`mask_array` 或 `indirect_array`

`va@=va2` 对 `va` 的每个元素执行 `v[i]@=va2[i]`；`@` 可以是 `/`、`%`、`+`、`-`、`^`、`&`、`|`、`<<` 或 `>>`

`va@=t` 对 `va` 的每个元素执行 `v[i]@=t`；`@` 可以是 `/`、`%`、`+`、`-`、`^`、`&`、`|`、`<<` 或 `>>`

`valarray` 可以被赋给另一个相同大小的 `valarray`。正如所料，`v1=v2` 会将 `v2` 的每个元素复制到 `v1` 中对应的位置。如果 `valarray` 大小不同，则赋值的结果未定义。

除了这种常规赋值之外，还可以将标量赋给 `valarray`。例如，`v=7` 将 `7` 赋给 `valarray` `v` 的每个元素。这可能会让一些程序员感到惊讶，最好将其理解为运算符赋值操作的一种偶尔有用的退化情况。例如：

```
valarray<int> v {1,2,3,4,5,6,7,8};
v *=2; // v={2,4,6,10,12,14,16}
v=7; // v={7,7,7,7,7,7,7,7}
```

# 40.5.2 下标操作

下标操作可用于选择 `valarray` 的一个元素或其中的一个子集：

`valarray<T>` 下标操作（§iso.26.6.2.4、§iso.26.6.2.5）

`t=va[i]` 下标：`t` 是 `va` 第 `i` 个元素的引用；无范围检查

`a2=va[x]` 子集：`x` 是 `slice`、`gslice`、`valarray<bool>` 或 `valarray<size_t>`

每个 `operator[]` 都返回来自 `valarray` 的一个元素子集。返回类型（表示子集的对象类型）取决于参数类型。

对于 `const` 参数，结果包含元素的副本。对于非 `const` 参数，结果持有元素的引用。由于 C++ 不直接支持引用数组（例如，我们不能说 `valarray<int&>`），实现将以某种方式模拟这一点。这可以高效地完成。下面按顺序给出一个包含示例的详尽列表（基于 §iso.26.6.2.5）。在每种情况下，下标描述了要返回的元素，且 `v1` 必须是具有适当长度和元素类型的 `valarray`：

+   - 一个 `const valarray` 的切片：

```
valarray<T> operator[](slice) const;// copyofelements
// ...
const valarray<char> v0 {"abcdefghijklmnop",16};
```

```
valarray<char> v1 {v0[slice(2,5,3)]}; // {“cfjlo”,5}
```

+   - 非 `const valarray` 的切片：

```
slice_array<T> operator[](slice); // references to elements
// …
valarray<char> v0 {“abcdefghijklmnop”,16};
valarray<char> v1 {“ABCDE”,5};
v0[slice(2,5,3)] = v1; // v0 == {“abAdeBghCjkDmnEp”,16}
```

+   - `const valarray` 的 `gslice`：

```
valarray<T> operator[](const gslice&) const; // copies of elements
// …
const valarray<char> v0 {“abcdefghijklmnop”,16};
const valarray<size_t> len {2,3};
const valarray<size_t> str {7,2};
valarray<char> v1 {v0[gslice(3,len,str)]}; // v1 == {“dfhkmo”,6}
```

+   - 非 `const valarray` 的 `gslice`：

```
gslice_array<T> operator[](const gslice&); // references to elements
// …
valarray<char> v0 {“abcdefghijklmnop”,16};
valarray<char> v1 {“ABCDE”,5};
const valarray<size_t> len {2,3};
const valarray<size_t> str {7,2};
v0[gslice(3,len,str)] = v1; // v0 == {“abcAeBgCijDlEnFp”,16}
```

+   - `const valarray` 的 `valarray<bool>`（掩码）：

```
valarray<T> operator[](const valarray<bool>&) const; // copies of elements // …
const valarray<char> v0 {“abcdefghijklmnop”,16};
const bool vb[] {false, false, true, true, false, true};
valarray<char> v1 {v0[valarray<bool>(vb, 6)]}; // v1 == {“cdf”,3}
```

+   - 非 `const valarray` 的 `valarray<bool>`（掩码）：

```
mask_array<T> operator[](const valarray<bool>&); // references to elements // …
valarray<char> v0 {“abcdefghijklmnop”, 16};
valarray<char> v1 {“ABC”,3};
const bool vb[] {false, false, true, true, false, true};
v0[valarray<bool>(vb,6)] = v1; // v0 == {“abABC eghijklmnop”,16}
```

+   - `const valarray` 的 `valarray<size_t>`（索引集合）：

```
valarray<T> operator[](const valarray<size_t>&) const; // references to elements // …
const valarray<char> v0 {“abcdefghijklmnop”,16};
const size_t vi[] {7, 5, 2, 3, 8};
valarray<char> v1 {v0[valarray<size_t>(vi,5)]}; // v1 == {“hfcdi”,5}
```

+   - 非 `const valarray` 的 `valarray<size_t>`（索引集合）：

```
indirect_array<T> operator[](const valarray<size_t>&); // references to elements // ...
valarray<char> v0 {"abcdefghijklmnop",16};
valarray<char> v1 {"ABCDE",5};
const size_t vi[] {7, 5, 2, 3, 8};
v0[valarray<size_t>(vi,5)] {v1}; // v0={"abCDeBgAEjklmnop",16}
```

请注意，使用掩码（`valarray<bool>`）进行下标操作会产生 `mask_array`，而使用索引集合（`valarray<size_t>`）进行下标操作会产生 `indirect_array`。

# 40.5.3 操作

`valarray` 的目的是支持计算，因此直接支持大量基本数值操作：

# `valarray<T>` 成员操作（§iso.26.6.2.8）

`va.swap(va2)` 交换 `va` 和 `va2` 的元素；`noexcept`；`n=va.size()`，`n` 是 `va` 的元素个数

`t=va.sum()` `t` 是 `va` 的元素之和，使用 `+=` 计算；`t=va.min()` `t` 是 `va` 的最小元素，使用 `<` 查找；`t=va.max()` `t` 是 `va` 的最大元素，使用 `<` 查找

```
va2=va.shift(n)
va2=va.cshift(n)
va2=va.apply(f)
va.resize(n,t)
va.resize(n)
```

元素的线性右移

元素的循环右移

应用 `f`：每个元素 `va2[i]` 的值是 `va[f(i)]`。将 `va` 变为一个有 `n` 个元素、值为 `t` 的 `valarray`。`va.resize(n,T{})`

不进行范围检查：使用函数访问空 `valarray` 的元素的行为未定义。

注意 `resize()` 不会保留任何旧值。

# `valarray<T>` 操作（§iso.26.6.2.6、§iso.26.6.2.7）

`v` 或 `v2`（但不能同时）可以是标量；对于算术运算，结果是 `valarray<T>`。`swap(va,va2)` 即 `va.swap(va2)`

`va3=va@va2` 对 `va` 和 `va2` 的元素执行 `@` 运算，得到 `va3`；`@` 可以是 `+`、`-`、`*`、`/`、`%`、`&`、`|`、`^`、`<<`、`>>`、`&&`、`||`

`vb=v@v2` 对 `v` 和 `v2` 的元素执行 `@` 运算，得到一个 `valarray<bool>`；`@` 可以是 `==`、`!=`、`<`、`<=`、`>`、`>=`

`v2=@(v)` 对 `v` 的元素执行 `@()` 运算，得到 `v2`；`@` 可以是 `abs`、`acos`、`asin`、`atan`、`cos`、`cosh`、`exp`、`log`、`log10`。`v3=atan2(v,v2)` 对 `v` 和 `v2` 的元素执行 `atan2()` 运算

`v3=pow(v,v2)` 对 `v` 和 `v2` 执行 `pow()` 运算

`p=begin(v)` `p` 是指向 `v` 首元素的随机访问迭代器

`p=end(v)` `p` 是指向 `v` 末元素之后位置的随机访问迭代器

二元运算定义在 `valarray` 之间以及 `valarray` 与其标量类型的组合上。标量类型被视为一个大小合适、每个元素的值都等于该标量的 `valarray`。例如：

```cpp
void f(valarray<double>& v, valarray<double>& v2, double d)
{
valarray<double> v3 = v*v2; // v3[i] = v[i]*v2[i] for all i
valarray<double> v4 = v*d;  // v4[i] = v[i]*d for all i
valarray<double> v5 = d*v2; // v5[i] = d*v2[i] for all i
valarray<double> v6 = cos(v); // v6[i] = cos(v[i]) for all i
}
```

这些向量运算都会以 `*` 和 `cos()` 示例所示的方式对其操作数的每个元素执行相应运算。显然，只有当标量类型定义了相应运算时，该运算才能使用；否则，编译器在尝试特化该运算符或函数时会报错。

当结果是 `valarray` 时，其长度与其 `valarray` 操作数相同。如果两个数组的长度不同，则对两个 `valarray` 进行二元运算的结果未定义。

这些 `valarray` 运算返回新的 `valarray`，而不是修改其操作数。这可能开销较大，但在应用激进优化技术时未必如此。

例如，如果 `v` 是一个 `valarray`，可以这样缩放：`v *= 0.2`，以及：`v /= 1.3`。也就是说，将标量作用于向量，就是将标量作用于向量的每个元素。与往常一样，`*=` 比 `*` 和 `=` 的组合（§18.3.1）更简洁，也更容易优化。

注意，非赋值运算会构造一个新的 `valarray`。例如：

```cpp
double incr(double d) { return d+1; }

void f(valarray<double>& v) {
valarray<double> v2 = v.apply(incr); // produce incremented valarray
// ...
}
```

这不会改变 `v` 的值。遗憾的是，`apply()` 不接受函数对象（§3.4.3、§11.4）作为参数。

逻辑移位和循环移位函数 `shift()` 和 `cshift()` 返回一个新的 `valarray`，其中的元素被适当地移位，原数组保持不变。例如，循环移位 `v2=v.cshift(n)` 产生一个 `valarray`，使得 `v2[i]==v[(i+n)%v.size()]`。逻辑移位 `v3=v.shift(n)` 产生一个 `valarray`，若 `i+n` 是 `v` 的有效索引，则 `v3[i]` 等于 `v[i+n]`；否则结果为默认元素值。这意味着 `shift()` 和 `cshift()` 在参数为正时左移，参数为负时右移。例如：

```cpp
void f()
{
int alpha[] = { 1, 2, 3, 4, 5, 6, 7, 8 };
valarray<int> v(alpha,8); // 1, 2, 3, 4, 5, 6, 7, 8
```

```
valarray<int> v2 = v.shift(2); // 3, 4, 5, 6, 7, 8, 0, 0
valarray<int> v3 = v<<2; // 4, 8, 12, 16, 20, 24, 28, 32
valarray<int> v4 = v.shift(-2); // 0, 0, 1, 2, 3, 4, 5, 6
valarray<int> v5 = v>>2; // 0, 0, 0, 1, 1, 1, 1, 2
valarray<int> v6 = v.cshift(2); // 3, 4, 5, 6, 7, 8, 1, 2
valarray<int> v7 = v.cshift(-2); // 7, 8, 1, 2, 3, 4, 5, 6
}
```

对于 `valarray`，`>>` 和 `<<` 是位移位运算符，而不是元素移位运算符或 I/O 运算符。因此，`<<=` 和 `>>=` 可用于在整型的元素内移位。例如：

```
void f(valarray<int> vi, valarray<double> vd)
{
vi <<= 2; // vi[i] <<= 2 for all elements of vi
vd <<= 2; // error :shift is not defined for floating-point values
}
```

`valarray` 上的所有运算符和数学函数也可以应用于 `slice_arrays`（§40.5.5）、`gslice_arrays`（§40.5.6）、`mask_arrays`（§40.5.2）、`indirect_arrays`（§40.5.2）以及这些类型的组合。但是，允许实现在执行所需运算前，将不是 `valarray` 的操作数转换为 `valarray`。

# 40.5.4 切片

切片是一种抽象，它允许我们将一维数组（如内置数组、`vector` 或 `valarray`）高效地当作任意维度的矩阵来操作。它是 Fortran 向量和 BLAS（基本线性代数子程序）库的关键概念，后者是大量数值计算的基础。本质上，切片就是数组中某一部分里每隔 `n` 个元素取一个元素：

```
class std::slice {
// starting index, a length, and a stride
public:
slice(); // slice{0,0,0}
slice(size_t start, size_t size, size_t stride);

size_t start() const; // index of first element
size_t size() const; // number of elements
size_t stride() const; // element n is at start()+n*stride()
};
```

步长（`stride`）是切片中两个元素之间的距离（以元素个数计）。因此，切片描述了从非负整数到索引的一种映射。元素个数（`size()`）不影响该映射（寻址），但允许我们找到序列的末尾。这种映射可用来在一维数组（如 `valarray`）中高效、通用且相当方便地模拟二维数组。考虑一个 3×4 矩阵（三行，每行四个元素）：

```
valarray<int> v {
{00,01,02,03}, // row0
{10,11,12,13}, // row1
{20,21,22,23} // row2
};
```

或图形化表示：

00 01 02 03

10 11 12 13

20 21 22 23

遵循通常的 C/C++ 约定，`valarray` 在内存中按行元素优先（行优先顺序）且连续布局：

```
for (int x : v) cout << x << ' ';
```

这会产生：

```
01231011121320212223
```

或图形化表示：

列 0: 0 4 8

00 01 02 03 10 11 12 13 20 21 22 23 行0: 123

行 `x` 由 `slice(x*4,4,1)` 描述。也就是说，行 `x` 的第一个元素是向量的第 `x*4` 个元素，行的下一个元素是第 `(x*4+1)` 个，等等，每行有 4 个元素。例如，`slice{0,4,1}` 描述 `v` 的第一行（行 0）：00, 01, 02, 03，而 `slice{1,4,1}` 描述第二行（行 1）。

列 `y` 由 `slice(y,3,4)` 描述。也就是说，列 `y` 的第一个元素是向量的第 `y` 个元素，列的下一个元素是第 `(y+4)` 个，等等，每列有 3 个元素。例如，`slice{0,3,4}` 描述第一列（列 0）：00, 10, 20，而 `slice{1,3,4}` 描述第二列（列 1）。
