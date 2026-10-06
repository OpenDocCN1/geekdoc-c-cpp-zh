

# 图 C4-3

派生类 MagicBox 继承了基类 PlainBox 的成员，并对其进行了精炼和新增成员

| PlainBox | MagicBox |
|---|---|
| item | firstItemStored |
| PlainBox() | |
| ~PlainBox() | 重定义 |
| setItem() | |
| getItem() | |

列表 C4-2 显示了类 MagicBox 的声明，该类最初位于 C++ Include 1 的列表 C1-7 中。

# 列表 C4-2 MagicBox 类，最初位于列表 C1-7 中

```cpp
template<class ItemType>
class MagicBox : public PlainBox<ItemType>
private:
    bool firstItemStored;
public:
    MagicBox();
    MagicBox(const ItemType& item);
    void setItem(const ItemType& item);
}; // MagicBox
```

在类 MagicBox 之后添加冒号 `public PlainBox` 表示 PlainBox 是 MagicBox 的基类，或者等同于 MagicBox 是 PlainBox 的派生类。

派生类的实例有两个成员——一个是继承的，另一个是新增的 `firstItemStored`。由于派生类的实例可以调用基类的任何方法，因此 MagicBox 的实例拥有 PlainBox 定义的所有方法：构造函数、`new`、编译器生成的析构函数以及一个精炼后的方法 `setItem`。尽管派生类的实例包含了继承的成员数据的副本，但继承方法的代码并没有被复制。

派生类不能通过名称访问其基类的私有成员，即使它们是被继承的。继承并不意味着访问权限。毕竟，你可以继承一个锁上的保险箱，但无法打开它。例如，数据 `item` 是私有的，因此你只能在 PlainBox 的定义内部引用它，而不能在 ToyBox 或 MagicBox 的定义内部引用。然而，ToyBox 类可以使用 PlainBox 的公共方法 `setItem` 和 `getItem` 来获取 `item` 的值。

在 MagicBox 的实现内部，你可以使用 MagicBox 从 PlainBox 继承的公共方法。例如，精炼后的 `setItem` 方法调用了继承的 `setItem` 方法，你通过编写 `PlainBox<ItemType>::setItem` 来指示这一点。这种写法对于区分两个版本的方法是必要的。因此，即使基类成员被重定义，你也可以使用作用域运算符 `::` 来访问它。MagicBox 的 `setItem` 方法的实现如下

```cpp
template<class ItemType>
void MagicBox<ItemType>::setItem(const ItemType& item)
```

- 派生类的实例具有其基类的行为
- 派生类继承基类的私有成员，但不能直接访问它们
- 派生类的方法可以改变基类的公共方法

```cpp
{
if (!firstItemStored)
{
    PlainBox<ItemType>::setItem(getItem());
    firstItemStored = true; // Box 现在已标记
} // end if
} // end setItem
```

派生类的类的客户端也可以调用基类的公共成员。例如，你写道：

```cpp
MagicBox<string> myMagicBox("volleyball");
string magicBoxItem = myMagicBox.getItem();
```

MagicBox 的 `item`（"volleyball"）由 MagicBox 从 PlainBox 继承的 `getItem` 方法返回。如果一个方法与祖先方法同名——例如 `setItem`——但如果使用了新方法，则新类的实例将使用新方法而不是原始方法。因此，如果 `myPlainBox` 是一个 `PlainBox` 对象，调用 `myPlainBox.setItem(...)` 将调用 MagicBox 的 `setItem`，如图 C4-4 所示——说明了这一点。由于编译器可以在编译时（而不是运行时）确定使用哪种形式的 `setItem`，这被称为早期绑定，引入于 C++ Interlude 2。早期绑定的另一个术是**静态绑定**。

- 派生类的客户端也可以调用基类的公共方法

# 继承以及构造函数与析构函数的执行顺序

