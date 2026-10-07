

```cpp
class Singer : public Worker { ... };
class Waiter : public Worker { ... };
class SingingWaiter : public Singer, public Waiter { ... };
```

# SingingWaiter 对象

![](img/cd111a87c1db9aff4db4b18834327463_829_0.png)

图 14.4 继承两个基类对象。

# 虚基类

虚基类允许派生自多个基类的对象（这些基类本身共享一个公共基类）只继承该共享基类的一个对象。对于这个示例，我们可以在类声明中使用 `virtual` 关键字将 Worker 设为 Singer 和 Waiter 的虚基类（`virtual` 和 `public` 的顺序可以任意）：

```cpp
class Singer : virtual Worker { ... };
class Waiter : public virtual Worker { ... };
```

然后你就可以像以前一样定义 SingingWaiter：
```cpp
class SingingWaiter:public Singer, public Waiter { ... };
```

现在，一个 SingingWaiter 对象将包含一个 Worker 对象的副本。从本质上讲，继承的 Singer 和 Waiter 对象共享一个公共的 Worker 对象，而不是各自带入自己的副本（见图 14.5）。由于 SingingWaiter 现在包含一个 Worker 子对象，你可以再次使用多态了。

# 第 14 章 C++ 中的代码复用

```cpp
class Singer : virtual public Worker { ... };
class Waiter : virtual public Worker { ... };
class SingingWaiter : public Singer, public Waiter { ... };
```

![](img/cd111a87c1db9aff4db4b18834327463_830_0.png)

让我们来看你可能有的某些问题：

- 为什么要用 virtual（虚）这个词？
- 为什么我们不直接声明基类为虚类，并将虚函数行为作为多重继承（MI）的规范呢？
- 有什么陷阱吗？

首先，为什么要用 virtual 这个词？毕竟，虚函数和虚基类这两个概念之间似乎没有明显的联系。C++ 社区面临着抵抗新关键字的压力。如果一个新关键字与某个主要程序中的某些重要函数或变量名冲突，那将很尴尬。因此，C++ 仅仅是为了这一新功能回收了 `virtual` 关键字——这有点像是关键字重载。

接下来，为什么我们不直接声明基类为虚类，并将虚函数行为作为多重继承的规范呢？首先，在某些情况下你可能需要基类的多个副本。其次，将基类设为虚需要程序进行一些额外的计数，如果你不需要该功能，就不应该为此付费。第三，还有下一段中提到的缺点。

最后，有什么陷阱吗？有的。要让虚基类工作需要对 C++ 规则进行调整，并且必须以不同的方式编写代码。此外，使用虚基类可能涉及修改现有代码。例如，将 SingingWaiter 类添加到 Worker 层次结构中，需要你返回向 Singer 和 Waiter 类添加 `virtual` 关键字。

# 新的构造函数规则

拥有基类需要一种处理类构造函数的方法。对于非虚基类，初始化列表中*唯一*可以出现的构造函数是其直接基类的构造函数。但这些构造函数反过来可以向基类传递信息。例如，你可以拥有如下的构造函数组织：

```cpp
class A
{
  int a;
public:
  A(int n = 0) : a(n) {}
  ...
}
class B : public A
{
  int b;
public:
  B(int m = 0, int n = 0) : A(n), b(m) {}
}
class C : public B
{
  int c;
public:
  C(int q = 0, int m = 0, int n = 0) : B(m, n), c(q) {}
  ...
};
```

构造函数只能调用来自 B 类的构造函数，A 和 B 构造函数只能调用来自 A 类的构造函数。在这里，C 构造函数使用了 `q` 值并将 `m` 和 `n` 的值传回 B 构造函数。B 构造函数使用 `m` 的值并将 `n` 的值传回 A 构造函数。

如果 Worker 是虚基类，这种自动信息传递就失效了。例如，考虑多重继承示例中以下可能的构造函数：

```cpp
SingingWaiter(const Worker &wk, int p = 0, int v = Singer::default)
  : Waiter(wk,p), Singer(wk,v) {} // 有缺陷的
```

