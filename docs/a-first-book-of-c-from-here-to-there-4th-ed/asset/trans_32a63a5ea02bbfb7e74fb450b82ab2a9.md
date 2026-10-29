

## 表13.4 deque类方法与操作总结

| 方法与操作 | 类型 | 描述 |
|---|---|---|
| deque<DataType> name | 构造函数 | 创建一个名为name的空deque，初始大小由编译器决定 |
| deque<DataType> name(source) | 构造函数 | 创建source deque的副本 |
| deque<DataType> name(n) | 构造函数 | 创建一个大小为n的deque |
| deque<DataType> name(n, object) | 构造函数 | 创建一个大小为n的deque，每个对象都初始化为object |
| deque<DataType> name(src.beg, src.end) | 构造函数 | 创建一个deque，使用源容器中从src.beg开始到src.end结束的对象进行初始化 |
| ~deque<DataType>() | 析构函数 | 销毁deque及其包含的所有对象 |
| name.at(index) | 访问器 | 返回index处的对象，如果索引越界则抛出异常 |
| name.front() | 访问器 | 返回deque前端的第一个对象，不检查第一个对象是否存在 |
| name.pop_front() | 修改器 | 移除deque前端的第一个对象，但不返回它 |
| name.push_front(object) | 修改器 | 在deque前端插入object |
| name.back() | 访问器 | 返回deque后端的最后一个对象，不检查最后一个对象是否存在 |
| name.pop_back() | 修改器 | 移除deque后端的最后一个对象，但不返回它 |
| name.push_back(object) | 修改器 | 在deque后端插入object |
| name.insert(itr, object) | 修改器 | 在迭代器位置itr处插入object |
| name.insert(itr, src.beg, src.end) | 修改器 | 在迭代器位置itr处插入对象 |

| 方法与操作 | 类型 | 描述 |
|---|---|---|
| name.insert(itr, n, object) | 修改器 | 在迭代器位置itr处插入n个object副本 |
| name2.assign(n, object) | 修改器 | 分配n个object副本 |
| name2(src.begin, src.end) | 修改器 | 将src容器（不一定是deque）在src.begin和src.end范围内的对象分配给name2 |
| name.erase(pos) | 修改器 | 移除指定位置pos处的对象 |
| name.erase(begin, end) | 修改器 | 移除指定范围内的对象 |
| name.resize(value) | 修改器 | 将deque调大，新对象通过默认构造函数实例化 |
| name.resize(value, object) | 修改器 | 将deque调大，新对象实例化为object |
| name.clear() | 修改器 | 移除deque中的所有对象 |
| name.swap(nameB) | 修改器 | 交换name和nameB deque中的对象；可以使用swap()算法执行 |
| name.begin() | 访问器 | 返回指向deque中第一个对象的迭代器 |
| name.end() | 访问器 | 返回指向deque中最后一个对象之后位置的迭代器 |
| name.rbegin() | 访问器 | 返回指向deque中第一个对象的反向迭代器 |
| name.rend() | 访问器 | 返回指向deque中最后一个对象之后位置的反向迭代器 |
| nameA == nameB | 关系运算 | 如果所有nameA对象等于nameB对象，则返回布尔值true；否则返回false |

## 栈

| 方法与操作 | 类型 | 描述 |
|---|---|---|
| `nameA != nameB` | 关系运算 | 如果所有`nameA`对象等于`nameB`对象，则返回布尔值`false`；否则返回`true`；等同于`!(nameA == nameB)` |
| `nameA < nameB` | 关系运算 | 如果`nameA`小于`nameB`，则返回布尔值`true`；否则返回`false` |
| `nameA > nameB` | 关系运算 | 如果`nameA`大于`nameB`，则返回布尔值`true`；否则返回`false`；等同于`nameB < nameA` |
| `nameA <= nameB` | 关系运算 | 如果`nameA`小于或等于`nameB`，则返回布尔值`true` |
| `nameA >= nameB` | 关系运算 | 如果`nameA`大于或等于`nameB`，则返回布尔值`true` |
| `name.size()` | 容量 | 以整数形式返回deque中的对象数量 |
| `name.empty()` | 容量 | 如果deque为空，则返回布尔值`true`；否则返回`false` |
| `name.max_size()` | 容量 | 以整数形式返回最大可能对象数 |
| `name.capacity()` | 容量 | 以整数形式返回不重新定位deque时的最大可能对象数 |

程序13.3使用deque类实现了一个栈。这个程序很直接，只实例化了一个栈，用户输入的姓名会被推入deque的前端，直到输入哨兵值x为止。检测到这个哨兵字符串值后，只要deque不为空，就会从deque前端弹出姓名。

## 信息点

## 将双端队列用作栈

栈和队列是更通用数据对象deque（代表“double-ended queue”，发音为“deck”）的两种特殊形式。在deque对象中，数据可以通过以下四种方式之一进行处理：

- 1. 在开头插入并从开头移除，这是一种后进先出（LIFO）栈。
- 2. 在开头插入并从末尾移除，这是一种先进先出（FIFO）队列。
- 3. 在末尾插入并从末尾移除，这表示一种反向的LIFO技术。
- 4. 在末尾插入并从开头移除，这表示一种反向的FIFO队列。

本部分讨论实现1（栈对象），下一部分介绍实现2（队列对象）。实现3和4有时用于跟踪内存地址，例如使用机器语言编程或在文件中处理对象时。当C++等高级语言自动管理数据区时，用户可能不会意识到数据存储在哪里，或正在应用哪种类型的deque。

## 程序13.3

```
#include <iostream>
#include <deque>
#include <string>
#include <cctype>
using namespace std;

int main()
{
    string name;
    deque<string> stack;

    cout << "Enter as many names as you want, one per line" << endl;
    cout << "To stop enter a single x" << endl;
    while(true)
    {
        cout << "Enter a name (or x to stop): ";
        getline(cin, name);
        if (tolower(name.at(0)) == 'x') break;
        stack.push_front(name);
    }

cout << "\nThe names in the stack are:\n";

// pop names from the stack
while(!stack.empty())
{
    name = stack.front();  // retrieve the name
    stack.pop_front();     // pop name from the stack
    cout << name << endl;
}
return 0;
}
```

以下是程序13.3的示例运行：

```
Enter as many names as you want, one per line
    To stop enter a single x
Enter a name (or x to stop): Jane Jones
Enter a name (or x to stop): Bill Smith
Enter a name (or x to stop): Jim Robinson
Enter a name (or x to stop): x

The names in the stack are:
Jim Robinson
Bill Smith
Jane Jones
```

## 练习13.3

- 1. **（复习）** 判断栈是否适用于以下各项任务，并说明原因：
  - a. 文字处理程序必须记住一行最多80个字符。按Backspace键删除前一个字符，按Ctrl+Backspace删除整行。用户必须能够撤销删除操作。
  - b. 客户必须等待一到三个月才能提到新车。经销商创建一份列表，以确定客户获得汽车的“公平”顺序；该列表按照客户提交新车请求的顺序编制。
  - c. 你需要在一堆杂志中向下查找，找到去年一月的那一期。每本杂志一收到就被放到这堆杂志上。
  - d. 一个编程团队接受任务，并根据紧急程度对其进行优先级排序。
  - e. 在公交站排成一队。

- 2. **（练习）** 输入并运行程序13.3。

- 3. **（修改）** 修改程序13.3，实现一个整数栈，而不是字符串栈。