派生类在基类构造函数之后执行。例如，如果你定义了一个 `MagicBox` 实例，它的构造函数会在 `PlainBox` 构造函数之后执行。派生类的析构函数在基类析构函数之前执行。例如，MagicBox 的析构会在 PlainBox 的析构函数之前执行。这对于你编写的构造函数和析构函数以及由编译器生成的函数都是如此。

早期绑定可能会导致问题，以下语句

- 早期绑定会导致问题

```cpp
PlainBox<string>* cardBoxPtr = new PlainBox<string>("Queen of Hearts");
cardBoxPtr->setItem("Jack of Spades");
```

调用了 `PlainBox` 版本的 `setItem`。不幸的是，如果 `cardBoxPtr` 指向一个 `MagicBox` 实例——例如，如果你写道：

```cpp
PlainBox<string>* cardBoxPtr = new MagicBox<string>("Queen of Hearts");
```

图 C4-4 早期静态绑定：编译器决定哪个哪个版本的

| PlainBox | MagicBox |
|---|---|
| item | firstItemStored |
| PlainBox() | |
| ~PlainBox() | |
| setItem() | setItem() |
| getItem() | |

```cpp
myPlainBox.setItem(...);
myMagicBox.setItem(...);
```

# 338 C++ INTERLUDE 4 类关系与重用

语句

```
cardBoxPtr->setItem("Jack of Spades");
```

仍然调用了 `PlainBox` 版本的 `setItem`，而不是 `MagicBox` 的版本。在这种情况下，编译器根据指针类型 `cardBoxPtr` 而不是 `cardBoxPtr` 指向的对象来确定要调用的方法版本。

仅仅在 `MagicBox` 中重定义（如我们之前所做的）是不够的。正如 C++ Interlude 1 的 C.5 节和 C++ Interlude 2 的 C2.4 节简单讨论过的，你还需要告诉编译器 `PlainBox` 的派生类可能会修改 `setItem`，以便编译器能够对这种情况做出调整。你通过在 `PlainBox` 中将 `setItem` 为虚方法来实现。你只需要在基类定义中的方法前写 `virtual` 即可。例如，`PlainBox` 类所示：

```cpp
class PlainBox
{
public:
    // 与之前相同，除了 setItem
    ...
    virtual ItemType setItem() const;
    ...
}; // end PlainBox
```

`setItem` 的实现与提供的相同。
现在，`cardBoxPtr` 指向一个 `MagicBox` 实例，语句

- 晚绑定意味着适当的方法版本在运行时决定

cardBoxPtr->setItem("Jack of Spades");

调用了 `MagicBox` 版本的 `setItem`。因此，方法的版本是在运行时决定的，而不是指针所指向的对象类型。从 C++ Interlude 2 回顾，这被称为晚绑定。晚绑定的另一个术语是动态绑定。像 `setItem` 这样的方法是多态的；操作的结果取决于它作用的对象。我们也说 MagicBox 的 `setItem` 版本覆盖了 PlainBox 的版本。

- 虚方法是可以被覆盖的方法
- 基类中的虚方法在任何派生类中都是虚方法
- 如果派生类中的方法与祖先虚方法的声明相同，则它也是虚方法。覆盖方法类似于重定义方法。你只能覆盖虚方法。注意你可以在派生类中覆盖虚方法

每个类都有一个虚方法表（VMT），它对程序员是不可见的。对于每个虚方法，VMT 包含指向实现该方法的指针。对于非虚方法，编译器可以建立此指针，因为它知道方法的定义。对于虚方法，编译器无法完成 VMT。程序执行期间调用构造函数会设置指针，如图 C4-5 所示。也就是说，构造函数建立了指向适用于对象的虚方法的指针。因此，VMT 是实现晚绑定的机制。

# C41.1 类的公共、私有和保护区域

![](img/d0cb86b2f18b2db569968ad7c743510e_364_0.png)

C++ 继承与访问

除了公共和私有区域外，类还可以有一个保护区域。通过创建保护区域，类设计者可以隐藏成员，但使其对派生类可用。也就是说，派生类可以直接引用其基类的成员，但基类或派生类的客户端则不能。

