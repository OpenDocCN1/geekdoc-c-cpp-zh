
```cpp
} else {

    ListNode<NODETYPE>* currentPtr(firstPtr);

    std::cout << "The list is ";

    while (currentPtr != nullptr) { // 拷贝元素

        std::cout << currentPtr->data << " ";

        currentPtr = currentPtr->nextPtr;

    }

    std::cout << "\n";

}

}
```

**图 19.5** | `List` 类模板定义。

```cpp
private:

    ListNode<NODETYPE>* firstPtr(nullptr); // 指向第一个节点的指针

    ListNode<NODETYPE>* lastPtr(nullptr); // 指向最后一个节点的指针

    // 分配新节点的工具函数

    ListNode<NODETYPE>* getNewNode(const NODETYPE& value) {

        return new ListNode<NODETYPE>{value};

    }

};
#endif
```
图 19.5 | `List` 类模板定义。（4 部分中的 4 部分。）

# 19.3.4 成员函数 `insertAtFront`

在接下来的页面中，我们将详细讨论 `List` 类的成员函数。`insertAtFront`（图 19.5，第 32–42 行）将新节点插入列表头部。该函数包含以下步骤：

1. 调用 `getNewNode` 函数（第 33 行），传递要插入节点的常量引用。
2. `getNewNode` 函数（第 136–138 行）使用运算符 `new` 创建一个新的列表节点并返回该新分配节点的指针，用于初始化 `insertAtFront` 中的 `newPtr`（第 33 行）。
3. 如果列表为空（第 35 行），将 `firstPtr` 和 `lastPtr` 设置为 `newPtr`（第 36 行）即首尾相同。
4. 如果列表不为空，通过将 `firstPtr` 拷贝到 `newPtr->nextPtr`（第 39 行）将新节点链入列表，使新节点指向原来的第一个节点，并将 `newPtr` 拷贝到 `firstPtr`（第 40 行），使 `firstPtr` 现在指向列表的第一个节点。

图 19.6 展示了 `insertAtFront` 函数的操作。部分 (a) 显示了调用 `insertAtFront` 之前的列表和新节点。部分 (b) 中的虚箭头说明了 `insertAtFront` 操作的第 4 ，使得包含 12 的节点成为新的列表头部。

![](img/09cee61886647f0b1e06dc44c0065a38_850_0.png)

图 19.6 | 图形表示的操作 操作。

# 19.3.5 成员函数 `insertAtBack`

`insertAtBack`（图 19.5，第 45–52 行）将新节点放在列表后端。该函数包含以下步骤：

1. 调用 `newNode` 函数（第 46 行），传递 `value`，它是要插入节点值的常量引用。
2. `getNode` 函数（第 136–138 行）使用运算符 `new` 创建一个新的列表节点并返回该新分配节点的指针，用于初始化 `insertAtBack` 中的 `newPtr`（第 46 行）。
3. 如果列表为空（第 48 行），则将 `firstPtr` 和 `lastPtr` 都设置为 `newPtr`（第 49 行）。
4. 如果列表不为空，通过将 `newPtr` 拷贝到 `lastPtr->nextPtr`（第 52 行）将 `newPtr` 指向的节点链入列表，使最后一个节点指向新节点，并将 `newPtr` 拷贝到 `lastPtr`（第 53 行），使 `insertAtBack` 指向列表的最后一个节点。

图 19.7 展示了 `insertAtBack` 操作。部分 (a) 显示了操作前的列表和新节点。部分 (b) 中的虚箭头说明了 `insertAtBack` 函数的第 4 ，使得新节点添加到非空列表的末尾。

# 19.3.6 成员函数 `removeFromFront`

`removeFromFront`（图 19.5，第 58–76 行）移除列表的头部节点并将节点值拷贝到引用参数。如果尝试从空列表中移除节点（第 59–61 行），函数返回 `false`；如果移除成功，则返回 `true`。该函数包含以下步骤：

1. 将 `tempPtr` 初始化为 `firstPtr` 所指向的地址（第 63 行）。最终 `tempPtr` 将用于删除被移除的节点。

# 19.3 链表 851

![](img/09cee61886647f0b1e06dc44c0065a38_851_0.png)

图 19.7 | 操作 `insertAtBack` 的图形化表示。

- 2. 如果 `firstPtr` 等于 `lastPtr`（第 65 行），即在尝试移除前列表中只有一个元素，则将 `firstPtr` 和 `lastPtr` 设置为 `nullPtr`（第 66 行），以取消该节点的链结（使链表为空）。
- 3. 如果在移除前列表中有多个节点，则保持 `lastPtr` 不变，并将 `firstPtr` 设置为 `firstPtr->nextPtr`（第 69 行）；即修改 `firstPtr` 指向移除前的第二个节点（现在是第一个节点）。
- 4. 在完成所有这些指针操作后，将被删除节点的值数据成员拷贝到引用参数中（第 72 行）。
- 5. 现在删除 `tempPtr` 所指向的节点（第 73 行）。
- 6. 返回 `true`，表示移除成功（第 74 行）。

