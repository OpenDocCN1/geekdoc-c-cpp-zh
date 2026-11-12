

### 编程提示：构造函数中的初始化器与设置方法

第 3 章建议你在构造函数中使用初始化器而不是赋值语句来初始化类的数据成员的值。这一建议仍然很好，初始化器清楚地显示了初始化。但是，如果你编写设置方法来更改数据成员的值，你就有机会确保所赋的值是有效的。当这些值由客户端提供时，这样做尤其重要。在这种情况下，构造函数可以调用设置方法来初始化数据成员。因此，在构造函数中初始化数据成员的值时，我们有以下建议：

- 如果数据成员的值没有限制，请使用初始化器。
- 如果数据成员的值需要验证，请使用设置方法。

请注意，即使你不想为特定数据成员提供公共设置方法，也可以为构造函数调用定义一个私有方法，或者让构造函数自行执行验证。

验证客户端给你的任何数据

## 7.3 使用异常的实现

我们对 ADT 栈的规范似乎能够处理所有情况。如果你尝试向已满的栈中添加一个项，方法 push 将返回 false。如果你尝试从空栈中移除一个条目，方法 pop 将返回 false。当你尝试查看空栈的栈顶时会发生什么？方法 peek 期望你不会这样做，如其前置条件所述。然而，我们的实现通过在其定义开始处使用以下语句来处理对该方法的误用：

```
assert(!isEmpty());
```

如果栈为空，assert 将发出错误消息并停止执行。

与使用 assert 不同，如果违反了前置条件，peek 可以抛出异常——也就是说，当栈为空时调用它。让我们定义 peek 可以使用的类 PrecondViolatedExcep。清单 7-5 和 7-6 显示了这个类。

### 清单 7-5 类 PrecondViolatedExcep 的头文件

```
//** File PrecondViolatedExcep.h **

#ifndef _PRECOND_VIOLATED_EXCEP
#define _PRECOND_VIOLATED_EXCEP

#include <stdexcept>
#include <string>

using namespace std;

class PrecondViolatedExcep: public logic_error
{
public:
   PrecondViolatedExcep(const string& message = "");
}; // end PrecondViolatedExcep

#endif
```

### 清单 7-6 类 PrecondViolatedExcep 的实现文件

```
/* #if File PrecondViolatedExcep.cpp */
#include "PrecondViolatedExcep.h"

PrecondViolatedExcep::PrecondViolatedExcep(const string& message):
    logic_error("Precondition Violated Exception: " + message)
{
} // end constructor
```

我们现在通过添加 throw 子句来修改头文件 ArrayStack.h 和 LinkedStack.h 中 peek 的声明，如下所示：

```
ItemType peek() const throw(PrecondViolatedExcep);
```

在实现文件中，我们将相同的 throw 子句添加到 peek 的头部，然后用以下 if 语句替换两个 peek 定义中的 assert 语句：

```
if (isEmpty())
    throw PrecondViolatedExcep("peek() called with empty stack");
```

因此，例如，LinkedStack 中 peek 的定义是

```
template<class ItemType>
ItemType LinkedStack<ItemType>::peek() const throw(PrecondViolatedExcep)
{
    // Enforce precondition
    if (isEmpty())
        throw PrecondViolatedExcep("peek() called with empty stack");
    // Stack is not empty; return top
    return topPtr->getItem();
} // end getTop
```

对 peek 的上述修改对于基于数组和基于链接的栈实现是相同的。

> **注意：** 在基于链接的栈实现中，方法 push 和复制构造函数都会分配新节点。如果系统没有可用的备用内存，此分配可能会失败。在这种情况下，将抛出标准异常 bad_alloc。但是，在我们的简单示例中，除非你的计算机系统内存大小受到严格限制，否则这种情况不太可能发生。为简单起见，我们不会担心这种情况。

> **问题 4** 定义异常类 MemoryAllocationException，然后修改类 LinkedStack 中方法 push 的定义，使其在无法分配新节点时抛出此异常。

## 总结

