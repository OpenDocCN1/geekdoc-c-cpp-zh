
```cpp
template <typename T> void g(T&& val);
int i = 0; const int ci = i;
```

- (a) `g(i)`;

- (b) `g(ci)`;

- (c) `g(i * ci)`;

练习 16.43：使用上一个练习中定义的函数，如果我们调用 `g(i = ci)`，`g` 的模板参数将会是什么？

**练习 16.44：** 使用与第一个练习相同的三个调用，如果 `g` 的函数参数声明为 `T`（而不是 `T&&`），请确定 `T` 的类型。

**练习 16.45：** 给定以下模板，解释如果对 42 之类的字面值调用 `g` 会发生什么。如果我们对 `int` 类型的变量调用 `g` 会怎样？

点击此处查看代码图像

```cpp
template <typename T> void g(T& val) { vector<T> v; }
```

# 16.2.6. 理解 std::move

![](img/3a7e14b77396239ca7166fc2adb32975_851_0.png)

*move* 函数（§ 13.6.1，第 533 页）是使用值引用的模板的良好示例。幸运的是，我们可以在不理解它所使用的模板机制的情况下使用 *move*。然而，观察 *move* 的工作原理有助于巩固我们对模板的通用理解和使用。

在 § 13.6.2 (534) 中我们发现，虽然我们不能直接将右值绑定到左值，但可以使用 *move* 获取一个绑定到左值的 r 引用。由于 *move* 可以接受本质上任何类型的参数，*move* 是一个函数模板这并不令人意外。

## std::move 如何定义

标准定义了 *move* 如下：

点击此处查看返回类型中的 typename 见 § 16.1.3 (第 670 页)

```cpp
// 返回类型中的 typename 见 § 16.1.3 (第 670 页)
// remove_reference 见 § 16.2.3 (第 684 页)
template <typename T>
remove_reference<T>::type&& move(T&&)
{
    // static_cast 见 § 4.11.3 (第 163 页)
    return static_cast<typename remove_reference<T>::type&&>(t);
}
```

这段代码很短但微妙。首先，*move*' 的函数参数 `T&&` 是右值的引用。通过引用折叠，该参数可以匹配任何类型。特别是，我们可以向 *move* 传递左值或右值：

点击此处查看代码图像

```cpp
string s1("hi"), s2;
s2 = std::move("bye!"); // 正确：从右值移动
s2 = std::move(s1); // 正确：赋值后 s1 
```

# std::move 如何工作

在第一次赋值中，`move` 的参数是 `string("bye")` 的右值。正如我们看到的，当我们向 r 引用传递右值时，从该右值推导出的引用的类型（见 6.2.5，第 687 页）。因此在 `std::move("bye!")` 中：

- 推导的类型是 `string`。
- 因此，`remove_reference` 使用 `string` 实例化。
- `remove_reference<string>` 的成员类型是 `string`。
- `move` 的返回类型是 `string&&`。
- 相应地，这实例化了 `move<string>`，其为 `string&&(string&&)`

该函数的体返回 `static_cast<string&&>(t)`。`t` 的类型已经是 `string&&`，因此没有代价。

现在考虑第二次赋值 `std::move(s1)`。在这次调用中，`move` 的参数是左值。此时：

- 推导的类型是 `string&`（string 的引用而非 string）。
- 因此，`remove_reference` 使用 `string&` 实例化。
- `remove_reference<string&>` 的成员类型是 `string&`。
- `move` 的返回类型是 `string&&`。
- `move` 的函数参数 `t` 实例化为 `string&`，折叠为 `string&`。

因此，这次调用实例化了 `move<string&>`，其为：

```cpp
string&& move(string &&t)
```

这正是我们想要的——我们想要将右值引用绑定到左值。该实例实例化体返回 `static_cast<string&&>(t)`。在这种情况下，`t` 的类型是 `string&`，转换为 `string&&`。

# 允许从左值 static_cast 到右值

通常情况下，`static_cast` 只能执行合法的转换（见 4.11.3，第 163 页）。然而，对于右值引用再次有一个例外：尽管我们不能隐式地将左值转换为右值引用，但可以使用 `static_cast` 显式地将左值转换为右值引用。

![](img/3a7e14b77396239ca7166fc2adb32975_853_0.png)

将右值引用绑定到左值允许修改左值。在某些情况下，例如在我们 § 13.6.1（第 533 页）的 `StrVec::reallocate` 函数中，我们知道修改左值是安全的。通过允许这样做，语言允许这种用法。强制我们使用转换防止我们意外这样做。

最后，尽管我们可以直接编写此类内容，但使用库的 `move` 函数要容易得多。此外，一致地使用 `std::move` 有于找到代码中可能修改左值的地方。

# 第 16.2.6 节练习

- **练习 16.46：** 解释：来自 § 13.5（第 530 页）的 `StrVec::reallocate` 中的循环：

点击此处查看代码图像

```cpp
for (size_t i = 0; i != size(); ++i)
    alloc.construct(dest++, std::move(*elem++));
```

# 16.2.7. 转发

![](img/3a7e14b77396239ca7166fc2adb32975_853_1.png)

