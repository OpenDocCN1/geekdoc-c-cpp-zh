

![](img/f2bfa570e453b020c16e048c79a3ea0e_485_0.png)

图 9.4 链表。

![](img/f2bfa570e453b020c16e048c79a3ea0e_485_1.png)

图 9.5 在第一个元素之前插入（需要更新头指针）。

![](img/f2bfa570e453b020c16e048c79a3ea0e_485_2.png)

图 9.6 在两个元素之间插入。

![](img/f2bfa570e453b020c16e048c79a3ea0e_485_3.png)

图 9.7 在最后一个元素之后插入。

要将一个值插入链表，我们必须遍历链表以找到插入位置。我们从链表的 *头* 开始，使用当前元素中的指针从一个元素移动到另一个元素，直到找到所需的插入位置。插入位置可以是四个地方之一：在第一个元素之前、在两个元素之间、在最后一个元素之后，或在空链表中。图 9.5 至 9.8 概述了每种情况，假设我们对前三种情况都使用图 9.4 中给出的链表。

要从链表中删除一个值，我们必须遍历链表以找到要删除的元素。我们从链表的头部开始，使用当前元素中的指针从一个元素移动到另一个元素。如果找到了要删除的元素，它可以是第一个元素、两个其他元素之间的元素，或最后一个元素。图 9.9 至 9.11 概述了这三种情况中的每一种。对于每种情况，我们都从图 9.4 中给出的链表开始。

![](img/f2bfa570e453b020c16e048c79a3ea0e_486_0.png)

图 9.8 在空链表中插入（需要更新头指针）。

![](img/f2bfa570e453b020c16e048c79a3ea0e_486_1.png)

图 9.9 删除第一个元素（需要更新头指针）。

![](img/f2bfa570e453b020c16e048c79a3ea0e_486_2.png)

图 9.10 删除两个元素之间的元素。

![](img/f2bfa570e453b020c16e048c79a3ea0e_486_3.png)

图 9.11 删除最后一个元素。

## 栈

栈被称为后进先出（LIFO）数据结构。你只能从栈顶插入（push）和删除（pop）元素。因此，从栈中删除的元素始终是最后添加的元素。栈在编译器设计以及在程序中解析函数调用流程方面至关重要。例如，每次调用函数时，都会将返回地址添加到栈中。每条返回语句都引用最后添加到栈中的地址。图 9.12 说明了栈的行为。

## 队列

队列被称为先进先出（FIFO）数据结构。你只能将元素添加（push）到队列的末尾，并仅从队列的前端删除（pop）元素。因此，从队列中删除的元素始终是首先添加到队列中的元素。队列在计算机工程和计算机科学应用中是有用的数据结构。例如，操作系统使用队列来处理作业请求。作业请求（例如打印机请求）在队列中等待处理。队列前端的作业请求首先被处理。图 9.13 说明了队列的行为。

![](img/f2bfa570e453b020c16e048c79a3ea0e_487_0.png)

图 9.12 栈的行为。

![](img/f2bfa570e453b020c16e048c79a3ea0e_487_1.png)

图 9.13 队列的行为。

## 实践！

- 1. 编写栈类的实现，如下面的类声明所示：

```cpp
class stack
{
    int* a;
    int sizeOfStack;
public:
    stack();
    void push(int);    //add value to top of stack
    int pop();         //remove top element
    int top();         //return value of top element
    int isempty();     //element is not removed
};
```

- 2. 将你的栈类修改为 double 类型的栈。
- 3. 将你的栈类修改为 point 类型的栈。

## 9.8 C++ 标准模板库

编写程序员定义的函数来插入和删除链式数据结构中的元素需要仔细的内存管理和指针重新分配，如在第 10 章中提供的用于实现二叉树概念的程序员定义类型的开发所示。但是，作为实现自己的数据结构库的替代方案，您可以选择使用 C++ STL 中定义的容器类。容器类是一个类，例如 vector 类，旨在保存对象。SGI 网站（http://www.sgi.com/tech/stl/）是完整和最新文档的良好来源。我们的第一个示例将说明 list 类的用法。

### list 类

要使用 list 类，必须包含编译器指令 #include<list>。定义新列表时，必须指定列表中对象的数据类型。以下类型声明语句定义了一个名为 alist 的空整数列表：

```
list<int> alist;
```

要有系统地从列表中插入和删除元素，我们必须能够遍历列表。list 类提供了一种特殊的指针类型，称为迭代器，以支持访问列表中的连续元素。迭代器基本上是指向列表中元素的指针。我们可以使用以下语句定义一个名为 iter 的迭代器来访问我们整数列表中的元素：

```
list<int>::iterator iter;
```

list 类包含许多成员函数来支持列表结构，包括用于从列表中插入和删除元素的函数。表 9.2 列出了 list 类的几个常用成员函数。

| 成员函数 | 描述 |
|---|---|
| begin() | 返回指向列表中第一个元素的迭代器。 |
| end() | 返回指向列表中最后一个元素之后位置的迭代器。 |
| empty() | 如果列表为空，则返回 true；否则返回 false。 |
| insert(iterator, value) | 在迭代器指定的位置插入值。 |
| remove(value) | 从列表中删除值的所有实例。 |
| sort() | 将元素按升序排列。 |

以下程序说明了这些函数中的几个的用法：

```
/*..........................................................*/
/* Program chapter9_10 */
/*
* This programs creates a list of data entered from
* standard input.
* The list is sorted and printed to standard output.
*/
#include<iostream>//Required for cout, cin
#include<list>//Required for list, begin(), end(), insert(), sort()
using namespace std;

int main()
{
    // Declare objects.
    list<int> alist;
    list<int>::iterator iter;
    int ivalue;

    // Set iter to beginning of alist.
    iter = alist.begin();

    cout << "enter integer values, 's' to stop\n";

    // While valid data, read value and insert into list.
    while(cin >> ivalue)
    {
        alist.insert(iter, ivalue);
        ++iter;
    }

    // Sort the list in ascending order.
    alist.sort();

    // Print the list to standard output.
    cout << "Sorted list: \n";
    for(iter=alist.begin(); iter!=alist.end(); ++iter)
    {
        cout << *iter << endl;
    }
    return 0;
}
```

如果从键盘输入数据 35 18 21 14 10 2 s，程序将生成以下输出：

```
Enter integer values, 's' to stop
Sorted List:
2
10
14
18
21
35
```

语句

```
++iter;
```

不执行标准指针运算，而是重新将 iter 指向列表中的下一个元素。

![](img/f2bfa570e453b020c16e048c79a3ea0e_490_0.png)

### stack 类

C++ STL 包含 stack 类，它提供了栈的基于对象的实现。要使用 stack 类，必须包含编译器指令 #include<stack>。

定义栈时，必须指定栈中对象的数据类型。以下类型声明语句定义了一个名为 astack 的空整数栈：

```
stack<int> astack;
```

| 函数 | 描述 |
|---|---|
| empty() | 如果栈为空，则返回 true；否则返回 false。 |
| pop() | 从栈中删除顶部元素。不返回值。 |
| push(value) | 将值添加到栈顶。 |
| size() | 返回栈中元素的数量。 |
| top() | 返回栈中第一个元素的值。该元素不会从栈中删除。 |

表 9.3 列出了 stack 类的成员函数。以下程序说明了这些函数中的几个的用法：

```
/*
* Program chapter9_11
*
* This programs creates a stack of data entered from
* standard input.
* The Stack is printed to standard output.
*/
```