- 1. 你可以使用数组来实现栈。如果栈底位于数组的第一个元素中，那么在添加或移除条目时，不会移动栈条目。
- 2. 你可以使用带有头指针的链接节点链来实现栈。链的第一个节点应包含栈顶，以提供最简单、最快速的添加和移除操作。
- 3. 你应该调用 `assert` 或抛出异常来强制执行方法 `peek` 的前置条件。

## 练习

- 1. 讨论与基于链接的实现相比，基于数组的 ADT 栈实现的优缺点。
- 2. 考虑第 1、3 和 4 章中描述的 ADT 袋。
  - a. 你能否使用袋来包含栈的条目来实现 ADT 栈？为什么或为什么不能？
  - b. 你能否使用栈来包含袋的条目来实现 ADT 袋？为什么或为什么不能？
- 3. 在程序调试期间，显示栈内容的操作可能很有用。向 ADT 栈添加一个 `display` 方法，使其
  - a. 该方法仅使用 ADT 栈操作；也就是说，它独立于栈的实现。
  - b. 该方法假设并使用 ADT 栈的基于链接的实现。
  - c. 该方法假设并使用 ADT 栈的基于数组的实现。
- 4. 重复上一个练习，但定义方法 `toVector` 而不是方法 `display`。
- 5. 向本章给出的 ADT 栈添加一个 void 方法 `remove(n)`，该方法从栈中移除并丢弃最顶部的 n 个条目。为此方法编写基于链接的实现。
- 6. 重复上一个练习，但改为编写基于数组的实现。
- 7. 给定的 ADT 栈基于链接的实现的析构函数调用 `pop`。虽然易于编写，但由于重复的方法调用，此析构函数可能效率低下。为析构函数编写另一种实现，该实现直接释放链接节点而不调用 `pop`。
- 8. 为链接栈实现一个内存安全的复制构造函数。如果内存分配失败，此构造函数应释放故障前分配的所有内存，然后抛出异常。
- 9. 想象一个基于数组的 ADT 栈实现，它从数组末尾开始存储栈的条目。描述你如何定义栈操作，使得 push 和 pop 操作不需要移动数组中的现有条目。
- 10. 想象一个基于链接的 ADT 栈实现，它将栈的顶部条目存储在链接节点链的末尾。描述你如何定义栈操作，使得不需要遍历链。
- 11. 虽然当 LinkedStack 中的方法或构造函数无法分配新节点时，我们通常不会抛出自己的异常，但你可以这样做。定义异常 `MemoryAllocationException`，并修改 `LinkedStack` 的复制构造函数，使其在 new 运算符无法分配内存时抛出 `MemoryAllocationException`。从构造函数抛出异常需要非常小心，因为你必须确保在抛出异常之前正确释放构造函数分配的任何内存。
  - 测试你修改后的 `LinkedStack` 版本。

## 编程问题

- 1. 编写一个使用可调整大小的数组来表示栈项的 ADT 栈实现。每当栈变满时，将数组大小加倍。保持栈底条目位于数组的开头。
- 2. 重复编程问题 1，但保持栈底条目位于数组的末尾。
- 3. 重复编程问题 1，但保持栈顶条目位于数组的开头。
- 4. 重复编程问题 1，但保持栈顶条目位于数组的末尾。
- 5. 重复前四个编程问题中的任何一个，但在数组第一次加倍之后，如果当前栈条目占用的数组位置少于一半，则将数组大小减半。
- 6. 假设当基于数组的栈变满时，你不是将数组大小加倍，而是将数组大小增加某个正整数 k。实现并演示这样的栈，它允许客户端在创建栈时指定 k。
- 7. 重复上一个编程问题，但每次栈变满时，按序列 3k、5k、7k、... 的下一个值增加数组大小，其中 k 为客户端指定的正整数。
- 8. 编写练习 10 所描述的 ADT 栈实现。
- 9. ADT 栈允许你在不移除栈顶条目的情况下查看它。对于某些栈应用，你还需要在不移除栈顶条目的情况下查看其下方的条目。我们将此类操作命名为 peek2。如果 peek2 失败，因为栈中包含少于两个条目，它应该抛出异常。编写一个包含 peek 和 peek2 的 ADT 栈的基于链接的实现。
- 10. 使用本章描述的 ADT 栈实现，重复第 6 章中的任何编程问题（第一个除外）。

