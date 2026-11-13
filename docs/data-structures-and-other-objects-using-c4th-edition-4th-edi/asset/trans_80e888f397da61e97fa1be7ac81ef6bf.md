

```
class bag
{
public:
  ...
private:
  value_type *data; // Pointer to dynamic array
  size_type used;   // How much of array is being used
  size_type capacity; // Current capacity of the bag
};
```

在掌握大部分类定义后，我们现在可以说明动态袋类的不变式：

## 修订版袋类的不变式

- 1. 袋中的项目数存储在成员变量 used 中。
- 2. 袋中的实际项目存储在一个部分填充的数组中。该数组是动态数组，由成员变量 data 指向。
- 3. 动态数组的总大小存储在成员变量 capacity 中。

## 成员函数根据需要分配动态内存

当类使用动态内存时，类的成员函数会根据需要分配动态内存。例如，动态袋的构造函数会分配成员变量 data 指向的动态数组。但这个数组应该有多大呢？我们的计划是让构造函数分配一个动态数组，其初始大小由构造函数的参数确定。随着袋子在程序中被使用，其动态数组的大小实际上可能会增加到所需的任何容量。

换句话说，构造函数的参数决定了袋子的初始容量，但即使达到这个初始容量后，仍然可以插入更多项目。每当向袋子中插入项目时——无论是通过 insert 成员函数还是 += 运算符——都会检查袋子的当前容量。如果当前容量太小，则成员函数会分配一个更大的新动态数组。袋子的用户无需做任何特殊操作即可获得增加的容量。insert 和 += 函数会根据需要增加容量。

你可能会好奇，为什么程序员需要关心袋子的初始容量。程序员难道不能从一个小的初始容量开始，然后一个接一个地插入项目吗？insert 函数会负责根据需要增加容量。是的，这种方法始终能正确工作。

*初始容量的重要性*

但是如果项目很多，那么 insert 的许多调用都需要增加容量。这可能效率低下。每次增加容量时，都会分配新内存，将项目复制到新内存中，并释放旧内存。为了避免这种重复的内存分配，程序员可以请求一个大的初始容量。考虑到这一点，新袋子构造函数的文档如下：

```
bag(size_type initial_capacity = DEFAULT_CAPACITY);
// Postcondition: The bag is empty with a capacity given by the parameter.
// The insert function will work efficiently (without allocating new
// memory) until this capacity is reached.
```

例如，假设程序员要将 1000 个项目放入名为 kilosack 的袋子中。在声明袋子时，程序员可以指定容量为 1000，如下所示：

```
bag kilosack(1000); // 1000 items can be efficiently added to kilosack.
```

达到初始容量后，insert 函数仍能正确工作，但可能会因内存分配而变慢。

*构造函数充当默认构造函数*

请注意，构造函数的参数有一个默认参数 DEFAULT_CAPACITY，它将是我们类定义中的一个常量。由于有默认参数，这个单一的构造函数实际上起到了两个作用：它可以带参数使用来构造具有特定容量的袋子，也可以作为默认构造函数使用（没有参数列表）。当构造函数不带参数列表使用时，DEFAULT_CAPACITY 用于初始容量。以下是两个示例，分别使用默认构造函数和带参数的构造函数：

```
bag ordinary; <-- The initial capacity is DEFAULT_CAPACITY.
bag super(9000); <-- The initial capacity is 9000.
```

这里还有一个示例，展示新构造函数如何与其他成员协同工作。该示例声明了一个初始容量为 6 的袋子，并向其中放入三个项目：

```
bag sixpack(6); <-- The constructor creates a bag
with an initial capacity of 6.
sixpack.insert(10);
sixpack.insert(20);
sixpack.insert(30);
```

这些声明之后，袋子的私有成员变量如下所示：

袋子的私有成员变量包括一个指向动态分配的六个元素数组的指针。前三个元素现在正在被使用。

![](img/7bf56f684fab50d5ff9e94ae2818f3ac_206_0.png)

稍后，程序可以向这个袋子中插入更多项目，甚至可能超过六个。如果项目超过六个，则袋子的成员函数将根据需要增加袋子的容量。

在袋子声明并已投入使用后，程序员可以通过一个名为 reserve 的新成员函数对袋子的容量进行显式调整。该成员函数的规格如下：

```
void reserve(size_type new_capacity);
// Postcondition: The bag's current capacity is changed to the
// new_capacity (but not less than the number of items already in the bag).
// The insert function will work efficiently (without allocating new memory) until
// the new capacity is reached.
```

在某种程度上，reserve 函数是一种奢侈。程序员可以完全避免使用 reserve，允许其他成员函数根据需要调整袋子的大小。但是，通过使用 reserve 成员函数，可以提高袋子的效率。

为这个函数使用 reserve 这个名称可能看起来是个奇怪的选择。我们选择这个名称是为了与标准库容器类匹配，这些容器类有一个 reserve 成员函数来更改容器的容量。

*尽可能使用标准库容器类的名称*

总而言之，我们迄今为止看到的五个成员函数可以分配新的动态内存：构造函数、reserve、insert 以及两个运算符（+= 和 +）。与任何分配动态内存的函数一样，这些函数都可能失败——堆可能没有足够空间。在这种情况下，函数会调用 new 运算符，而 new 运算符会失败并抛出 bad_alloc 异常。这会打印错误消息并停止程序。对于我们的程序，打印错误消息并停止就足够了。但是，我们的类文档的一部分将指明哪些成员函数分配动态内存，以便更有经验的程序员可以以自己的方式处理异常。你可以在图 4.8 的底部看到此文档，它提供了我们新袋类头文件（bag2.h）的完整文档。

## 头文件文档

```
// 类 bag 的类型定义和成员常量：
// typedef ___ value_type
// bag::value_type 是袋中项目的数据类型。它可以是任何 C++
// 内置类型（int、char 等），或者是带有默认构造函数、赋值
// 运算符以及用于测试相等性（x == y）和不等性（x != y）的运算符的类。
// typedef ___ size_type
// bag::size_type 是任何用于跟踪袋中有多少项目的变量的数据类型。
// static const size_type DEFAULT_CAPACITY = _____
// bag::DEFAULT_CAPACITY 是由默认构造函数创建的袋子的初始容量。
// 类 bag 的构造函数：
// bag(size_type initial_capacity = DEFAULT_CAPACITY)
// 后条件：袋子为空，初始容量由参数给出。insert 函数将高效工作（不分配新
// 内存），直到达到此容量。
// 类 bag 的修改成员函数：
// size_type erase(const value_type& target)
// 后条件：target 的所有副本已从袋中移除。
// 返回值是移除的副本数量（可能为零）。
// bool erase_one(const value_type& target)
// 后条件：如果 target 在袋中，则移除一个副本；
// 否则袋子保持不变。true 返回值表示移除了一个副本；false 表示未移除任何内容。
// void insert(const value_type& entry)
// 后条件：entry 的新副本已插入袋中。
// void reserve(size_type new_capacity)
// 后条件：袋子的当前容量更改为
// 新容量（但不小于袋中已有的项目数量）。insert 函数将高效工作（不分配
// 新内存），直到达到新容量。
// void operator +=(const bag& addend)
// 后条件：addend 中的每个项目都已添加到此袋中。

reserve 成员函数提供了效率。
```

