

## 9.6. 修订赋值运算符

```cpp
{
    Strings tmp(other);
    // more to follow
    return *this;
}
```

你可能会觉得 `operator=(Strings tmp)` 这种优化很有吸引力，但让我们先把这个问题放一放（至少等到 9.7 节再说）。

既然我们已经完成了复制部分，那么删除部分呢？是不是还有另一个小问题？毕竟我们确实完成了复制，但并不是复制到我们原本打算的对象（当前对象 `*this`）中。

这时，是时候引入*交换*了。交换两个变量意味着这两个变量互换各自的值。下一节我们会详细讨论交换，但现在先假设我们已经为 `Strings` 类添加了一个成员 `swap(Strings &other)`。这样就可以完成 `Strings` 的 `operator=` 实现了：

```cpp
Strings &operator=(Strings const &other)
{
    Strings tmp(other);
    swap(tmp);
    return *this;
}
```

这个 `operator=` 的实现具有通用性：它可以应用于任何对象可交换的类。它是如何工作的呢？

-   用 `other` 对象中的信息来初始化局部对象 `tmp`。这负责了赋值运算符的复制部分；
-   调用 `swap` 确保当前对象获得其新值（而 `tmp` 则获得当前对象原来的值）；
-   当 `operator=` 终止时，局部对象 `tmp` 不复存在，其析构函数会被调用。由于此时 `tmp` 包含的是当前对象先前拥有的数据，当前对象的原始数据随之被销毁，从而完成了赋值操作中的销毁部分。

不错吧？

### 9.6.1 交换

许多类（例如 `std::string`）都提供了 `swap` 成员，允许我们交换其两个对象。*标准模板库*（STL，参见第 18 章）提供了各种与交换相关的函数。甚至还有一个 `swap` 通用算法（参见 19.1.61 节），它通常使用赋值运算符实现。在为我们的 `Strings` 类实现 `swap` 成员时，如果 `Strings` 的所有数据成员都可以交换，那么该算法就可以使用。由于这一点是成立的（*为什么*成立稍后会讨论），我们可以为 `Strings` 类添加一个 `swap` 成员：

```cpp
void Strings::swap(Strings &other)
{
    swap(d_string, other.d_string);
    swap(d_size, other.d_size);
}
```

将这一成员添加到 `Strings` 后，就可以使用 `Strings::operator=` 的 copy-and-swap 实现了。

![](img/859c398c8f9601f32700b78894504b0a_188_0.png)

*图 9.3：交换链表*

当两个变量（例如 `double one` 和 `double two`）交换时，交换后各自持有对方的值。因此，如果 `one == 12.50` 且 `two == -3.14`，那么执行 `swap(one, two)` 后，`one == -3.14`，`two == 12.50`。

基本数据类型的变量（指针和内置类型）可以交换；类类型对象如果其类提供了 `swap` 成员，也可以交换。

那么，我们应该为类提供 `swap` 成员吗？如果要提供，又该如何实现呢？

上面的例子（`Strings::swap`）展示了实现 `swap` 成员的标准方式：依次交换它的每个数据成员。但有些情况下，即使类只定义了基本数据类型的成员，也无法用这种方式实现 `swap` 成员。请考虑图 9.3 所示的情形。

图中包含四个对象，每个对象都有一个指向下一个对象的指针。这种类的基本结构如下：

```cpp
class List
{
    List *d_next;
    ...
};
```

初始时，四个对象的 `d_next` 指针分别指向下一个对象：1 指向 2，2 指向 3，3 指向 4。这显示在图的上半部分。下半部分显示的是对象 2 和对象 3 交换后的情况：对象 3 的 `d_next` 指针现在位于对象 2，而对象 2 仍然指向 4；对象 2 的 `d_next` 指针指向对象 3 的地址，但对象 2 的 `d_next` 现在位于对象 3 中，因此它指向自身。糟糕！

另一种对象交换出错的情况是，类的数据成员指向或引用同一对象的其他数据成员。图 9.4 展示了这种情形。

