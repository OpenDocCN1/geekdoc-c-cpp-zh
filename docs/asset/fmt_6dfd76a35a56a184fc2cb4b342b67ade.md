
## 向后兼容性：`auto_ptr`

库的早期版本包含一个名为 `auto_ptr` 的类，它具有 `unique_ptr` 的某些但并非全部的属性。特别是，无法在容器中存储 `auto_ptr`，也无法从函数返回它。

尽管 `auto_ptr` 仍然标准库的一部分，但程序应该使用 `unique_ptr` 代替。

### 向 `unique_ptr` 传递删除器

与 `shared_ptr` 一样，默认情况下，`unique_ptr` 使用 `delete` 来释放 `unique_ptr` 指向的对象。对于 `shared_ptr`，我们可以在 `unique_ptr` 中覆盖默认删除器（§ 12.1.4, p. 468）。然而，由于我们在 § 16.1.6 (p. 676) 中描述的原因，`unique_ptr` 管理删除器的方式与 `shared_ptr` 不同。

在 `unique_ptr` 中覆盖删除器会影响 `unique_ptr` 类型，也会影响我们构造（或重置）该类型对象的方式。类似于覆盖关联容器的比较操作（§1.2.2, p.425），我们必须在尖括号内提供删除器类型，以及 `unique_ptr` 可以指向的类型。当我们创建或重置一个对象时，提供一个指定类型的调用对象：

```cpp
// p 指向类型为 objT 的对象，使用类型为 delT 的对象来释放它
unique_ptr<objT, delT> p(new objT, fcn);
```

作为一个更具体的例子，我们将重写连接程序，使用 `unique_ptr` 代替 `shared_ptr`：

```cpp
void f(destination d /* 其他参数 */)
{
    connection c = &d; // 打开连接
    // 当 p 被毁时，连接将关闭
    unique_ptr<connection, decltype(end_connection)> p(c, end_connection);
}
// 当 f 退出时，即使发生异常，连接也将正确关闭
```

在这里我们使用 `decltype` (§2.5) 来指定指针类型。因为 `decltype(end_connection)` 返回一个类型，我们必须加上 `*` 表示我们正在使用该类型的指针 (§6.7.)

## 练习 12.1.5

**练习 12.16：** 如果尝试拷贝或赋值 `unique_ptr`，编译器并不总是给出易于理解的信息。编写一个包含这些错误的程序，查看编译器如何诊断它们。

**练习 12.17：** 下列哪些 `unique_ptr` 声明是非合法的或可能导致错误的？解释每种情况的问题。

```cpp
int ix = 10, *pi = &ix, *pi2 = new int(20);
unique_ptr<int> p;
(a) p0(ix);
(b) p1(pi);
(c) p2(pi2);
(d) p3(&ix);
(e) p4(new int(20));
(f) p5(pi2.get());
```

**练习 12.18：** 为什么 `shared_ptr` 没有 `release` 成员？

## 12.1.6. `weak_ptr`

`weak_ptr` 是一种智能指针，它不控制其指向对象的生命周期。相反，`weak_ptr` 指向由 `shared_ptr` 管理的对象。将 `weak_ptr` 绑定到 `shared_ptr` 不改变 `shared_ptr` 的引用计数。一旦指向该对象的最后一个 `shared_ptr` 消失，该对象将被删除。这捕捉了 `weak_ptr` “弱”共享对象的思想。

### 表 12.5. `weak_ptr`

| `weak_ptr<T>` | 可以指向类型 T 对象的空 `weak_ptr`。 |

| `weak_ptr<T> w(sp)` | 指向与 `shared_ptr` `sp` 相同对象的 `weak_ptr`。T 必须转换为 `sp` 指向的类型。 |

| `w = p` | `p` 可以是 `shared_ptr` 或 `weak_ptr`。赋值后 `w` 与 `p` 共享所有权。 |

| `w.reset()` | 使 `w` 置空。 |

