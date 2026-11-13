

```cpp
cout << *p << endl; // Prints the value of p's item
*p = 42; // Changes the value of p's item to 42
```

## 节点迭代器——++ 运算符的两个版本

节点迭代器有两个版本的 ++ 运算符。这些版本允许我们编写 ++p 或 p++。让我们来看看这些版本，以了解它们的区别。

### 前置版本

前置版本的写法如下：

```cpp
node_iterator& operator ++() // Prefix ++
...
```

对于节点迭代器 p，此函数允许我们编写 ++p，其中 ++ 位于 p 之前。通常，我们单独编写表达式 ++p。在这种情况下，++ 函数由迭代器 p 激活，p 向前移动到下一个项目。

表达式 ++p 也可以作为更大表达式的一部分使用。当 ++p 作为更大表达式的一部分使用时，需要知道 ++p 的返回值是已经向前移动的迭代器 p 本身。例如，假设 p 当前位于此列表的第一个项目：

![](img/7bf56f684fab50d5ff9e94ae2818f3ac_359_0.png)

我们可以编写语句 cout << * (++p);。在此语句中，表达式 ++p 将 p 向前移动到第二个项目，并返回迭代器 p 以供 cout 语句使用。* 运算符在 p 向前移动后应用于 p，因此 cout 语句的结果是打印列表的第二个项目（13）。

您可能已经注意到，此运算符的返回类型是引用类型（node_iterator& 而非仅 node_iterator）。这意味着 ++p 的返回值实际上是 p 本身（移动后），而不是 p 的副本。让我们看看完整实现中是如何做到的，如下所示：

```cpp
node_iterator& operator ++() // Prefix ++
{
    current = current->link();
    return *this;
}
```

当 ++p 被激活时，第一条语句将 p 的当前指针向前移动一个节点。第二条语句是：return *this;。该语句使用关键字 this，它始终是指向激活该函数的对象的指针（参见第 188 页）。因此，*this 始终是激活成员函数的对象，而 return *this; 是使函数返回最初实际激活该函数的对象的常用方式。

### 后置版本

后置版本的写法如下：

```cpp
node_iterator operator ++(int) // Postfix ++
```

这种写法确实看起来很奇怪！它看起来好像这个版本的 ++ 运算符有一个 int 参数。但实际上并非如此。相反，在通常放置参数的位置使用关键字 int，用于表示“这是 ++ 运算符的后置版本”。使用更有意义的关键字，或者可能使用“前置”和“后置”两个关键字，会更合理。但我们必须遵循原始 C++ 要求，使用 (int) 来指示我们正在实现后置版本。

无论如何，此函数允许我们编写 p++，其中 p++ 位于 p 之后。当单独编写时（不是更大表达式的一部分），p++ 与 ++p 具有相同的含义，即将 p 向前移动到下一个项目。但是，在更大的表达式中，p++ 的返回值与 ++p 不同。特别是，p++ 的返回值是更改前 p 的副本。例如，假设 p 当前位于此列表的第一个项目：

![](img/7bf56f684fab50d5ff9e94ae2818f3ac_360_0.png)

我们可以编写语句 cout << * (p++);。在此语句中，表达式 p++ 将 p 向前移动到第二个项目，但返回值是移动前 p 的副本。* 运算符应用于此副本，因此 cout 语句的结果是打印列表的第一个项目（42）。

由于后置运算符的返回值是 p 原始值的副本，因此返回类型不是引用类型（它是 node_iterator 而非 node_iterator&）。通常，如果要返回对象的副本，请不要使用引用返回类型。让我们看看完整实现中副本是如何制作的，如下所示：

```cpp
node_iterator operator ++(int) // Postfix ++
{
    node_iterator original(current);
    current = current->link();
    return original;
}
```

副本在函数开始时制作，并存储在局部变量 original 中。然后将当前指针向前移动，返回语句返回原始迭代器的副本。

### 编程提示

++p 比 p++ 更高效

当您单独向前移动 p（不是更大表达式的一部分）时，编写 ++p 比 p++ 更高效。原因是每次激活 p++ 都会在更改前制作 p 的副本，即使返回值从未被使用。

## 常量集合的迭代器

如前所述，当指针使用 const 关键字声明时，我们必须小心，因为必须禁止对关联链表进行任何更改。例如，考虑这个函数，它应该遍历整数链表，累加所有整数的值：

```cpp
int add_values(const node<int>* head_ptr)
{
    node_iterator<int> start(head_ptr); // start is at the first node
    node_iterator<int> finish; // finish is beyond the end
    node_iterator<int> position; // position moves through list
    int sum = 0;

    for (position = start; position != finish; ++position)
    {
        sum += *position;
    }
    return sum;
}
```

![](img/7bf56f684fab50d5ff9e94ae2818f3ac_361_0.png)

问题是 head_ptr 被声明为 const node<int>*，因此不能用作节点迭代器构造函数的参数。该构造函数具有以下原型，要求一个指向节点的普通指针：

```cpp
node_iterator(node<Item>* initial);
```

解决方案是提供另一个迭代器——const_node_iterator——它可以与 const 节点一起使用。我们之前已经为 multiset 见过这种 const 迭代器（参见第 144 页）；它可以遍历容器，但绝不能以任何方式更改容器。

图 6.6 展示了我们为 node 类实现的 const 迭代器。我们的迭代器名为 const_node_iterator（这只是一个名称，而不是两个或多个独立的单词）。除了名称更改之外，const_node_iterator 与普通 node_iterator 还有一个不同之处：每次使用数据类型 Item 或 node<Item>* 时，现在都写为 const Item 或 const node<Item>*。

### 图 6.6 节点模板类的 Const 迭代器定义

### 模板类定义

```cpp
template <class Item>
class const_node_iterator
: public std::iterator<std::forward_iterator_tag, const Item>
{
public:
    const_node_iterator(const node<Item>* initial = NULL)
    { current = initial; }
    const Item& operator *() const
    { return current->data(); }
    const_node_iterator& operator ++() // Prefix ++
    {
        current = current->link();
        return *this;
    }
    const_node_iterator operator ++(int) // Postfix ++
    {
        const_node_iterator original(current);
        current = current->link();
        return original;
    }
    bool operator ==(const const_node_iterator& other) const
    { return current == other.current; }
    bool operator !=(const const_node_iterator& other) const
    { return current != other.current; }
private:
    const node<Item>* current;
};
```

使用 const_node_iterator，我们可以编写一个正确的 add_values 函数，如下所示：

```cpp
int add_values(const node<int>* head_ptr)
{
    const_node_iterator<int> start(head_ptr);
    const_node_iterator<int> finish;
    const_node_iterator<int> position;
    int sum = 0;
    for (position = start; position != finish; ++position)
    {
        sum += *position;
    }
    return sum;
}
```

### 编程提示

### 何时使用 Const 迭代器

使用 const 迭代器遍历常量项的容器。迭代器本身不是常量；它可以遍历容器，但绝不能以任何方式更改容器的任何部分。

## 第 6.5 节自测练习

- 28. 编写一个函数，遍历具有整数值的节点链表，将每隔一项更改为零。该函数的参数应为指向节点的指针，并且应有一个局部变量，即节点迭代器。
- 29. 为什么本章中的 node_iterator 类派生自 STL 迭代器？
- 30. 编写一个函数，遍历具有整数值的节点链表，统计零出现的次数。该函数的参数应为指向节点的指针，并且应有一个局部变量，即 const_node_iterator。
- 31. 节点迭代器的实现如何区分 ++ 运算符的前置版本和后置版本？
- 32. ++ 的哪个版本通常更高效？为什么？

