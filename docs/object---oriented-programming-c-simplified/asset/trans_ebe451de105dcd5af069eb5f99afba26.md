
## C++ 面向对象编程（简化版）

```cpp
void show()
{
    while(start != NULL)
    {
        cout << start->data << "->";
        start = start->next;
    }
}
;
void main()
{
    Linklist<int> L;
    L.add(10);
    L.add(20);
    L.add(30);
    cout << "\nLinked List of integer\n";
    L.show();
    Linklist<char> L1;
    L1.add('A');
    L1.add('B');
    L1.add('C');
    L1.add('E');
    cout << "\n Linked List of characters \n";
    L1.show();
    Linklist<char*> L2;
    L2.add("Hari");
    L2.add("Mohan");
    L2.add("Pandey");
    L2.add("Lecturer");
    cout << "\n Linked list of string \n";
    L2.show();
    Linklist<float> L3;
    L3.add(123.456f);
    L3.add(34.56f);
    L3.add(456.67f);
    L3.add(4532.895f);
    cout << "\nLinked list of float \n";
    L3.show();
}
```

### 输出

```
Linked list of integer
10->20->30->
Linked list of character
A->B->C->E->
Linked list of string
Hari->Mohan->Pandey->Lecturer
Linked list of float
123.456->34.56->456.67->4532.895->
```

### 说明

该程序与前一个程序类似，区别在于这里我们创建了一个类模板，它将针对不同的类型被实例化 4 次。也就是说，L 表示整数链表，L1 表示字符链表，L2 表示字符串链表，L3 表示浮点数链表。

```cpp
/* PROG 13.19 TEMPLATE BASED LINKED LIST WITHOUT USING STRUCTURE AS A NODE */

#include <iostream.h>
template <class LIST>
class linklist
{
    LIST data;
    linklist* next;
public:
    linklist(LIST num)
    {
        data = num;
        next = NULL;
    }
    void add_node(linklist* node)
    {
        node->next = this;
        this->next = NULL;
    }
    linklist* getnext()
    {
        return next;
    }
    LIST getdata()
    {
        return data;
    }
};

void main()
{
    linklist<int> LL(1);
    linklist<int>* temp, *link;
    link = &LL;
    int j;
    for(j = 2; j <= 5; j++)
    {
        temp = new linklist<int>(j);
        temp->add_node(link);
        link = temp;
    }
    temp = &LL;
    cout << "Linked list is \n";
    for(j = 1; j <= 5; j++)
    {
        cout << temp->getdata() << "->";
        temp = temp->getnext();
    }
}
```

### 输出

```
Linked List is
1->2->3->4->5->
```

### 说明

类 linklist 包含一个 linklist 类型的指针数据成员 next。这种类型的类称为自引用类。该类有一个通用类型的数据成员 data。类模板 linklist 的构造函数为类创建第一个节点，并将值 1 赋给 data，将 NULL 赋给 next。临时类类型指针 link 保存 main 中由 LL 表示的第一个节点的地址。注意，这里链表的每个节点都是 linklist 类的对象。在 for 循环中，对于 `j = 2`，语句：

```cpp
temp = new linklist<int>(j);
```

创建一个数据值为 2 且 `next = NULL` 的新节点。现在需要将这个节点添加到链表的末尾。为此，我们调用函数 `add_node` 并将 `link` 作为参数传递：

```cpp
temp->add_node(link);
```

新节点是 `temp`，而 `this` 指针在函数 `add_node` 内部代表 `temp`。`link` 代表第一个节点。因此，在函数 `add_node` 中，link 节点的 `next` 将存储由 `this` 指针表示的这个新节点的地址，而这个新节点的 `next` 将为 NULL。函数 `add_node` 中实现上述操作的方式如下：

```cpp
node->next = this;
this->next = NULL;
```

```cpp
void main()
{
    demo<A> d1;
    demo<B> d2;
    d1.showd();
    d2.showd();
}
```

### 输出

```
Hello from A
Hello from B
```

### 说明

在该程序中，用自定义类型替代通用类型，而不是基本类型。我们有两个不同的类 A 和 B。两个类都有一个 `show` 函数。类模板 `demo` 只有一个 `showd` 函数。在 main 中，当我们编写 `demo<A> d1;` 时，通用类型 T 被替换为 A；当我们调用 `d1.showd()` 时，在 `showd` 函数内部会调用类 A 的 `show`，因为 `showd` 的函数定义是 `A.show`。当我们编写 `demo<B> d2;` 时，通用类型 T 被替换为 B；当我们调用 `d2.showd()` 时，在 `showd` 函数内部会调用类 B 的 `show`，因为 `showd` 内部调用的函数是 `B.show`。