问题在于，自动信息传递会通过两个独立的路径（Waiter 和 Singer）将 `wk` 传递给 Worker 对象。为了避免这种潜在的冲突，如果基类是虚类，C++ 会禁用通过中间类向基类的的自动信息传递。因此，构造函数将初始化 `panache` 和 `voice` 成员，但参数中的信息会丢失。编译器必须在构造派生对象之前构造基类对象组件；在这种情况下，它将使用默认的 Worker 构造函数。

# 第 14 章 C++ 中的代码复用

如果你想对虚基类使用默认基构造函数以外的内容，你需要显式调用相应的基构造函数。因此，构造函数应该如下：

```cpp
SingingWaiter(const Worker &wk, int p = 0, int v = Singer::other)
  : Worker(wk), Waiter(wk,p), Singer(wk,v) {}
```

在这里，代码显式调用了 `Worker(const Worker &)` 构造函数。注意，这种用法对于虚基类是合法的且往往是必要的，但对于非虚基类来说是非法的。

# 注意事项

如果一个类具有间接虚基类，则该类的构造函数应该显式调用虚基类的构造函数，除非仅需要虚基类的默认构造函数。

# 哪种方法？

除了类构造函数规则的改变外，多重继承通常还需要其他调整。考虑将 `Show()` 方法扩展到 SingingWaiter 类中的问题。由于 SingingWaiter 对象没有新的数据成员，你可能认为可以直接使用继承的方法。这引出了一个问题。假设你省略了新版本的 `Show()`，并尝试使用 SingingWaiter 对象调用继承的 `Show()` 方法：

```cpp
SingingWaiter newhire("Elise Hawks", 2005, 6, soprano);
newhire.Show(); // 冲突
```

在单继承中，未重定义 `Show()` 会导致使用最新的祖先定义。在这种情况下，每个直接祖先都有 `Show()` 函数，导致此调用产生义。

# 注意事项

多重继承会导致函数调用冲突。例如，`BadDude` 类可能继承自 `Gunslinger` 类和 `PokerPlayer` 类的 `Draw()` 方法。你可以使用作用域解析符来明确你的意思：

```cpp
SingingWaiter newhire("Elise Hawks", 2005, 6, soprano);
newhire.Singer::Show(); // 使用 Singer 版本
```

然而，更好的方法是在 SingingWaiter 中重定义 `Show()` 并指定使用哪个 `Show()`。例如，如果你想让 SingingWaiter 使用 Singer 版本，你可以这样做。这种让派生方法调用基方法的方法对于单继承来说足够了。例如，假设 `HeadWaiter` 类派生自 `Waiter` 类。你可以使用如下定义序列，每个派生类都增加其基类显示的信息：

```cpp
void Worker::Show() const
{
    cout << "Name: " << "\n";
    cout << "Employee ID: " << id << "\n";
}
```

```cpp
void Worker::Show() const
{
    Worker::Show();
    cout << "Panache rating: " << panache << "\n";
}
```

```cpp
void HeadWaiter::Show() const
{
    Waiter::Show();
    cout << "Presence rating: " << presence << "\n";
}
```

这种增量方法在 SingerWaiter 案例中失效了。然而，以下方法忽略了 Waiter 组件：

```cpp
void SingingWaiter::Show()
{
    Singer::Show();
}
```

你可以通过调用 Waiter 基类版本来修复这个问题：

```cpp
void SingingWaiter::Show()
{
    Singer::Show();
    Waiter::Show();
}
```

这会显示两次姓名和 ID，因为 `Singer::Show()` 和 `Waiter::Show()` 都调用了 `Worker::Show()`。

如何修复这个问题？一种方法是使用模块化方法而不是增量方法。即，使用一个只显示 Worker 组件的方法，另一个只显示 Waiter 组件的方法（而不是 Waiter 加上 Worker 组件），以及另一个只显示 Singer 组件的方法。那么