图 19.8 展示了 `removeFrom`。部分 (a) 展示了移除操作前的链表。部分 (b) 显示了从非空列表中移除头部节点的实际指针操作。

## 19.3.7 成员函数 `removeBack`

函数 `removeBack`（图 19.5，第 79–105 行）移除链表的尾节点并将节点值拷贝到引用参数。如果尝试从空列表中移除节点，则返回 `false`（第 80–82 行），如果移除成功则返回 `true`。该函数由几个步骤组成：

- 1. 将 `tempPtr` 初始化为 `lastPtr` 所指向的地址（第 84 行）。最终，`tempPtr` 用于删除被移除的节点。
- 2. 如果 `firstPtr` 等于 `lastPtr`（第 86 行），即在尝试移除前列表中只有一个元素，则将 `firstPtr` 和 `lastPtr` 设置为 `nullPtr`（第 87 行），将该节点从链表中取消（使链表为空）。

# 第 19 章 模板化数据结构

![](img/09cee61886647f0b1e06dc44c0065a38_852_0.png)

图 19.8 | 操作 `removeFront` 的图形化表示。

- 3. 如果在移除前列表中有多个节点，则将 `currentPtr` 初始化为 `firstPtr` 所指向的地址（第 90 行），为为“遍历链表”做准备。
- 4. 现在，使用 `currentPtr` “遍历链表”，直到它指向最后一个节点的前一个节点。该节点在移除操作完成后将成为最后一个节点。这是通过一个 `while` 循环实现的（第 93–95 行），在 `currentPtr->nextPtr` 不等于 `lastPtr` 的情况下，不断用 `currentPtr->nextPtr` 替换 `currentPtr`。
- 5. 将 `lastPtr` 赋值为 `currentPtr` 所指向的地址（第 97 行），以便从链表中重新读取尾节点。
- 6. 在新链表中将 `currentPtr->nextPtr` 设置为 `nullptr`（第 98 行）。
- 7. 在完成所有指针操作后，将被删除节点的值数据成员拷贝到引用参数中（第 101 行）。
- 8. 现在通过 `tempPtr` 删除节点（第 102 行）。
- 9. 返回 `true`（第 103 行），表示移除成功。

图 19.9 展示了 `removeFromFront`。图 (a) 展示了移除操作前的链表。图 (b) 显示了实际的指针操作。

## 19.3 成员函数 `print`

函数 `print`（图 19.5，第 113–129 行）首先确定链表是否为空（第 114 行）。如果是，则打印“The list is empty”并返回（第 115–116 行）。否则，输出每个节点中的值。函数将 `currentPtr` 初始化为 `firstPtr`（第 119 行），然后打印字符串“The list is: ”第 121 行）。当 `currentPtr` 不为 `nullptr` 时（第 123 行），打印 `currentPtr->data`（第 124 行）并将 `currentPtr` 赋值为 `currentPtr->nextPtr` 的值（第 125 行）。注意，如果链表中最后一个节点的链接不是 `nullptr`，打印算法将错误地尝试打印链表末尾之后。这里的打印算法对于链表、栈和队列是相同的（因为这些数据结构都基于相同的链表基础）。

![](img/09cee61886647f0b1e06dc44c0065a38_853_0.png)

图 19.9 | 操作 `removeFromBack` 的图形化表示。

## 19.3.9 循环链表和双向链表

我们讨论的链表类型是单向链表——链表从指向第一个节点的指针开始，每个节点包含一个指向“序列”中下一个节点的指针。以一个指针成员值为 `nullptr` 的节点结束。单向链表只能向一个方向遍历。

循环单向链表（图 19.10）从指向第一个节点的指针开始，每个节点包含一个指向下一个节点的指针。最后一个节点的值不是 `nullptr`；而是指向第一个节点，从而形成环。

![](img/09cee61886647f0b1e06dc44c0065a38_853_0.png)

图 19.10 | 循环链表。

双向链表（图 19.11）从指向第一个节点的指针开始，每个节点包含一个指向下一个节点的指针和一个指向前一个节点的指针。它以一个指针成员值为 `nullptr` 的节点结束。双向链表可以在两个方向上遍历。

![](img/09cee61886647f0b1e06dc44c0065a38_854_0.png)

图 19.11 | 双向链表。

