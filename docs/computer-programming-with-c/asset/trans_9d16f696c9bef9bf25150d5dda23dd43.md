

## 输出

```text
Added 10
Added 20
Added 30
**********Order of removing elements**************
10
20
30
```

## 错误查找练习

以下是一些可能包含错误或没有错误的程序。如果代码中存在错误，请纠正它们，并在应用修正后确定输出。

## 程序 1

```cpp
template <class G>
int a=0,b=0;
G add(G a,G b)
{
```

```cpp
cout<<"Full List"<<endl;
for(temp = l1.begin();temp != l1.end() ; temp++)
{
    cout<<*temp<<" ";
}
}
```

## 程序 4

```cpp
using namespace std;
#include<iostream>
template <class G1,class G2>
G2 add(G1 a,G2 b)
{
G2 c = a+b;
return c;
}
template <class G1,class G2>
G2 add(G2 a,G1 b)
{
G2 c = a+b;
return c;
}


void main()
{
int x;
float y,res1;
cout<<"Enter values of x and y"<<endl;
cin>>x>>y;
res1=add(x,y);
cout<<"Addition of x and y is "<<res1<<endl;
}
```

## 复习题

- 1. 举例说明类模板和函数模板的用法。
- 2. 解释 vector 和链表之间的区别。
- 3. 什么是 map？它的应用有哪些？
- 4. 编写一个 C++ 程序，使用内置的 list 类创建一个 Employee 对象的链表。为每个员工存储工资，并按工资对链表进行排序。将链表中存储的 Employee 对象按工资升序排列。
- 5. 什么是迭代器？迭代器有哪些不同类型？
- 6. 栈和队列之间的区别是什么？解释这两种数据结构的实现。

## 第17章 | C++中的异常处理

### 17.1 概述

异常是程序中的一种异常情况，如果程序员不处理它，可能会导致程序终止。以下是一些异常示例：

- 1. 如果你在程序中意外执行除以零的操作，则称为除以零异常。
- 2. 如果你访问数组索引特定边界之外的数组元素，则称为数组索引越界异常。例如，如果数组 a 的大小为 5，你意外尝试访问不存在的 a[7]，则可能产生逻辑上不正确的结果，这就是一种异常。
- 3. 如果你的程序需要从用户处输入员工的工资，但用户错误地输入了一个负数，则称为无效输入异常。
- 4. 如果你的程序正在向文件写入内容，但该文件是只读的，则执行输出操作时存在访问权限违反，这也是异常的一个示例。
- 5. 在网络通信中，如果你编写自己的 C++ 客户端与同一网络上的服务器通信，并且当你在客户端程序中发送消息时服务器已关闭，则称为“资源不可用”类型的异常。

根据具体情况，你的程序中可能还会出现更多特定类型的异常。重要的是要理解什么是异常，以及如何有效地处理它们，以确保在异常发生时程序不会突然终止。程序员有责任创建健壮的程序，即使在发生任何异常情况时也不会突然失败。

> **注意**
>
> 异常和错误之间是有区别的。如果程序中有错误，程序肯定会失败。例如，语句后缺少分号是语法错误；运行大型循环时程序内存不足是内存错误，等等。错误无法处理，因此当错误发生时程序必然会失败。而异常是可以在程序中处理的，从而避免程序突然失败。C++ 中的异常处理器用于处理异常（而不是错误）。任何异常只要得到适当处理，即使发生异常也能避免程序突然终止。然而，如果异常未被处理，它会在发生时立即终止程序。

### 17.2 C++ 中的异常处理器

try-catch 块是 C++ 中的异常处理器。程序中可能产生异常的部分必须放在 try 块中。catch 块包含一段仅在特定异常发生时执行的代码。以下是在 C++ 中编写 try-catch 块的语法：

```cpp
try
{
/*Code which has a possibility of exception*/
}
catch(exceptionType1 variable1)
{
/*Handler for exceptionType1*/
}
catch(exceptionType2 variable2)
{
/*Handler for exceptionType2*/
}
catch(exceptionType3 variable3)
{
/*Handler for exceptionType3*/
}
...
catch(exceptionTypeN variableN)
{
/*Handler for exceptionTypeN*/
}
```

![](img/57c0d966bb33c67a5a188e6bf39e4e02_985_0.png)

在单个 try 块之后可以有多个 catch 块。每个 catch 块专门处理特定类型的异常。在上面的示例中，如果 try 块中出现了 `exceptionType3` 的异常，则执行控制将转移到第三个 catch 块，跳过前两个 catch 块。

总之，这意味着控制会根据 try 块中的异常类型转移到正确的 catch 块。在最好的情况下，如果 try 块中没有异常，则不会执行任何 catch 块，执行控制将转移到最后一个 catch 块之后的语句，从而跳过所有 catch 块，如图 17.1 所示。

### 17.3 throw 关键字

throw 关键字用于生成异常。throw 语句的语法是

```cpp
throw <Exception>;

或

throw;
```

我们稍后会看到这些语法各自的示例。目前，你只需要理解：无论何时需要在程序中生成异常，都必须使用 throw 关键字。

### 17.4 示例

#### 17.4.1 数组索引越界异常：一个示例

作为第一个示例，让我们创建一个 C++ 程序来处理数组索引越界异常。这里，我们想象一种情况：程序意外地尝试访问数组中超出其索引允许范围的元素。考虑以下程序，它使用初始化块创建了一个大小为 5 的数组 a。然后，我们从用户处输入 i 的值，并打印数组中位置 i 处的元素。

```cpp
#include<iostream.h>
void main()
{
int a[] = {10,20,30,40,50};
int i;
cout<<"Enter index of an array"<<endl;
cin>>i;
cout<<"Element at position"<<i<<"is"<<a[i]<<endl;
}
```

```text
Output
Enter index of an array
7
Element at position 7 is -82103460
```

如果用户输入 i 的值在 0 到 4 之间（即数组的边界），程序会完美运行。然而，如果用户输入无效的 i 值，上述程序存在失败（产生错误结果）的风险。例如，假设用户输入的 i 值为 7，如输出所示，程序会生成一个存储在该位置的垃圾值。我们知道 a[7] 不存在，因为数组大小只有 5。因此，程序无法在输出中生成逻辑正确的值。这称为**程序崩溃**。我们可以使用**异常处理**来避免这种情况。以下是使用异常处理重写的程序：

```cpp
#include<iostream.h>
void main()
{
int a[] ={10,20,30,40,50};
int i;
    try {
        cout<<"Enter index of an array"<<endl;
        cin>>i;
        if(i<0 || i>4)
        {
            throw i;
            cout<<"This statement will not be executed"<<endl;
        }
        else
        {
            cout<<"Element at position "<<i<<" is "<<a[i]<<endl;
        }
    }
    catch(int t)
    {
        cout<<"Invalid array index "<<t<<endl;
    }
    cout<<"Good Bye"<<endl;
}
```

```text
Output
Enter index of an array
7
Invalid array index 7
Good Bye
```

可能产生异常的语句放在 try 块中。程序使用 cin 语句输入 i 的值。实际上，cin 语句是在 try 块内部还是外部并不重要。我们有意识地将它放在 try 块内部，因为正是通过 i 的值，我们才能决定是否生成异常。下面的 if 块检查用户输入的 i 值是否是数组的有效索引。由于数组大小为 5，有效索引