某些函数需要将其一个或多个参数转发给未被转发函数改变的类型。在这种情况下，我们需要保留参数的所有信息，包括参数类型是否为 `const`，以及参数是左值还是右值。

例如，我们将编写一个接受可调用表达式和两个额外参数的函数。我们的函数将以相反顺序向可调用对象提供另外两个参数。以下是 `flip` 函数的初步尝试：

点击此处查看代码图像

```cpp
// 接受可调用对象和两个参数的模板
// 并用翻转后的参数调用给定的可调用对象
// flip1 是不完整的实现：顶层 const 和引用丢失了
```

```cpp
template <typename F, typename T1, typename T2>
void flip(F f, T1 t1, T2 t2)
{
    f(t2, t1);
}
```

这个模板运行良好，直到我们想要使用它调用一个具有引用参数的函数：

# 点击此处查看图像

```cpp
void f(int v1, int &v2) // 注意 v2 是一个引用
{
    cout << v1 << " " << v2 << endl;
}
```

`f` 改变了 `v2` 的值。然而，如果我们通过 `flip1` 调用 `f`，`f` 所所的改变不会影响原始参数：

```cpp
f(42, i); // f 改变 i
flip1(f, j); // 通过 flip1 调用 f，j 保持不变
```

问题在于 `j` 被传递给了 `flip1` 的 `t1` 参数。该参数是普通的非引用类型 `int` 而不是 `int&`。因此，这次调用 `flip1` 的实例化为：

```cpp
void flip1(void(*fcn) (int, int&), int t1, int t2);
```

`j` 的值被拷贝到 `t1`。`f` 的引用参数绑定到 `t1` 而不是 `j`。

# 定义保留类型的函数参数

为了通过我们的 `flip` 函数传递引用，我们需要重写我们的函数，使其参数保留参数的“值值性”。再往前想一下，想象我们还想保留参数的常量性。

通过将相应的函数参数定义为对模板参数的引用，我们可以保留参数中的所有类型信息，因为引用类型中的 `const` 是底层的。通过引用折叠（见 16.2.5，第 688 页），如果我们将函数参数定义为 `T1&&` 和 `T2&&`，就可以保留 `flip` 参数的左值/右值属性（见 16.2.5，第 687 页）：

# C++ Primer 第五版

```cpp
template <typename F, typename T1, typename T2>
void flip2(F f, T1 &&t1, T2 &&t2)
{
    f(t2, t1);
}
```

正如我们之前的通话中所说的，如果我们调用 `flip2(f, j, 42)`，左值 `j` 被传递给参数 `t1`。但在 `flip2` 中，为 `T1` 推导出的类型是 `int&`，这意味着 `t1` 的类型折叠为 `int&`。引用 `t1` 绑定到 `j`。当 `flip2` 调用 `f` 时，`f` 中的引用参数 `v2` 绑定到 `t1`，而 `t1` 又绑定到 `j`。当 `f` 增加 `v2` 时，它改变的是 `j` 的值。

> 注意

作为模板参数右值用的函数参数（即 `T&`）保留其对应参数的常量属性以及左值/右值属性。

这个版本的 `flip2` 解决了我们的一半问题。`flip` 函数对于接受左值引用的函数运行良好，但不能用于调用具有右值引用参数的函数。例如：

点击此处查看代码图片

```cpp
void g(int &&i, int &j)
{
    cout << i << " " << j << endl;
}
```

如果我们尝试通过 `flip2` 调用 `g`，我们将把参数 `t2` 传递给 `g` 的右值引用参数。即使我们向 `flip2` 传递一个右值：

点击此处查看代码图片

```cpp
flip2(g, i, 42); // ：无法从左值初始化 int&
```

传递给 `g` 的也将是 `flip2` 内部的参数 `t2`。函数参数像任何变量一样是一个表达式（§ 13.6.1, p. 533）。因此，`flip2` 中对 `g` 的调用向 `g` 的右值引用参数传递了一个左值。

### 使用 std::forward 在调用中保留类型信息

我们可以使用一个名为 `forward` 的新库，以保留原始参数类型的方式传递 `flip2` 的参数。与 `move` 类似，`forward` 定义在 `<utility>` 头文件中。与 `move` 不同，`forward` 必须带有显式的模板参数调用（§ 16.2.2, p. 682）。`forward` 返回指向该显式参数类型的右值引用。也就是说，`forward<T>` 的返回类型是 `T&`。

通常，我们使用 `forward` 传递定义为右值用的函数参数。通过其返回类型上的引用折叠，`forward` 保留了给定参数的左值/右值本质：

点击此处查看代码图片

```cpp
template <typename Type> intermediary(Type &&arg)
{
    finalFn(std::forward<Type>(arg));
}
//...
```

在这里，我们使用了从 `arg` 推导出的 `forward` 显式模板参数类型。由于 `arg` 是模板参数的右值引用，`Type` 将代表传递给 `arg` 的参数的所有类型信息。如果该参数是右值，那么 `Type` 就是普通的（非引用）类型，`forward<Type>` 将返回 `Type&&`。如果参数是左值，那么通过引用折叠，`Type` 本身就是左值引用。在这种情况下，返回类型是左值引用类型的右值引用。再次通过引用折叠——这次是在返回类型上——`forward<Type>` 将返回左值引用类型。

