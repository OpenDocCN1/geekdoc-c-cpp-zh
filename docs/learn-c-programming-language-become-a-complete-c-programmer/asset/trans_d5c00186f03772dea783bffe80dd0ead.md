

### 27.3.1 模板作为接口

模板类可用于为通用实现提供灵活且类型安全的接口。§25.3 中的 `Vector` 就是一个很好的例子：

```
template<typename T>
class Vector<T*>
    : private Vector<void*>
{
    // ...
};
```

总的来说，这种技术可用于提供类型安全的接口，并将类型转换局部化到实现中，而不是强迫用户编写它们。

## 27.4 模板参数作为基类

在经典的基于类层次结构的面向对象编程中，我们将不同类之间可能不同的信息放置在派生类中，并通过基类中的虚函数来访问它（§3.2.4、§21.2.1）。这样，我们就能编写通用代码，而不必担心实现中的变化。然而，这种技术不允许我们改变接口中使用的类型（§27.2）。此外，与内联函数的简单操作相比，虚函数调用可能代价较高。为了弥补这一点，我们可以将特化的信息和操作作为模板参数传递给基类。实际上，模板参数可以用作基类。

以下两个小节讨论的一般问题是：“我们如何将分别指定的信息组合成一个具有良好定义接口的紧凑对象？”这是一个基本问题，其解决方案具有普遍重要性。

### 27.4.1 组合数据结构

考虑编写一个平衡二叉树库。由于我们提供的库会被许多不同的用户使用，我们不能将用户（应用）数据的类型构建到我们的树节点中。我们有许多备选方案：

-   我们可以将用户数据放在派生类中，并使用虚函数来访问它。但虚函数调用（或者说运行时解析和检查的解决方案）相对昂贵，而且我们面向用户数据的接口不是以用户类型来表达的，因此仍然需要使用类型转换来访问它。
-   我们可以在节点中放置一个 `void*`，让用户用它来引用在节点外部分配的数据。但这会使分配次数加倍，增加许多（可能代价高昂的）指针解引用，并且每个节点还要增加一个指针的空间开销。我们还需要使用类型转换，以正确的类型访问用户数据。这种转换无法进行类型检查。
-   我们可以在节点中放置 `Data*`，其中 `Data` 是数据结构的“通用基类”。这可以解决类型检查问题，但结合了前两种方法的代价和不便。

还有其他备选方案，但请考虑：

```
template<typename N>
struct Node_base { // doesn’t know about Val (the user data)
    N* left_child;
    N* right_child;

    Node_base();
    void add_left(N* p) {
        if (left_child == nullptr)
            left_child = p;
        else
            // ...
    }
    // ...
};
```

```
template<typename Val>
struct Node : Node_base<Node<Val>> { // use derived class as part of its own base
    Val v;
    Node(Val vv);
    // ...
};
```

这里，我们将派生类 `Node<Val>` 作为模板参数传递给其自身的基类（`Node_base`）。这使得 `Node_base` 能够在其接口中使用 `Node<Val>`，甚至不需要知道它的真实名称！注意，`Node` 的布局是紧凑的。例如，`Node<double>` 大致等价于以下形式：

```
struct Node_base_double {
    double val;
    Node_base_double* left_child;
    Node_base_double* right_child;
};
```

遗憾的是，在这种设计下，用户必须了解 `Node_base` 的操作以及所生成树的结构。例如：

```
using My_node = Node<double>;

void user(const vector<double>& v)
{
    My_node root;
    int i = 0;

    for (auto x : v) {
        auto p = new My_node{x};
        if (i++ % 2) // choose where to insert
            root.add_left(p);
        else
            root.add_right(p);
    }
}
```

然而，用户要保持树的结构合理并非易事。通常，我们希望让树通过实现树平衡算法来负责这一点。然而，为了平衡树以便高效搜索，平衡器需要知道用户的值。

我们如何向设计中添加平衡器？我们可以将平衡策略硬编码到 `Node_base` 中，并让 `Node_base` “窥视”用户数据。例如，平衡树实现（如标准库的 map，默认情况下）要求值类型提供小于（<）操作。这样，`Node_base` 的操作就可以直接使用 `<`：

```
template<typename N>
struct Node_base {
    static_assert(Totally_ordered<N>(), "Node_base: N must have a <");

    N* left_child;
    N* right_child;
    Balancing_info bal;

    Node_base();
    void insert(N& n) {
        if (n < *left_child) {
            // ... do something ...
        }
        else {
            // ... do something else ...
        }
    }
    // ...
};
```

这样效果很好。事实上，我们在 `Node_base` 中构建的节点信息越多，实现就越简单。特别地，我们可以用值类型而不是节点类型来参数化 `Node_base`（如 `std::map` 所做的那样），这样就能够在单个紧凑的包中得到整棵树。然而，这样做并不能解决我们在这里试图解决的基本问题：如何组合来自多个独立指定来源的信息。把所有内容写在一个地方回避了这个问题。

因此，让我们假设用户想要操作 `Node`（例如，将节点从一棵树移动到另一棵树），这样我们就不能简单地将用户数据存储到匿名节点中。进一步假设我们希望能够使用多种平衡算法，因此需要将平衡器作为一个参数。这些假设迫使我们直面这个基本问题。最简单的解决方案是让 `Node` 将值类型与平衡器类型组合起来。然而，`Node` 不需要使用平衡器，所以它只是将平衡器传递给 `Node_base`：

```
template<typename Val, typename Balance>
struct Search_node : public Node_base<Search_node<Val, Balance>, Balance> {
    Val val; // user data
    Search_node(Val v) : val(v) {}
};
```

这里 `Balance` 被提及两次，因为它是节点类型的一部分，也因为 `Node_base` 需要创建一个 `Balance` 类型的对象：

```
template<typename N, typename Balance>
struct Node_base : Balance {
    N* left_child;
    N* right_child;

    Node_base();
    void insert(N& n) {
        if (this->compare(n, *left_child)) // use compare() from Balance
            // ... do something ...
        else
            // ... do something else ...
    }
    // ...
};
```

我本可以使用 `Balance` 来定义一个成员，而不是将其用作基类。然而，一些重要的平衡器不需要每个节点的数据，因此将 `Balance` 作为基类，我可以受益于空基类优化。语言保证，如果基类没有非静态数据成员，那么在派生类对象中不会为其分配内存（§iso.1.8）。此外，除了较小的风格差异外，这个设计与一个真实的二叉树框架 [Austern,2003] 是一致的。我们可以这样使用这些类：

```
struct Red_black_balance {
    // data and operations needed to implement red-black trees
};

template<typename T>
using Rb_node = Search_node<T, Red_black_balance>; // type alias for red-black trees

Rb_node<double> my_root; // a red-black tree of doubles

using My_node = Rb_node<double>;

void user(const vector<double>& v)
{
    for (auto x : v)
        my_root.insert(*new My_node{x});
}
```

节点的布局是紧凑的，我们可以轻松地内联所有性能关键函数。通过这套略显精巧的定义，我们实现了类型安全和易于组合。与所有在数据结构或函数接口中引入 `void*` 的方法相比，这种精巧设计带来了性能优势。这种对 `void*` 的使用会使有价值的基于类型的优化技术失效。在平衡二叉树实现的关键部分选择低级（C 风格）编程技术意味着显著的运行时开销。

我们将平衡器作为独立的模板参数传递：

```
template<typename N, typename Balance>
struct Node_base : Balance {
    // ...
};

template<typename Val, typename Balance>
```

