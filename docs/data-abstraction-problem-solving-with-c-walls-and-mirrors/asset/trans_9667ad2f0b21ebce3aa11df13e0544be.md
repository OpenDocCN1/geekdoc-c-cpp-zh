

## 412 第14章 队列与优先队列的实现

```cpp
{
slistPtr->insertSorted(newEntry);
  return true;
} // 结束 add

template<class ItemType>
bool Sl_PriorityQueue<ItemType>::remove() {
 // 高优先级项位于有序列表的末尾
  return slistPtr->remove(slistPtr->getLength());
}
```

我们将该实现的剩余部分留给您作为练习题。但请注意，我们将在第17章中讨论一种时间效率更高的实现，在 true章我们将引入 ADT 堆（heap）。

问题 6：为有序列表实现的 ADT 优先队列定义方法 peek 方法。

# 总结

- 1. 队列的入队（enqueue）和出队（dequeue）操作需要对队列的两端进行高效访问。因此，基于链的队列实现使用一个具有头指针和尾指针的线性链链。或者，你可以使用循环链。
- 2. 基于数组的队列实现容易发生右移现象（rightward drift）。这种现象可能导致队列在并没有满的情况下显示为满。移动数组中的项只是为了补偿右移。一种更高效的解决方案是使用循环数组。
- 3. 如果你使用循环数组来实现队列，你必须能够区分队列满和队列空。你可以通过计算队列中项的数量、使用布尔变量 isFull，或者留出一个空数组位置来区分这种状态。
- 4. 你可以使用数组、链节点链或有序列表来包含优先队列中的项。使用 ADT 堆可以实现更时间效率更高的实现，我们将在书的后部分考虑它。

# 练习题

- 1. 为列表 14-3 中声明的 LinkedQueue 类编写拷贝构造函数。提示：查看第 7 章列表 7-4 中 ADT 栈的拷贝构造函数。
- 2. 重复上一个练习，但改为实现一个内存安全的构造函数。如果内存分配失败，该构造函数应该释放失败之前分配的所有内存，然后抛出异常。
- 3. 列表 14-3 中声明的 LinkedList 类的析构函数可以多次调用 dequeue。虽然写起来简单，但由于重复的方法调用，该析构函数的效率可能较低。编写另一个析构函数的实现，直接释放链链而不调用 dequeue。
- 4. 一个显示队列内容的操作在程序调试期间可能非常有用。为 ADT 队列添加一个 display 操作，使得 display 假设并使用 ADT 队列的链实现。
- 5. 考虑一个名为 getNumberOfElements 的方法，它返回队列中的元素数量而不改变队列。返回类型为 int，且不接受任何参数。
    - a. 在本章提供的基于数组的 ADT 队列中添加 getNumberOfElements。
    - b. 在本章提供的基于链的 ADT 队列中添加 getNumberOfElements。
- 6. 证明第 14.1 节描述的使用数组元素的队列实现比使用计数器更高效，尽管它在测试中看起来似乎执行了两个操作：
```cpp
front equals (back + 1) % MAX_QUEUE + 1
```
- 7. 考虑使用队列中的项来实现 ADT 队列的 ListQueue 类。当 ADT 列表的实现是，入队和出队操作的效率：
    - a. 基于数组
    - b. 基于链
- 8. 列表 14-1 给出的 ListQueue 类将队列的头部维护在队列项列表的末尾，并将队列的尾部维护在开头。注意该列表是 LinkedList 类的对象。如果我们将队列头部维护在列表开头，尾部在列表末尾，对入队出队操作的效率会有什么影响？
- 9. 按照第 14.2 节描述完成 SL_PriorityQueue 类的实现。
- 10. 实现一个允许更高优先级的队列。这种优先队列在使用操作系统和其他应用程序时非常有用。当有序列表是基于链实现时，使用最低值作为最高优先级可以使优先队列操作更高效。描述为什么这种优势是真实的。

# 编程题

- 1. 编写一个基于链的队列实现，使用循环链来表示队列中的项。你需要一个单指针。完成后，将你的实现与使用两个外部指针的链的实现进行比较。哪种实现更容易理解？哪种更高效？
- 2. 编写一个基于数组的队列实现，使用一个可调整大小的循环数组来表示队列中的项。
- 3. 修订本章提供的基于数组的队列实现。不要计算队列中项的数量，而是使用布尔变量 isFull 来区分满和空状态。
- 4. 本章描述了另一种基于数组的队列实现，它不使用特殊数据（如 count 或 isFull）来区分满和空状态（参见上一个编程题）。在这一实现中，为数组项声明 MAX_QUEUE + 1 个位置，但仅使用其中的 MAX_QUEUE 个项。你通过牺牲一个数组，让 front 成为队列头部位置的索引。如果 front 等于 (back + 1) % (MAX_QUEUE + 1)，则队列满；如果 front 等于 back，则队列为空。实现这种基于数组的方法。
- 5. 上一章的练习第 9 题定义了双端队列（deque）。使用循环数组实现 ADT deque。
- 6. 重复上一个编程题，但使用链维护 deque 的项。
- 7. 按照上一章练习第 9 题，作为 ArrayQueue 的派生类。

# 重载运算符与友元访问

C++ 提供了许多运算符。例如，当我们使用整数时，+ 是加法， 是赋值，== 是比较。当我们使用类时，我们必须重载它们。要重载运算符，你需要定义一个名称形式为

```
operator symbol
```

其中 symbol 是你要重载的运算符。对于 == 运算符，你命名为 operator== 并声明一个参数：位于右侧的对象。当前对象表示左侧的对象。对于 LinkedList，你会在头文件中添加

```cpp
bool operator==(const LinkedList<ItemType>& rightSide) const;
```

为了理解这一点，请意识到我们可能声明了一个成员函数 isEqualTo 来比较类型列表和当前对象以判断相等性。该函数的声明如下：

```cpp
bool isEqualTo(const LinkedList<ItemType>& rightSide) const;
```

为了使用 isEqualTo 比较 myList 和 yourList，你可以写：

```cpp
if (myList.isEqualTo(yourList))
    cout << "The lists are equal.\n";
```

你可以像对待 isEqualTo 一样对待 operator==；所以你可以写：

```cpp
if (myList.operator==(yourList))
    cout << "The lists are equal.\n";
```

因为 operator== 是一个简单的方法。但你也可以使用更简洁的 myList == yourList，编译器会理解你正在使用 operator== 方法。该方法的 LinkedList 实现是：

```cpp
template <class ItemType>
bool LinkedList<ItemType>::operator==(const LinkedList<ItemType>& rightSide) const
{
    bool isEqual = true; // 假设相等
// 首先检查项的数量是否相同
    if (itemCount != rightSide.getLength())
        isEqual = false;
```
（实现部分继续）

两个列表相等当它们的长度相同且每个项都

