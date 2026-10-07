

# 第10章 对象与类

```cpp
// 如果栈为空，pop() 返回 false；否则返回 true
bool pop(Item &item);      // 将栈顶元素弹出到 item
}
#endif
```

在列表 10.10 的示例中，私有部分（private section）显示栈是通过数组实现的，但公共部分（public section）并没有公开这一事实。因此，你可以将数组替换为（动态数组，而无需更改类接口。这意味着栈的实现不需要你对链接或现有的程序代码进行重编码。

如果 `pop()` 和 `push()` 返回关于栈状态（满或空）的信息而不是 `void` 类型，那么该接口就是冗余的。这为程序员提供了处理超出栈限制或清空栈的几种选择。他（或她）可以在尝试修改栈之前使用 `isEmpty()` 和 `isFull()` 来进行检查，或者使用 `push()` 和 `pop()` 的返回值来判断操作是否成功。

该类并没有根据特定类型来定义栈，而是根据通用的 `Item` 类型来描述它。在这种情况下，头文件使用 `typedef` 将项定义为 `unsigned long`。如果你需要一个 `double` 栈或结构类型的栈，可以更改 `typedef` 并保持类声明和方法定义不变。类模板（参见第 14 章，“在 C++ 中重用代码”）提供了一种更强大的方法，将类设计与存储的数据类型隔离开来。

接下来，你需要实现类方法。列表 10.11 显示了一种可能性。

# 列表 10.11 stack.cpp

```cpp
// stack.cpp -- 栈成员函数
#include "stack.h"
Stack::Stack() 
{
    top = 0;
}

bool Stack::isEmpty() const
{
    return top == 0;
}

bool Stack::isFull() const
{
    return top == MAX;
}

bool Stack::push(const Item & item)
{}
```

```cpp
if (top < MAX)
{
    items[top++] = item;
    return true;
}
else
    return false;
```

```cpp
bool Stack::pop(Item & item)
{
    if (top > 0)
    {
        item = items[--top];
        return true;
    }
else
    return false;
}
```

默认构造函数保证了所有栈在创建时都是空的。`pop()` 和 `push()` 的代码保证了栈顶被正确管理。这种保证是使 OOP（面向对象编程）可靠的因素之一。假设你创建了一个独立的数组来表示栈，并使用一个独立的变量来表示栈顶索引。在这种情况下，确保在每次创建新栈时代码都是正确的就成了你的责任。如果没有了私有数据提供的保护，总有可能发生某些无意更改数据的错误。

让我们测试一下这个栈。列表 10.12 模拟了一个办事员从收件箱中购买订单的场景，使用了栈的 FIFO（后进先出）方法。

# 列表 10.12 stacker.cpp

```cpp
// stacker.cpp -- 测试 Stack 类
#include <iostream>
#include <cctype> // 或 ctype.h
#include "stack.h"
int main()
{
    using namespace std;
    Stack st; // 创建一个空栈
    char ch;
    unsigned long po;
    cout << "Please enter A to add a purchase order,\n";
    << "P to process a PO, or Q to quit.\n";
    while (cin >> ch && toupper(ch) != 'Q');
}
```

```cpp
while (cin.get() != '\n')
  continue;
if (!isalpha(ch))
{
  cout << '\a';
  continue;
}
switch (ch)
{
  case 'A':
  case 'a': cout << "Enter a PO number to add: ";
    cin >> po;
    if (st.isfull())
      cout << "stack already full\n";
    else
      st.push(po);
    break;
  case 'P':
  case 'p': if (st.isEmpty())
    cout << "stack already empty\n";
    else {
      st.pop(po);
      cout << "PO #" << po << " popped\n";
    }
    break;
}
cout << "Please enter A to add a purchase order,\n"
  << "P to process a PO, or Q to quit.\n";
cout << "Bye!\n";
return 0;
}
```

列表 10.12 中的短 `while` 循环在目前并不是绝对必要的消除行的剩余部分，但在第 14 章修改此程序时将很有用。这里是一个运行示例：

Enter A to add a purchase order,
P to process a PO, or Q to quit.

Enter a PO number to add: 17885
Enter A to add a purchase order,
P to process a PO, or Q to quit.

PO #17885 popped
Please enter A to add a purchase order,

P to process a PO, or Q to quit.

A

Enter a PO number to add: 17965
nPlease enter A to add a purchase order,
P to process a PO, or Q to quit.

# 第10章 对象与类

# 总结

OOP 强调数据和方法。迈向 OOP 的第一步是设计类的类。接下来，你需要实现类方法。如果 `pop()` 和 `push()` 返回关于栈状态（满或空）的信息而不是 `void` 类型，那么该接口就是冗余的。这为程序员提供了处理超出栈限制或清空栈的几种选择。他（或她）可以在尝试修改栈之前使用 `isEmpty()` 和 `isFull()` 来进行检查，或者使用 `push()` 和 `pop()` 的返回值来判断操作是否成功。

该类并没有根据特定类型来定义栈，而是根据通用的 `Item` 类型来描述它。在这种情况下，头文件使用 `typedef` 将项定义为 `unsigned long`。如果你需要一个 `double` 栈或结构类型的栈，可以更改 `typedef` 并保持类声明和方法定义不变。类模板（参见第 14 章，“在 C++ 中重用代码”）提供了一种更强大的方法，将类设计与存储的数据类型隔离开来。

类是一种自定义类型，对象是类的实例。C++ 试图让自定义类型与标准类型相似，因此你可以声明对象、指针和对象数组。你可以将对象作为参数传递、作为返回值返回并将一个对象赋值给另一个。如果你提供构造方法，你可以在创建对象时初始化它们。如果你提供析构方法，程序会在对象失效时执行它。

每个对象拥有自己的数据副本，但它们共享方法。如果 `mr_object` 是特定对象的名称，`try_me()` 是一个成员函数，你使用点运算符调用该函数：`mr_object.try_me()`。OOP 术语将此函数描述为发送消息，随后应用于 `mr_object` 的数据成员。同样，函数调用 `i_try_me()` 访问 `i_object` 的成员。

类非常适合描述 ADT。公共成员函数接口提供了 ADT 定义的服务，而类的私有部分和类方法的代码提供了对客户端隐藏的实现。

# 复习

+   1. 什么是类？
2. 类如何实现抽象、封装和数据隐藏？
3. 对象与类之间是什么关系？
4. 除了都是函数，类函数成员与数据成员有何不同？
5. 定义一个类来表示银行账户。数据成员应包括存款人姓名、账号（使用字符串）和余额。成员函数应允许以下操作：

+   - 创建对象并对其初始化。
- 显示存款人姓名、账号和余额
- 存入给定的金额
- 提取给定的金额

（只需显示类声明，无需显示方法实现。练习 1 为你提供了编写实现的机会。）