| `w.use_count()` | 与 `w` 共享所有权的 `shared_ptr` 数量。如果 `w.use_count()` 为零返回 true，否则返回 false。 |

| `w.lock()` | 如果过期，返回空 `shared_ptr`；否则返回 `w` 指向对象的 `shared_ptr`。 |

当我们创建一个 `weak_ptr` 时，从 `shared_ptr` 初始化它：

```cpp
auto p = make_shared<int>(42);
weak_ptr<int> wp(p); // wp 与 p 弱共享；p 中的引用计数保持不变
```

在这里，`wp` 和 `p` 指向同一个对象。由于共享是弱的，`wp` 不会改变 `p` 的引用计数；`wp` 指向的对象可能会被删除。

由于对象不再存在，我们无法使用 `weak_ptr` 直接访问其对象。要访问它，必须调用 `lock`。`lock` 函数检查 `weak_ptr` 指向的对象是否存在。如果是，`lock` 返回一个指向共享对象的 `shared_ptr`。与任何其他 `shared_ptr` 一样，我们保证只要 `shared_ptr` 存在，它指向的底层对象就会继续存在。例如：

```cpp
if (shared_ptr<int> np = wp.lock()) { // 如果 np 不为空则为
    // 在 if 内部，np 与 p 共享其对象
}
```

在这里，只有在 `lock` 调用成功时我们进入 if 的体。在 if 内部，使用 `np` 访问该对象是安全的。

## 检查指针类

为了说明 `weak_ptr` 的用处，我们将为 `StrBlob` 定义一个辅助指针类，命名为 `StrBlobPtr`。我们的指针类将存储一个指向初始化它的 `StrBlob` 数据成员的 `weak_ptr`。通过使用 `weak_ptr`，我们不会影响特定 `StrBlob` 所指向的 `vector` 的生命周期。然而，我们可以防止用户尝试访问已不存在的 `vector`。

`StrBlobPtr` 有两个数据成员：`wptr` 和 `curr`，`curr` 是该对象当前表示的元素的索引。与其伴侣 `StrBlob` 类一样，我们的指针类有一个 `check` 成员，用于验证解引用 `StrBlobPtr` 是安全的：

```cpp
// StrBlobPtr 在尝试访问不存在的元素时抛出异常
class StrBlobPtr {
public:
    StrBlobPtr(): curr(0) { }
    StrBlobPtr(const StrBlob&, size_t sz = 0):
        wptr(a.data), curr(sz) { }
    std::string& deref() const;
    StrBlobPtr& incr(int n); // 前缀版本
private:
    // 如果检查成功，返回指向 vector 的 shared_ptr
    std::shared_ptr<std::vector<std::string>> check(size_t size, const std::string& s) const;
    // 存储 weak_ptr，这意味着底层 vector 可能被销
    std::weak_ptr<std::vector<std::string>> wptr;
    size_t curr; // 数组中的当前位置
};
```

默认构造函数生成一个空的 `StrBlobPtr`。它的构造函数初始化列表（§ 7.1.4, 265）将 `curr` 初始化为 0，并隐含 `wptr` 为空指针。第二个构造函数接受一个 `StrBlob` 的引用和一个可选的索引值。该构造函数将 `wptr` 初始化为指向共享 `StrBlob` 对象中的 `vector`，并将 `curr` 初始化为 `sz` 的值。

# C++ Primer 第五版

我们使用默认参数 (§ 6.5.1, p. 236) 来初始化 `curr`，使其默认指向第一个元素。正如我们将看到的，`sz` 参数将由 `StrBlob` 的 `end` 成员使用。

值得注意的是，我们不能将 `StrBlobPtr` 绑定到 `const StrBlob` 对象。这一限制是因为构造函数接收的是一个非 `const` 类型 `StrBlob` 的引用。

`StrBlobPtr` 的 `check` 成员与 `StrBlob` 中的不同，因为它必须检查它指向的 `vector` 是否仍然存在。

点击此处查看代码图像

