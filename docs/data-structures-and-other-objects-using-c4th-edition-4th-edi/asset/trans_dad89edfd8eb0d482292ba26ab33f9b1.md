

## (图 8.11 续)

```cpp
template <class Item>
void queue<Item>::operator=(const queue<Item>& source)
// Library facilities used: node2.h
{
  if (this == &source) // Handle self-assignment
    return;
  main_savitch_6B::list_clear(front_ptr);
  main_savitch_6B::list_copy(source.front_ptr, front_ptr, rear_ptr);
  count = source.count;
}

template <class Item>
Item queue<Item>::front( ) const
// Library facilities used: cassert
{
  assert( !empty( ) );
  return front_ptr->data( );
}

template <class Item>
void queue<Item>::pop( )
// Library facilities used: cassert, node2.h
{
  assert( !empty( ) );
  main_savitch_6B::list_head_remove(front_ptr);
  --count;
}

template <class Item>
void queue<Item>::push(const Item& entry)
// Library facilities used: node2.h
{
  if (empty( ))
  { // Insert the first entry.
    main_savitch_6B::list_head_insert(front_ptr, entry);
    rear_ptr = front_ptr;
  }
  else // Insert an entry that is not the first.
  { main_savitch_6B::list_insert(rear_ptr, entry);
    rear_ptr = rear_ptr->link( );
  }
  ++count;
}
```

### 第 8.3 节自测练习

- 17. 在什么情况下辅助函数有用？
- 18. 编写一个新的常量成员函数，返回队列尾部元素的副本。使用队列的数组版本。
- 19. 在队列的循环数组实现中，为什么构造函数将 last 设置为数组的最后一个索引？
- 20. 一位看到我们在第 418 页图 8.10 中所示的数组队列实现的程序员给出了以下建议：“既然队列中的元素数量可以通过 front 和 rear 的值来确定，为什么不消除 count 成员变量呢？” 该建议有问题吗？
- 21. 编写一个新的常量成员函数，返回队列尾部元素的副本。使用队列的链表版本。
- 22. 对于我们的实现，空队列中 rear_ptr 的值是多少？
- 23. 对于我们的实现，空队列时 front_ptr 必须为 NULL。哪些成员函数依赖于此要求？
- 24. 如果我们尝试将队列的前端放在链表的尾部，会出什么问题？

## 8.4 实现 STL deque 类

队列的一种变体是 *双端队列*，也称为 *deque*（发音类似单词“deck”）。deque 的关键属性是元素可以在两端快速插入和删除。这与栈（仅使用一端）和普通队列（元素从一端进入，从另一端离开）不同。deque 两端的名称称为“front”和“back”，但这些名称是任意的，因为相同的操作可以在两端发生。

我们之前在图 5.17（第 280 页）中已经见过 STL deque 类的大部分成员函数了。当时介绍该类是因为它与 vector 和 list 类相似。

deque 最直接的实现与我们使用循环数组或链表见过的队列实现类似——但链表必须使用一种特殊技术。在查看自测练习的答案之前，试着猜猜这种特殊技术是什么。

STL 使用一种更复杂的 deque 实现，最初分配一个固定大小的动态数组来存放元素。这个动态数组称为一个块，如果需要更多空间，则不会调整块的大小。相反，会分配一个相同固定大小的第二个块。根据需要分配越来越多的块，并将所有这些块的指针保存在一个单独的指针数组中。图 8.12 显示了符合此方案的 deque 私有成员变量的一种可能声明。

## 图 8.12 STL deque 类的一种可能数据结构

这个 deque 有三个 value_type 项的块（每个块标记为一个 X）。每个块是一个包含固定数量元素的动态数组（在我们的示例中为五个，尽管实际实现会有更大的块大小）。第一个块开头和最后一个块末尾的阴影数组位置当前未被使用——因此 deque 现在只有九个元素。

左侧的动态数组是指向块的指针数组。它目前最多可容纳 12 个指针，尽管当前只使用了 3 个。如果需要超过 12 个块，则可以扩展该指针数组。

整个数据结构还有六个其他指针。可以添加更多成员变量（例如一个用于 deque 当前大小的整数），但此处显示的内容足以实现一个良好的实现。

![](img/7bf56f684fab50d5ff9e94ae2818f3ac_454_0.png)

私有成员指针可能以如下方式声明：