```cpp
// Fig. 19.13: Stack.h
// Stack 类-模板定义。

#ifndef STACK_H
#define STACK_H

#include "List.h" // List 类定义

template<typename STACKTYPE>
class Stack { private: List<STACKTYPE> list;

public:
    // push 调用 List 的函数 insertFront
    void push(STACKTYPE& data) {
        insertAtFront(data);
    }
    // pop 调用 List 的函数 removeFromFront
    bool pop(STACKTYPE& data) {
        return removeFromFront(data);
    }
    // isEmpty 调用 List 的函数 isEmpty
    bool isEmpty() const {
        return this->isEmpty();
    }
    // printStack 调用 List 的函数 print
    void printStack() const {
        this->print();
    }
};
#endif
```

Fig. 19.13 | `Stack` 类-模板定义。

## 19.4.3 类模板中的依赖名称（Dependent Names）

在第 23 行和第 28 行显式使用 `this->` 是必须的，以便编译器能够正确解析模板定义中的标识符。依赖名称是指依赖模板参数的标识符。例如，对 `removeFromFront` 的调用（第 18 行）依赖于参数 `data`，而 `data` 的类型依赖于模板参数 `STACKTYPE`。依赖名称的解析发生在模板实例化时。

相比之下，`List` 类中不带参数的函数（如 `isEmpty` 或 `print`）的标识符是非依赖名称。标识符通常在模板定义处进行解析。如果模板尚未实例化，则非依赖名称的函数代码尚不存在，某些编译器会生成编译错误。在第 23 行和第 28 行中添加显式的 `this->` 使用可以使对基类成员函数的调用依赖于模板参数，并确保代码能够正常编译。

## 19.4.4 测试 `Stack` 类模板

类模板在 `main` 函数中（图 19.14）被用于实例化类型为 `Stack<int>` 的整数栈 `intStack`（第 8 行）。整数 0 到 2 被推入 `intStack`（第 13–16 行），然后从 `intStack` 中弹出（第 21–25 行）。程序使用 `Stack` 类创建类型为 `Stack<double>` 的 `doubleStack`（第 27 行）。值 1.1、2.2 和 3.3 被推入 `doubleStack`（第 33–37 行），然后从 `doubleStack` 中弹出（第 42–46 行）。

```cpp
// Fig. 19.14: fig19_1.cpp
// 一个简单的栈程序。

#include <iostream>
#include "Stack.h" // Stack 类定义
using namespace std;

int main() {
  Stack<int> intStack; // 创建整数类型的栈
  cout << "processing an integer Stack" << endl;
  // 将整数推入 intStack
  for (int i=0; i < 3; ++i) {
    intStack.push(i);
    intStack.printStack();
  }
  int popInteger; // 存储从栈中弹出的整数
  // 从 intStack 弹出整数
  while (!intStack.isEmpty()) {
    intStack.pop(popInteger);
    cout << popInteger << " popped from stack" << endl;
    intStack.printStack();
  }
  Stack<double> doubleStack; // 创建双精度类型的栈
  double value{1.1};
  cout << "processing a double Stack" << endl;
  // 将浮点值推入 doubleStack
  for (int j=0; j < 3; ++j) {
    doubleStack.push(value);
    doubleStack.printStack();
    value += 1.1;
  }
  double popDouble; // 存储从栈中弹出的双精度值
  // 从 doubleStack 弹出浮点值
  while (!doubleStack.isEmpty()) {
    doubleStack.pop(popDouble);
  }
}
```

Fig. 19.14 | 一个简单的栈程序。（部分，共 2 部分）。

# 第 19 章 自定义模板数据结构

```
44 cout << popDouble << " popped from stack" << endl;
45 doubleStack.printStack();
46 }
47 }
```

processing an integer Stack
The list is: 0

The list is: 1 0

The list is: 2 1 0

2 popped from stack
The list is: 1 0

1 popped from stack
The list is: 0

0 popped from stack
The list is empty

processing a double stack
The list is: 1.1

The list is: 2.2 1.1

The list is: 3.3 2.2 1.1

3.3 popped from stack
The list is: 2.2 1.1

2.2 popped from stack
The list is: 1.1

1.1 popped from stack
The list is empty

All nodes destroyed

All nodes destroyed

> Fig. 19.14 | 一个简单的栈程序。（部分 2，共 2 部分。）

## 19.4.5 通过组合 `List` 对象实现类模板 `Stack` 类

实现 `Stack` 模板的另一种方法是通过组合重用 `List` 类模板。图 19.15 是 `Stack` 类的一种新实现，它包含一个名为 `stackList` 的 `List<STACKTYPE>` 对象（第 33 行）。此版本的 `Stack` 类使用了图 19.5 中的 `List` 类。要测试此 `Stack` 类，使用图 19.14 中的驱动程序，但包含新的头文件 `Stackcomposition.h`。该 `Stack` 类的输出与 19.4 相同。

```cpp
// Fig. 19.15: Stackcomposition.h
// 组合 List 对象的 Stack 类模板定义。

#ifndef STACKCOMPOSITION_H
#define STACKCOMPOSITION_H
```
