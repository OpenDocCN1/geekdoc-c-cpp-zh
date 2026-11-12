

## 重载运算符和友元访问

## C++ 插曲 5

### 目录

- C5.1 重载运算符 415
- C5.1.1 重载 = 用于赋值 417
- C5.1.2 重载 + 用于连接 419
- C5.2 友元访问和重载 << 421

### 先决条件

- 第 4 章 链式实现
- 第 8 章 列表
- 第 9 章 列表实现

C++ 提供了许多运算符，例如 +、-、*、/、=、==、<、> 和 <<，这些运算符是为原始数据类型定义的。例如，在处理整数时，符号 + 表示加法运算，= 用于赋值运算，== 用于相等性比较。当我们使用类定义新的 C++ 数据类型时，这些符号没有定义如何添加或比较类的两个对象。这个 C++ 插曲描述了 C++ 为你提供的工具，用于扩展当前的运算符定义，以便它们可以应用于你创建的类。

![](img/288a0c22d14d2450c1e772f228f867b0_441_0.png)

### C5.1 重载运算符

C++ 中的标准算术运算符实际上具有多种含义。虽然表达式 2 + 3 和 2.0 + 3.0 中的加法运算符看起来相同，但实际上并不相同。因为像 2 和 3 这样的整数具有与 2.0 和 3.0 这样的浮点数不同的内部表示，所以添加两个整数的算法必须与添加两个浮点数的算法不同。C++ 可以使用两个不同的符号来指定整数加法和浮点加法，但它只使用一个符号，即 +。+ 运算符的实际含义——即它指定的加法类型——由其操作数的数据类型暗示。具有多种含义的运算符是重载的，是简单多态形式的示例。

重载运算符具有多种含义

如前所述，你通过使用类在 C++ 中定义新数据类。此类数据类型的客户端应该能够像使用语言的标准数据类型一样自然地使用它们。特别是，客户端应该能够以有意义的方式将类的实例与 C++ 运算符结合使用。要使特定运算符能够正确地对类的实例进行操作，你通常必须为运算符定义新含义；也就是说，你必须重载它。

假设 mylist 和 yourlist 是 LinkedList 的两个实例，如第 9 章清单 9-2 所示，你编写

```cpp
if (mylist == yourlist)
    cout << "The lists are equal.\n";
```

你必须为 LinkedList 提供 == 的定义，因为编译器不会提供默认解释。为此，让我们声明，如果列表 myList 与列表 yourList 相等，当且仅当

两个列表相等，当且仅当它们具有相同的长度和项目

- mylist 和 yourlist 具有相同的大小，且
- mylist 上的每个项目都与 yourlist 上的相应项目相同

要重载运算符，你定义一个运算符方法，其名称形式为

```
operator symbol
```

其中 symbol 是你想要重载的运算符。对于 == 运算符，你将方法命名为 operator== 并声明一个参数：将出现在运算符右侧的对象。当前对象表示运算符左侧的对象。对于 LinkedList，你将在头文件中的类定义中添加以下声明

```cpp
bool operator==(const LinkedList<ItemType>& rightHandSide) const;
```

要理解此表示法，请注意，我们也可能声明了一个客户端函数 isEqualTo，它将类型为 LinkedList 的参数与当前对象进行比较以确定相等性。此类函数的声明如下：

```cpp
bool isEqualTo(const LinkedList<ItemType>& rightHandSide) const;
```

要使用 isEqualTo 比较列表 mylist 和 yourlist，你将编写

```cpp
if (mylist.isEqualTo(yourlist))
    cout << "The lists are equal.\n";
```

你可以像处理 isEqualTo 一样处理 operator==；也就是说，你可以编写

```cpp
if (mylist.operator==(yourlist))
    cout << "The lists are equal.\n";
```

因为 operator== 只是一个方法名。但是，你也可以使用更自然的简写表示法 mylist == yourlist，编译器将理解你指的是 operator== 方法。

此方法的 LinkedList 实现如下

```cpp
template <class ItemType>
bool LinkedList<ItemType>::operator==(const
    LinkedList<ItemType>& rightHandSide) const
{
   bool isEqual = true; // Assume equal

   // First check whether the number of items is the same
   if (ItemCount != rightHandSide.getLength())
      isEqual = false;
else
{ // Then compare items
    Node<ItemType>* leftSidePtr = headPtr;
    Node<ItemType>* rightSidePtr = rightHandSide.headPtr;
    while ((leftSidePtr != nullptr) && (rightSidePtr != nullptr) && isEqual)
    {
        ItemType leftItem = leftSidePtr->getItem();
        ItemType rightItem = rightSidePtr->getItem();
        isEqual = (leftItem == rightItem);
        leftSidePtr = leftSidePtr->getNext();
        rightSidePtr = rightSidePtr->getNext();
    } // end while
} // end if
return isEqual;
} // end operator==
```

必须为 ItemType 定义 == 运算符

请注意，此方法依赖于列表中项目的 == 运算符。如果这些项目本身是类的实例，则该类必须重载 ==。你可以以类似的方式重载关系运算符（<、<=、>、>=）。

现在假设你希望第 8 章清单 8-1 中给出的所有 ListInterface 实现都提供 == 运算符的实现。你需要将以下声明添加到接口 ListInterface

```cpp
virtual bool operator==(const ListInterface<ItemType>& rightHandSide) const = 0;
```

ListInterface 的每个实现都将提供 == 的定义，从而允许你比较任何两个 ListInterface 对象。进行此比较的挑战在于，只能对右侧的列表使用 ListInterface 方法，从而影响比较具有两种不同实现的列表时的相等性检查效率。例如，如果我们有一个基于数组的列表，希望将其与基于链接的列表进行比较，那么在访问条目时，我们无法利用底层链式结构的节点结构。相反，我们需要使用 getEntry 来访问条目，但每次调用 getEntry 都会从列表开头迭代直到到达所需条目。

其他关系运算符的实现以类似的方式完成。

### C5.1.1 重载 = 用于赋值

重载赋值运算符 (=) 与重载相等运算符类似，但它带来了额外的考虑。再次假设 myList 和 yourList 是 LinkedList 的两个实例。如果你在列表 yourList 中放入多个项目，然后编写

```cpp
myList = yourList;
```

没有重载赋值运算符，你会得到浅拷贝

你可能期望 myList 是 yourList 的精确副本。然而，如果没有重载赋值运算符，你会得到 yourList 的浅拷贝而不是深拷贝，如第 4 章图 4-8 所示。虽然浅拷贝对于静态分配的数据结构可能足够，但对于动态分配的结构（例如链式实现 LinkedList 中的链接节点链）来说，深拷贝是必要的。LinkedList 对象（yourList）的浅拷贝只会复制数据成员 itemCount（列表 yourList 的长度）和 headPtr（指向 yourList 第一个项目的指针）。列表中的项目不会被复制。

要为类 LinkedList 提供赋值运算符，你将添加以下声明

```cpp
LinkedList<ItemType>& operator=(const LinkedList<ItemType>& rightHandSide);
```

