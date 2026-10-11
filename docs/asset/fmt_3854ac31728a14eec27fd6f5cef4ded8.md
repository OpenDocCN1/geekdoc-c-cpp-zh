
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
- 5 返回下标数组的引用，该引用有效直到为数组调用成员函数 `resize(size_t, T)` [29.7.2.8] 或数组的生命周期结束，以先发生者为准。

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

- 9 返回：包含 `indirect` 元素的 `valarray`。

# ISO/IEC 14882:2017(E)

```cpp
explicit valarray(size_t n);
```

影响：构造一个长度为 `n` 的 `valarray`。数组的每个元素都经过值初始化（11.6）。

```cpp
valarray(const T& v, size_t n);
```

影响：构造一个长度为 `n` 的 `valarray`。数组的每个元素都用 `v` 初始化。

```cpp
valarray(const T* p, size_t n);
```

要求：`p` 指向一个至少包含 `n` 个元素的数组（11.3.4）。
影响：构造一个长度为 `n` 的 `valarray`。数组的每个元素都用第一个参数所指向的前 `n` 个值进行初始化。

```cpp
valarray(const valarray& v);
```

影响：构造一个长度与 `v` 相同的 `valarray`。元素用 `v` 对应元素的值初始化。

```cpp
valarray(valarray&& v) noexcept;
```

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