```
static const size_t block_size = 5; // Number of value_type items in each block
typedef int value_type; // The elements in the deque
typedef value_type* vtp; // A pointer to a dynamic array of value_type items
vtp* block_pointers; // A pointer to the dynamic array of block pointers
vtp* first_bp; // A pointer to the first block pointer that's now being used
vtp* last_bp; // A pointer to the last block pointer that's now being used
vtp* block_pointers_end; // A pointer to the final entry in the array of block pointers
vtp* front_ptr; // A pointer to the front element of the whole deque
vtp back_ptr; // A pointer to the back element of the whole deque
```

图 8.12 使用了几种你以前未曾见过的特性。例如，左侧的四个指针的数据类型都是 vtp*。这是一个指向 vtp 变量的指针。但请注意，vtp 变量本身是一个指向 value_type 变量的指针。换句话说，vtp* 是一个指向指针的指针，你可以在图中看到这一点。如果你决定实现这个类，那么你还需要了解另一条信息：

### 指针运算

如果 p 是指向数组的指针且 n 是整数，则表达式 p+n 会给出一个新指针，该指针位于 *p 之后 n 个元素处。在此情况下，表达式 ++p 会改变 p，使其指向数组中的下一个元素，而 --p 会改变 p，使其指向数组中的前一个元素。如果 p 和 q 都是指向同一数组的指针，则表达式 q-p 会给出一个整数，指示 q 和 p 之间的距离。例如，如果 *q 是 *p 之后的元素，则 q-p 为 1。

作为使用指针运算的示例，图 8.13 显示了使用图 8.12 中数据结构的 deque pop_back 函数的一种可能实现。该函数设计有三种情况：

- 1. 如果 deque 只有一个元素，则 front_ptr 和 back_ptr 都指向同一个位置。在这种情况下，我们只需调用 clear 成员函数来删除该元素（并在 deque 变为空时可能执行其他所需的清理工作）。
- 2. 在第二种情况中，我们要删除的元素是最后一个块中的第一个元素。这是图 8.12 中的情况，其中两个不同的指针指向右下角的第九个 X。这两个指针是什么？一个是 back_ptr，另一个是 *last_bp。请注意，我们写的是 *last_bp 而不是仅 last_bp。你能看出原因吗？（参见自测练习。）一旦检测到这两个指针相同，工作涉及三个子步骤：（a）删除整个最后一个块；（b）使用 --last_bp 在指针数组中将 last_bp 向后移动；（c）使用指针运算将 back_ptr 重置为新最后一个块中的最后一个元素。
- 3. 在唯一剩下的情况中，我们要删除的元素不可能位于其块的顶部，因此我们只需将 back_ptr 向后移动一个位置。

## 图 8.13 Deque pop_back 函数的一种可能实现

### 成员函数实现

```cpp
void mydeque::pop_back() {
    // An empty deque has a NULL back_ptr:
    assert (back_ptr != NULL);

    if (back_ptr == first_bp)
    {
        // Case 1: There is just one element with just one block,
        // so delete it, and reset things back to the start.
        clear ();
    }
    else if (back_ptr == *last_bp)
    {
        // Case 2: back_ptr is pointing to the first element of the last block in the deque.

        // a. Remove the entire last block. Note that this will
        // call the destructor for each item in the block:
        delete [] back_ptr;

        // b. The last block pointer that we are using is now
        // one spot earlier in the array of block pointers:
        --last_bp;

        // c. The new back element is now the last element in the last block:
        back_ptr = (*last_bp) + (block_size-1);
    }
    else
    {
        // Case 3: The element we are removing is not the only element
        // in its block, so we just move the back_ptr backward:
        --back_ptr;
    }
}
```

### 调用 deque value_type 项的析构函数和构造函数

对于容器类的实际实现，还有我们尚未涉及的注意事项。例如，我们的 deque 实现使用小型动态数组（“块”）来存放 value_type 对象。这些对象的构造函数和析构函数在什么时候被调用？在图 8.13 中，析构函数似乎仅在删除整个块时被调用（步骤 2a）。另一种方法是在每次弹出一项时调用一次析构函数，这也将要求在每次 push 时调用构造函数。我们尚未了解如何对析构函数和构造函数进行显式的单独调用，因此我们在图 8.13 中没有采用该方法。