```cpp
std::shared_ptr<std::vector<std::string>>
StrBlobPtr::check(std::size_t i, const std::string& msg)
const
{
    auto ret = wptr.lock(); // vector 还在吗？
    if (!ret)
        throw std::runtime_error("unbound StrBlobPtr");
    if (i >= ret->size())
        throw std::out_of_range(msg);
    return ret; // 否则，返回指向 vector 的 shared_ptr
}
```

由于 `weak_ptr` 不参与其对应的 `shared_ptr` 的引用计数，该 `StrBlobPtr` 可能指向已经被删除的 `vector`。如果 `vector` 已消失，`lock` 将返回空指针。在任何情况下，对 `vector` 的任何引用都会失败，因此我们将抛出一个异常。否则，`check` 会验证给定的索引。如果该值有效，`check` 返回从 `lock` 获取的 `shared_ptr`。

# 指针操作

我们将在第14章学习如何定义我们的 `deref` 和 `incr` 运算符。目前，我们分别定义了函数 `deref` 来解引用和递增 `StrBlobPtr`。

`deref` 成员调用 `check` 来验证使用 `vector` 是安全的，并且 `curr` 在范围内：

点击此处查看代码图像

```cpp
std::string& StrBlobPtr::deref() const
{
    auto p = check(curr, "dereference past end");
    return (*p)[curr]; // (*p) 是该对象指向的 vector
}
```

如果 `check` 成功，`p` 就是指向该 `StrBlobPtr` 所指向 `vector` 的 `shared_ptr`。表达式 `(*p)[curr]` 解引用 `shared_ptr` 以获取 `vector`，并使用下标运算符获取并返回位于 `curr` 处的元素。

`incr` 成员也调用了 `check`：

点击此处查看代码图像

```cpp
// 前缀：返回递增对象的引用
StrBlobPtr& StrBlobPtr::incr()
{
    // 如果 curr 已经指向容器之外，则无法递增
    check(curr, "increment past end of StrBlobPtr");
    ++curr; // 推进当前状态
    return *this;
}
```

为了访问数据成员，我们的指针类必须是 `StrBlob` 的友元类 (§7.3.4, p. 279)。我们将为 `StrBlob` 类提供 `begin` 和 `end` 操作，返回指向以下位置的 `StrBlobPtr`：

点击此处查看代码图像

```cpp
// StrBlob 中的友元声明需要前置声明
class StrBlobPtr;
class StrBlob {
    friend class StrBlobPtr;
    // 其他成员见 §12.2.1 (p. 456)
    // 返回指向第一个元素和最后一个元素之后元素的 StrBlobPtr
    StrBlobPtr begin() { return StrBlobPtr(*this); }
    StrBlobPtr end() {
        auto ret = StrBlobPtr(*this, data->size());
        return ret; }
}
```

# 练习 12.1.6

**练习 12.19：** 定义你自己的版本的 `StrBlobPtr`，并使用相应的友元声明以及 `begin` 和 `end` 成员来更新你的 `StrBlob` 类。

**练习 12.20：** 编写一个程序，每次读取一个输入文件到 `StrBlob` 中，并使用 `StrBlobPtr` 打印该 `StrBlob` 中的每个元素。

**练习 12.21：** ways这样写 `StrBlobPtr` 的 `deref` 成员：

点击此处查看代码图像

```cpp
std::string& deref() const { return (*check(curr, "dereference past end"))[curr]; }
```

你认为哪种版本更好？为什么？

# 练习 12.22：为了创建一个可以与名为 `ConstStrBlobPtr` 的 `const StrBlob` 使用的类，需要对新的 `StrBlobPtr` 做出哪些修改？

# 12.2. 动态数组

一次分配一个对象。某些应用程序需要能够一次性为许多对象分配存储。例如，`vector` 和 `string` 将元素存储在连续内存中，当容器必须重新分配时，必须一次性分配多个元素 (§ 9.4, p. 355)。