> 注意

当与模板类型参数（`T&&`）的右值函数参数配合时，`forward` 保留关于参数类型的所有细节。

使用 `forward`，我们再次重写了 `flip` 函数：

点击此处查看代码图片

```cpp
template <typename F, typename T1, typename T2>
void flip(F f, T1 &&t1, T2 &&t2)
{
    f(std::forward<T2>(t2), std::forward<T1>(t1));
}
```

如果我们调用 `flip(g, i, 42)`，`i` 将作为 `int&` 传递给 `g`，`42` 将作为 `int&&` 传递。

> 注意

与 `std::move` 一样，不为 `std::forward` 提供 `using` 声明是一个好主意。§18.2.3 (p. 798) 将解释原因。

# 16.3. 模板重载

函数模板可以被其他模板或普通的非模板函数重载。和通常一样，同名的函数必须在参数的数量或类型上有所不同。

### 练习题章节 16.2.7

**练习题 16.47：** 编写你自己的 `flip` 函数版本，并通过调用具有左值和右值引用参数的函数来测试它。

函数匹配（§ 6.4, 233）受函数模板存在的影响：

- 调用的候选函数包括任何模板参数推导（§ 16.2, 678）成功的函数模板实例化。
- 候选函数模板始终是可用的，因为模板参数推导已经消除了任何不可用的模板。
- 同样如往常一样，可用的函数（模板和非模板）根据为了该调用所需的转换（如果有的话）进行排序。当然，调用函数模板时使用的转换是非常有限的（§ 16.2.1, p. 679）。
- 同样如往常，如果恰好有一个函数比其他任何函数都提供更好的匹配，则选择该函数。然而，如果有多个更好的匹配，则调用是歧义的。

> 警告

正确地定义重载模板需要理解模板。

## 编写重载模板

作为一个示例，我们将构建一组 `debug_rep` 函数。首先，我们定义一个接受引用的版本：

```cpp
template <typename T> string debug_rep(const T &t)
{
    ostringstream ret;
    ret << "address: " << &t;
    return ret.str();
}
```

接下来，我们定义一个接受指针的版本：

```cpp
template <typename T> string debug_rep(T *p)
{
    ostringstream ret;
    if (p)
        ret << "value: " << *p;
    else
        ret << "null pointer";
    return ret.str();
}
```

最后，我们定义一个接受右值的版本：

```cpp
template <typename T> string debug_rep(T&&)
{
    ostringstream ret;
    ret << "rvalue: " << t; // 注意：此处原文应为 t，但逻辑为 rvalue
    return ret.str();
}
```

我们可以这样使用这些函数：

```cpp
string s("hi");
cout << debug_rep(s) << endl;
```

对于这次调用，只有第一个版本的 `debug_rep` 是可用的。第二个版本 `debug_rep` 需要指针类型，而在调用中传递了一个非指针对象。参数推导失败。由于只有一个可用的函数，它就是被调用的。

如果我们用指针调用 `debug_rep`：

```cpp
cout << debug_rep(&s) << endl;
```

两个函数都生成了可用实例化：

- `debug_rep(const string&)`，`T` 绑定到 `string*` 的第一个版本实例化
- `debug_rep(string*)`，`T` 绑定到 `string` 的第二个版本实例化

第二个版本 `debug_rep` 的实例化对于这次调用是精确匹配。第一个版本的实例化需要将普通指针转换为常量指针。普通函数匹配应该优选择第二个模板，事实上的运行的也是它。

## 多个可用模板

作为另一个示例，考虑以下调用：

```cpp
const string *sp = &s;
cout << debug_rep(sp) << endl;
```

在这里两个都是用的且提供了精确匹配：

- `debug_rep(const string*&)`，`T` 绑定到 `const string*` 的第一个版本实例化
- `debug_rep(const string*)`，`T` 绑定到 `const string` 的第二个版本实例化

在这种情况下，普通函数匹配无法区分这两个调用。我们可能认为这次调用是歧义的。然而，由于重载函数模板的特殊规则，它解析为 `debug_rep(T*)`，这是更具特性的模板。

该规则的原因是，如果没有它，将无法对常量指针调用指针。问题是模板 `debug_rep(const T&)` 几乎可以对任何类型调用，包括指针类型。该模板比 `debug_rep(T*)` 更通用，后者只能对指针类型调用（此处原文截断）

关于指针类型。如果没有这条规则，传递给 `const` 指针的调用将始终具有歧义。

> 注意

> 当有多个重载模板为调用提供同等良好的匹配时，将优先选择最特化化的版本。

## 非模板与模板重载

在下一个示例中，我们将定义一个 `debug_rep` 的普通非模板版本，用于打印双引号内的字符串：

点击此处查看代码图片

```
// 打印双引号内的字符串
string debug_rep(const string&s)
{
    return "\"" + s + "\"";
}
```

现在，当我们对一个字符串调用 `debug_rep` 时，

点击此处查看代码图片
