

- 8. 描述如何修改第 364 页图 7.5 中的计算器程序，以允许计算器输入中包含注释。注释出现在表达式的末尾，以双斜杠 // 开头，并持续到行尾。
- 9. 第 364 页图 7.5 中的计算器程序可能出现哪些错误导致栈下溢？
- 10. 进行分析，确定第 364 页图 7.5 中的计算器程序中哪种表达式会导致栈变大。
- 11. iostream 函数 peek 和 ignore 与栈的 top 和 pop 操作有何相似之处？它们有何不同？
- 12. 算术表达式求值算法的时间复杂度（大 O 表示法）是多少？解释你的推理。

## 7.3 栈类的实现

作为程序员，你可以在不了解其工作原理的情况下使用 STL 栈。作为计算机科学的学生，研究栈的实现对你的其他编程工作是很好的经验。我们将给出我们栈类的两种实现：一种是使用固定大小数组的静态实现，另一种是使用链表的动态实现。标准库中典型的栈实现采用第三种方法（动态数组）。

### 栈的数组实现

图 7.6 给出了一个与 STL 栈类似的栈模板类的头文件。类定义为栈使用了两个私有成员变量：

- 1. 一个名为 data 的数组，最多可容纳 CAPACITY 个元素（其中 CAPACITY 是栈类的静态常量）。这是一个部分填充的数组，在 data[0]、data[1] 等位置存储栈的元素。
- 2. 一个名为 used 的单个成员变量，指示当前正在使用部分填充数组的多少部分。data[0] 处的条目位于栈的“底部”。data[used-1] 处的条目位于栈的“顶部”。如果 used 的值为零，则表示空栈。

换句话说，我们的栈实现只是一个以通常方式实现的部分填充数组：一个数组和一个指示最后使用的数组位置索引的变量。这个描述是我们类的不变式，因此每个成员函数（构造函数除外）在操作激活时都可以假设栈是以这种方式表示的。每个操作都有责任确保在操作完成时，栈仍然以这种方式表示。

栈条目存储在部分填充的数组中

### FIGURE 7.6 Header File for the Array Version of the Stack Template Class

### A Header File

```
// FILE: stack1.h (part of the namespace main_savitch_7A)
// TEMPLATE CLASS PROVIDED: stack<Item>
//
// TEMPLATE PARAMETER, TYPEDEFS, and MEMBER CONSTANTS for the stack<Item> class:
//   The template parameter, Item, is the data type of the items in the stack, also defined
//   as stack<Item>::value_type. It may be any of the C++ built-in types (int, char, etc.), or
//   a class with a default constructor, a copy constructor, and an assignment operator.
//   The definition stack<Item>::size_type is the data type of any variable that keeps track
//   of how many items are in a stack. For this implementation, stack<Item>::CAPACITY
//   is the maximum capacity of any stack (once CAPACITY is reached, further pushes
//   are forbidden).
//
// CONSTRUCTOR for the stack<Item> template class:
//   stack( )
//     Postcondition: The stack has been initialized as an empty stack.
//
// MODIFICATION MEMBER FUNCTIONS for the stack<Item> template class:
//   void push(const Item& entry)
//     Precondition: size( ) < CAPACITY.
//     Postcondition: A new copy of entry has been pushed onto the stack.
//
//   void pop( )
//     Precondition: size( ) > 0.
//     Postcondition: The top item of the stack has been removed.
//
// CONSTANT MEMBER FUNCTIONS for the stack<Item> template class:
//   Item top( ) const
//     Precondition: size( ) > 0.
//     Postcondition: The return value is the top item of the stack, but the stack is
//     unchanged. This differs slightly from the STL stack (where the top function returns a
//     reference to the item on top of the stack).
//
//   size_type size( ) const
//     Postcondition: The return value is the total number of items in the stack.
//
//   bool empty( ) const
//     Postcondition: The return value is true if the stack is empty, and false otherwise.
//
// VALUE SEMANTICS for the stack<Item> template class:
//   Assignments and the copy constructor may be used with stack<Item> objects.
//
```

### (FIGURE 7.6 continued)