为了支持这种用法，语言和库提供了两种新表达式，用于分配和初始化对象数组。库包含一个模板类 `allocator`，它允许我们将分配与初始化隔离开。由于我们将在 § 12.2.2 (p. 481) 中解释的原因，分配器通常能提供更好的性能和更灵活的内存管理。

然而，许多应用程序不需要动态数组。当应用程序需要数量数量的对象时，像我们处理 `StrBlob` 那样做总是更容易、更快且更安全：使用 `vector`（或其他库容器）。由于我们将在 § 13.6 (p. 531) 中解释的原因，使用容器的优势是显著的。

**最佳实践**

大多数应用程序应该使用容器而不是动态数组。

**警告**

不要分配动态数组。

### 12.2.1. 数组

我们使用 `new` 通过指定大小来分配对象数组。在这种情况下，`new` 返回一个指向元素类型的指针。

# 分配数组产生元素类型

尽管将 `new[]` 分配的内存称为“动态数组”很常见，但这种用法是有误导性的。当我们使用 `new` 分配数组时，我们得到的并不是数组类型。相反，我们得到的是指向元素类型的指针。

当初始化内置数组对象 (§ 3.5.1, 114) 时，如果初始化器较少，剩余元素将进行值初始化。通过在大小后紧跟空括号，我们可以对数组元素进行值初始化。由于分配的内存没有数组类型，我们不能使用 `auto` 来分配数组 (§ 12.1.2, p. 459)。

# 初始化动态对象数组

默认情况下，由 `new` 分配的对象——无论是作为单个对象还是数组分配的——都是默认初始化的。我们可以通过在大小后紧跟空括号来对数组中的元素进行值初始化 (§ 3.3.1, 98)。

点击此处查看代码图像

```cpp
int *p1 = new int[10]; // 十个未初始化的 int 块
int *pla2 = new int[10](); // 十个值初始化的块
```

根据标准，我们还提供了一个元素初始化器的列表列表：

点击此处查看代码图像

```cpp
// 十个 int 块，每个都从相应的初始化器初始化
int *pia3 = new int[10]{0,1,2,3,4,5,6,7,8,9};
```

```cpp
string *psa3 = new string[10]{"a", "an", "the",
string(3,'x')};
```

我们可以使用任意表达式来确定要分配对象的数量：

# 点击此处查看图片

```
size_t n = get_size(); // get_size 返回所需的元素数量
int* p = new[n]; // 分配一个数组来存放元素
for (int* q = p; q != p + n; ++q)
/* process the array * // ;
```

一个有趣的问题随了：如果 `get_size` 返回 0 会发生什么？答案是我们的代码可以运行。尽管我们无法创建一个大小为 0 的数组变量，但 `n` 等于 0 的 `new[n]` 是合法的：

# 点击此处查看图片

```
char arr[0]; // error：不能定义长度为零的数组
char *cp = new char[0]; // ok：但不能进行解引用
```

当我们使用 `new` 分配大小为零的数组时，它返回一个有效的非零指针。该指针保证与 `new` 返回的任何其他指针不同。该指针充当零元素数组的越界指针 ([3.5.3, 119])。我们可以像使用越界迭代器一样使用该指针。该指针可以在上面的循环中进行比较。我们可以对该指针加上零（或减去零），并从指针本身减去指针，使区域清零。该指针不能被解引用——它指向任何地方。

在我们的假设情况下，如果 `get_size` 返回 0，那么 `n` 也是 0。`new` 将分配零个对象。`for` 循环中的条件将失败（因为 `n` 为 0，`p` 等于 `q + n`）。因此，循环体不会执行。

## 释放动态数组

要释放动态数组，我们使用特殊形式的 `delete`，它包含一对空方括号：

# 点击此处查看图片

```
delete p; // p 必须指向动态分配的对象或空
delete [] pa; // pa 必须指向动态分配的数组或空
```

第二个语句会破坏 `pa` 所向数组中的元素并释放相应的内存。数组中的元素按逆序销毁。也就是说，最后一个元素先被销毁，然后是倒数第二个，以此此类推。