```cpp
/* PROG 13.21 CLASS TEMPLATE WITH FIX ARGUMENTS */

#include <iostream.h>
#include <typeinfo.h>
template <class TARR, int size>
class demo
{
    TARR arr[size];
public:
    demo()
    {
        int i;
        cout << "Enter " << size << " " << typeid(TARR).name()
             << "numbers \n";
        for(i = 0; i < size; i++)
            cin >> arr[i];
    }
    TARR sum()
    {
        int i;
        TARR s = 0;
        for(i = 0; i < size; i++)
```

## 第 14 章
## C++ 中的异常处理

### 14.1 引言

在 C++ 中，错误可以分为两类：

- **1. 编译时错误**和
- **2. 运行时错误。**

编译时错误是在编写程序过程中出现的语法错误。编译时错误最常见的例子有缺少分号、缺少逗号、缺少双引号等。它们主要是由于对语言理解不够或在编写程序时注意力不集中造成的。

还有一种逻辑错误，主要是由于程序员对程序逻辑理解不当造成的。逻辑错误会导致意外或不想要的输出。

异常是程序员通常不会预期的运行时错误。它们偶然发生，可能导致程序异常终止。C++ 提供了异常处理机制，可用于捕获这种异常，并在捕获异常后使程序平稳运行。

常见的异常示例有除零、打开不存在的文件、内存不足、数组越界等。

### 14.2 异常处理基础

异常处理是在程序运行时若产生异常则对该异常进行处理的过程。异常处理的目标是编写代码，将产生的异常传递给能够处理该异常并采取适当措施的例程。任何异常处理机制都必须包含以下步骤：

- **步骤 1：** 编写异常类（可选）。
- **步骤 2：** 编写 try 块。
- **步骤 3：** 抛出异常。
- **步骤 4：** 捕获并处理抛出的异常。

### 1. try 块

异常由写在 try 块中的语句抛出。每当 try 块中产生异常时，就会抛出该异常。异常是一个对象，因此我们可以说抛出了一个异常对象。`throw` 关键字用于抛出异常。使用 throw 语句的惯常做法如下：

```cpp
throw exception;
```

用于抛出异常，而简单形式为：

```cpp
throw;
```

用于重新抛出异常。

try 块的语法如下所示：

```cpp
try
{
    statements;
    statements;
    statements;
    throw exception;
}
```

### 2. catch 块

由 try 块抛出的异常由 catch 块捕获。一个 try 块必须至少有一个 catch，尽管可以有多个 catch 块来捕获不同类型的异常。catch 块之前必须有一个会抛出异常的 try 块。catch 块的用法如下：

```cpp
try
{
    statements;
    statements;
    statements;
    throw exception;
}
catch (object or argument)
{
    statements for handling the exception;
}
```

catch 块会捕获 try 块抛出的任何异常。如果抛出的异常与块中的参数或对象匹配，则执行 catch 块内编写的语句，此时我们说 try 块抛出的异常已被 catch 块成功捕获。在 catch 块语句成功执行之后，将执行 catch 块后面的任何语句。如果参数与抛出的异常不匹配，则 catch 块无法处理该异常，这可能导致程序异常终止。

### 14.3 异常处理机制

try、throw 和 catch 三者共同提供了 C++ 中的异常处理机制。异常由写在 try 块中的 `throw` 关键字产生。在 try 块内产生的任何异常都通过该 `throw` 关键字抛出。紧跟着 try 块之后编写 catch 块。一旦发生某个运行时错误，try 块就会使用 `throw` 抛出异常，通知 catch 块在 try 块中发生了错误。这个 try 块也称为异常产生块。catch 块负责捕获 try 块抛出的异常。当 try 块抛出异常时，程序的控制权转移到 catch 块；如果参数如前面所解释的那样匹配，则异常被捕获。如果没有抛出异常，则忽略 catch 块，控制权转移到 catch 块之后的下一条语句。

```cpp
/* PROG 14.1 DEMO OF EXCEPTION HANDLING */

#include <iostream.h>
void main()
{
    try
    {
        throw "DEMO OF EXCEPTION";
    }
    catch(char* E)
    {
        cout << "Exception caught=" << E << endl;
    }
    cout << "Continue after catch block" << endl;
}
```

### 输出

```
Exception caught=DEMO OF EXCEPTION
Continue after catch block
```

![](img/ad5299318df8d4d7c6df5eaa86590ea3_664_0.png)

图 14.1 程序 14.1 的输出屏幕