```
#ifndef MAIN_SAVITCH_STACK1_H
#define MAIN_SAVITCH_STACK1_H
#include <cstddef> // Provides size_t
namespace main_savitch_7A
{
    template <class Item>
    class stack
    {
    public:
        // TYPEDEFS and MEMBER CONSTANT -- See Appendix E if this fails to compile.
        typedef std::size_t size_type;
        typedef Item value_type;
        static const size_type CAPACITY = 30;
        // CONSTRUCTOR
        stack( ) { used = 0; }
        // MODIFICATION MEMBER FUNCTIONS
        void push(const Item& entry);
        void pop( );
        // CONSTANT MEMBER FUNCTIONS
        bool empty( ) const { return (used == 0); }
        size_type size( ) const { return used; }
        Item top( ) const;
    private:
        Item data[CAPACITY]; // Partially filled array
        size_type used; // How much of array is being used
    };
}
#include "stack1.template" // Include the implementation.
#endif
```

### 栈类的不变式（数组版本）

- 1. 栈中的元素数量存储在成员变量 used 中。
- 2. 栈中的元素存储在一个名为 data 的部分填充数组中，栈底位于 data[0]，下一个条目位于 data[1]，依此类推，直到栈顶位于 data[used-1]。

### FIGURE 7.7 Implementation File for the Array Version of the Stack Template Class

### An Implementation File

```
// FILE: stack1.template
// TEMPLATE CLASS IMPLEMENTED: stack<Item> (see stack1.h for documentation)
// INVARIANT for the stack class:
//   1. The number of items in the stack is the member variable used.
//   2. The items in the stack are stored in a partially filled array called
//      data, with the bottom of the stack at data[0], the next entry at
//      data[1], and so on, to the top of the stack at data[used - 1].

#include <cassert>    // Provides assert
namespace main_savitch_7A
{
    template <class Item>
    const typename stack<Item>::size_type stack<Item>::CAPACITY;

    template <class Item>
    void stack<Item>::push(const Item& entry)
    // Library facilities used: cassert
    {
        assert(size( ) < CAPACITY);
        data[used] = entry;
        ++used;
    }

    template <class Item>
    void stack<Item>::pop( )
    // Library facilities used: cassert
    {
        assert(!empty( ));
        --used;
    }

    template <class Item>
    Item stack<Item>::top( ) const
    // Library facilities used: cassert
    {
        assert(!empty( ));
        return data[used-1];
    }
}
```

操作我们栈的成员函数现在非常直接。要初始化栈，将私有成员变量 used 设置为零，表示空数组，因此也是空栈。要向栈中添加一个条目（在 push 函数中），我们将新条目存储在 data[used]，然后将 used 加一。要查看栈顶条目（函数 top），我们只需查看数组位置 data[used-1] 中的条目。要从栈中移除一个条目（在 pop 函数中），我们减小 used。用于测试空栈和返回大小的成员函数是简单的内联实现，用于检查 used 的值。

我们栈的实现文件在第 372 页的图 7.7 中给出。

### 栈的链表实现

链表是实现栈的一种自然方式，作为一种动态结构，其大小可以在执行过程中增长和缩小，而没有在编译时确定的预定义限制。链表的头节点充当栈顶。第 375 页的图 7.8 包含了一个使用链表实现的栈模板类的头文件。以下是新栈类此版本不变式的精确说明：

### 栈类的不变式（链表版本）

- 1. 栈中的元素存储在链表中，栈顶存储在头节点，一直到栈底位于尾节点。
- 2. 成员变量 top_ptr 是元素链表的头指针。

和往常一样，所有成员函数（构造函数除外）在函数激活时都假设栈是以这种方式表示的，并且所有函数都确保在函数结束时栈仍然以这种方式表示。

由于我们使用链表，因此我们可以放入栈中的元素数量没有预定义限制。因此，在头文件中我们省略了常量 CAPACITY，但添加了文档，指示某些函数分配动态内存，并在动态内存耗尽时抛出 bad_alloc。

使用链表的进一步后果是，合理地利用第 0.4 节中的 node 模板类。因此，在图 7.8 中你会找到这个包含指令：

```
#include "node2.h" // Node template class
```

通过使用工具包，许多栈成员函数可以只用一两行代码来实现，如第 376 页的图 7.9 所示。

