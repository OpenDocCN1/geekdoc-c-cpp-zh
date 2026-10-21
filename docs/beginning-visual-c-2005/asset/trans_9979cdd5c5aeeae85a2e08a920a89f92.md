
CBox 可用体积为 120
CBox 可用体积为 102

现在将箱子压入堆栈...
将箱子弹出堆栈时，它们以相反的顺序呈现：
CBox 可用体积为 102
CBox 可用体积为 120
CBox 可用体积为 20.4
CBox 可用体积为 24

现在将整数压入堆栈：
    2    4    6    8    10    12

从堆栈弹出整数，结果如下：
    12    10    8    6    4    2
按任意键继续 . . .

## 工作原理

用于存储 Box 对象句柄的堆栈在以下语句中定义：

```
Stack<Box^>^ stack = gcnew Stack<Box^>;          // 创建堆栈
```

类型参数是 Box^，因此堆栈存储的是 Box 对象或 GlassBox 对象的句柄。将对象压入堆栈以及将其弹出的代码与 Ex9_14 中的完全相同，输出也相同。这里的区别在于：如果类型没有将 Box 作为直接或间接基类，则无法将对象压入堆栈，因此泛型类型保证了所有对象都是 Box 对象。

现在存储整数需要一个新的 Stack<> 对象：

```
Stack<int>^ numbers = gcnew Stack<int>;          // 创建堆栈
```

原始版本使用同一个非泛型 Stack 对象来存储 Box 对象引用和整数，从而说明了堆栈操作完全缺乏类型安全。这里你将泛型类的类型参数指定为值类型 int，因此只有该类型的对象才会被 Push() 函数接受。

从堆栈弹出对象的循环表明，Pop() 函数中的返回 T() 对于 int 类型确实返回 0，对于句柄类型 Box^ 则返回 nullptr。

## 泛型接口类

你可以像定义泛型引用类一样定义泛型接口，并且泛型引用类可以根据泛型接口来定义。为了说明其工作方式，你可以定义一个由泛型类 Stack<> 实现的泛型接口。下面是一个泛型接口的定义：

```
// 堆栈操作的接口
generic<typename T> public interface class IStack
{
    void Push(T obj);     // 将项压入堆栈
    T Pop();
};

| 类型 | 描述 |
|---|---|
| List<T> | 将类型 T 的项存储在一个简单列表中，必要时可自动增长大小。 |
| LinkedList<T> | 将类型 T 的项存储在双向链表中。 |
| Stack<T> | 将类型 T 的项存储在堆栈中，这是一种后进先出的存储机制。 |
| Queue<T> | 将类型 T 的项存储在队列中，这是一种先进先出的存储机制。 |
| Dictionary<K,V> | 存储键/值对，其中键的类型为 K，值的类型为 V。 |

我不会详细介绍所有这些集合类，但会简要提及你最可能在程序中使用的三个。为简单起见，我的示例将存储值类型，但当然这些集合类同样适用于引用类型。

## List<T> —— 泛型列表

List<T> 定义了一个泛型列表，该列表在必要时会自动增大容量。你可以使用 Add() 函数向列表中添加项，也可以像数组一样使用索引访问存储在 List<T> 中的项。下面是如何定义一个存储 int 类型值的列表：

```
List<int> numbers = gcnew List<int>;
```

这有一个默认容量，但你也可以指定所需的容量。下面是一个容量为 500 的列表定义：

```
List<int> numbers = gcnew List<int>;
```

你可以使用 Add() 函数向列表中添加对象：

```
for(int i = 0 ; i<1000 ; i++)
    numbers->Add( 2*i+1);
```

这将 1000 个整数添加到 numbers 列表中。如果列表的容量小于 1000，列表会自动增长。当你想在现有列表中插入项时，可以使用 Insert() 函数将第二个参数指定的项插入到第一个参数指定的索引位置。列表中的项像数组一样从零开始索引。

你可以像这样对列表的内容求和：

```
int sum = 0;
for(int i = 0 ; i<numbers->Count ; i++)
    sum += numbers[i];