这里的对象有两个数据成员，如下面的类定义所示：

```cpp
class SelfRef
{
    size_t *d_ownPtr;      // initialized to &d_data
    size_t d_data;
};
```

图 9.4 的上半部分展示了两个对象；它们的上层数据成员指向各自的下层数据成员。但如果交换这两个对象，就会遇到图中下半部分的情形。此处地址 a 和地址 c 处的值被交换，于是它们不再指向各自的下层数据成员，而是突然指向了另一个对象的数据成员。又一个坏消息。

![](img/859c398c8f9601f32700b78894504b0a_189_0.png)

*图 9.4：自引用数据对象的交换*

这些失败交换操作的共同原因很容易识别：当数据成员指向或引用了交换所涉及的数据时，必须避免简单的交换操作。如果在图 9.4 中，地址 a 和地址 c 处的数据成员指向的是这两个对象之外的信息（例如，指向动态分配的内存），那么简单的交换就能成功。

然而，交换 `SelfRef` 对象时遇到的困难并不意味着两个 `SelfRef` 对象不能交换；它只意味着我们在设计 `swap` 成员时必须小心。下面是 `SelfRef::swap` 的一种实现：

```cpp
void SelfRef::swap(SelfRef &other)
{
    swap(d_data, other.d_data);
}
```

在这个实现中，交换时让自引用数据成员保持不变，仅仅交换其余的数据。也可以为图 9.3 所示的链表设计类似的 `swap` 成员。

#### 9.6.1.1 快速交换

正如我们在 placement new 中看到的那样，对象可以构造在大小为 `sizeof(Class)` 字节的内存块中。因此，同一个类的两个对象各自占用 `sizeof(Class)` 字节。

如果我们的类对象能够被交换，并且类的数据成员不引用实际参与交换操作的数据，那么就可以实现一种非常快速的交换方法，其基础正是我们知道对象的大小。

在这种快速交换方法中，我们仅仅交换 `sizeof(Class)` 字节的内容。这个过程可以应用于那些对象可以通过逐成员交换操作进行交换的类，并且（在实践中，尽管这可能超出了 C++ ANSI/ISO 标准所描述的操作范围）也可以用于具有引用数据成员的类。它只是定义一个 `sizeof(Class)` 字节的缓冲区，然后执行一次循环的 `memcpy` 操作。下面是针对一个假设类 `Class` 的实现，它能实现非常快速的交换：

```cpp
#include <cstring>

void Class::swap(Class &other)
{
    char buffer[sizeof(Class)];
    memcpy(buffer, &other, sizeof(Class));
    memcpy(&other, this, sizeof(Class));
    memcpy(this, buffer, sizeof(Class));
}
```

下面是一个简单的例子：某个类定义了一个引用数据成员，并提供了一个如上实现的 `swap` 成员。引用数据成员被初始化为外部流。运行程序后，`one` 包含两行 *hello to 1*，`two` 包含两行 *hello to 2*（为简洁起见，`Reference` 的所有成员都定义为内联形式）：

```cpp
#include <fstream>
#include <cstring>

class Reference
{
    std::ostream &d_out;

public:
    Reference(std::ostream &out)
        :
        d_out(out)
    {}
    void swap(Reference &other)
    {
        char buffer[sizeof(Reference)];
        memcpy(buffer, this, sizeof(Reference));
        memcpy(this, &other, sizeof(Reference));
        memcpy(&other, buffer, sizeof(Reference));
    }
    std::ostream &out()
    {
        return d_out;
    }
};

int main()
{
    std::ofstream one("one");
    std::ofstream two("two");

    Reference ref1(one);        // ref1/ref2 hold references to
    Reference ref2(two);        // the streams

    ref1.out() << "hello to 1\n";    // generate some output
    ref2.out() << "hello to 2\n";

    ref1.swap(ref2);

    ref2.out() << "hello to 1\n";    // more output
    ref1.out() << "hello to 2\n";
}
```

快速交换只应用于自定义类，并且必须能证明快速交换在交换时不会破坏其对象。