```

Count 是一个属性，返回列表中当前的项数。可以通过默认索引属性访问列表中的项，并可以通过这种方式获取和设置值。请注意，你

## 类继承与虚函数

不能使用默认索引属性来增加列表的容量。如果在列表当前项范围之外使用索引，将会抛出异常。

你也可以像这样对列表中的项求和：

```
for each(int n in numbers)
    sum += n;
```

你还可以对列表应用许多其他函数，包括删除元素、排序和搜索列表内容的函数。

### LinkedList<T> —— 泛型双向链表

LinkedList<T> 定义了一个带有前向和后向指针的链表，因此你可以沿任一方向遍历链表。你可以像这样定义一个存储浮点数的链表：

```
LinkedList<double>^ values = gcnew LinkedList<double>;
```

你可以像这样向列表中添加值：

```
for(int i = 0 ; i<1000 ; i++)
    values->AddLast(2.5*i);
```

AddLast() 函数将一个项添加到列表末尾。你可以使用 AddFirst() 函数将项添加到列表开头。或者，你也可以使用 AddHead() 和 AddTail() 函数来完成同样的操作。

Find() 函数返回一个 LinkedListNode<T>^ 类型的句柄，指向列表中包含你作为参数传递给 Find() 的值的节点。你可以使用这个句柄在找到的节点之前或之后插入一个新值。例如：

```
LinkedListNode<double>^ node = values->Find(20.0); // 查找包含 20.0 的节点
if(node != nullptr)
    values->AddBefore(node, 19.9); // 在节点前插入 19.9
```

第一条语句找到包含值 20.0 的节点。如果该节点不存在，Find() 函数返回 nullptr。最后一条语句在 node 不为 null 时执行，在 node 之前添加一个新值 19.9。你可以使用 AddAfter() 函数在给定节点之后添加一个新值。搜索链表相对较慢，因为必须按顺序遍历元素。

你可以像这样对列表中的项求和：

```
double sumd = 0;
for each(double v in values)
    sumd += v;
```

for each 循环遍历列表中的所有项，并将总和累加到 sum 中。

Count 属性返回链表中的项数，Head 和 Tail 属性返回第一项和最后一项的值。First 和 Last 属性是 Head 和 Tail 的替代项。

### Dictionary<TKey, TValue> —— 存储键/值对的泛型字典

泛型 Dictionary<> 集合类需要两个类型参数，第一个是键的类型，第二个是与键关联的值的类型。当你有一对想要存储的对象，且其中一个对象是访问另一个对象的键时，字典尤其有用。姓名和电话号码是键值对的一个例子，你可能希望将其存储在字典中，因为你通常希望使用姓名作为键来检索电话号码。假设你已定义了 Name 和 PhoneNumber 类来分别封装姓名和电话号码。你可以像这样定义一个存储姓名/号码对的字典：

```
Dictionary<Name^, PhoneNumber^> phonebook = gcnew Dictionary<Name^, PhoneNumber^>;
```

两个类型参数是 Name^ 和 PhoneNumber^，因此键是姓名的句柄，值是电话号码的句柄。

```
Name^ name = gcnew Name("Jim", "Jones");
PhoneNumber^ number = gcnew PhoneNumber(914, 316, 2233);
phonebook->Add(name, number); // 将姓名/号码对添加到字典
```

要检索字典中的条目，你可以使用默认索引属性（例如：

```
try
{
	PhoneNumber^ theNumber = phonebook[name];
}
catch(KeyNotFoundException^ knfe)
{
	Console::WriteLine(knfe);
}
```

你将键作为默认索引属性的索引值提供，在本例中是 Name 对象的句柄。如果键存在，则返回值；如果集合中未找到该键，则抛出 KeyNotFoundException 类型的异常；因此，每当你访问一个可能不存在的键的值时，代码应置于 try 块中。

Dictionary<> 对象具有 Keys 属性，返回包含字典中键的集合；还具有 Values 属性，返回包含值的集合。Count 属性返回字典中键/值对的数量。

让我们在一个可运行的示例中试用其中的一些功能。

## 试一试

### 使用泛型集合类

此示例演示了你已见过的三个集合类：

```
// Ex9_22.cpp : 主项目文件。
// 使用泛型集合类
#include "stdafx.h"
using namespace System;
```

