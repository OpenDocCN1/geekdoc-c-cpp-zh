
**12.** 以下程序的输出是什么？

```cpp
#include <iostream>
#include <string>
#include "myStack.h"

using namespace std;

template <class type>
void mystery(stackType<type>& s1, stackType<type>& s2, stackType<type>& s3);

int main()
{
    stackType<string> stack1;
    stackType<string> stack2;
    stackType<string> newStack;

    string fNames[] = {"Chelsea", "Kirk", "David",
                       "Stephanie", "Bianca", "Katie", "Holly"};
    string lNames[] = {"Jackson", "McCarthy", "Miller",
                       "Pratt", "Holman", "Smith", "Klien"};

    for (int i = 0; i < 7; i++)
    {
        stack1.push(fNames[i]);
        stack2.push(lNames[i]);
    }

    mystery(stack1, stack2, newStack);

    while (!newStack.isEmptyStack())
    {
        cout << newStack.top() << endl;
        newStack.pop();
    }
}

template <class type>
void mystery(stackType<type>& s1, stackType<type>& s2,
             stackType<type>& s3)
{
    while (!s1.isEmptyStack() && !s2.isEmptyStack())
    {
        s3.push(s1.top() + " " + s2.top());
        s1.pop();
        s2.pop();
    }
}
```

**13.** 以下程序的输出是什么？

```cpp
#include <iostream>
#include <cmath>
#include "myStack.h"

using namespace std;

void mystery(stackType<int>& s, stackType<double>& t);

int main()
{
    int list[] = {1, 2, 3, 4, 5};

    stackType<int> s1;
    stackType<double> s2;

    for (int i = 0; i < 5; i++)
        s1.push(list[i]);

    mystery(s1, s2);

    while (!s2.isEmptyStack())
    {
        cout << s2.top() << " ";
        s2.pop();
    }
    cout << endl;
}

void mystery(stackType<int>& s, stackType<double>& t)
{
    double x = 1.0;

    while (!s.isEmptyStack())
    {
        t.push(pow(s.top(), x));
        s.pop();
        x = x + 1;
    }
}
```

**14.** 解释为什么在栈的链式实现中，没有必要实现用于判断栈是否已满的操作。

**15.** 假设 stack 是 linkedStackType<int> 类型的对象。语句 stack.top(); 和 stack.pop(); 之间有什么区别。

**16.** 编写函数模板 printListReverse 的定义，它使用栈以逆序打印链表。假设此函数是第 16 章设计的类 linkedListType 的成员。

**17.** 编写方法 second 的定义，它接受一个栈对象作为参数并返回栈的第二个元素。原始栈保持不变。

**18.** 假设 `queue` 是大小为 50 的 `queueType<int>` 类型对象，queue 的第一个元素索引是 7，最后一个元素索引是 25。还假设 `num` 是 `int` 类型变量。(9)

- a. queue 中有多少个元素？
- b. 编写将 queue 的第一个元素赋给 `num` 的语句。
- c. 编写删除 queue 第一个元素的语句。
- d. 编写将 28 插入 queue 的语句。

**19.** 假设 `queue` 是大小为 50 的 `queueType<string>` 类型对象，queue 包含 20 个元素，且 queue 第一个元素索引是 35。(9)

- a. queue 最后一个元素的索引是多少？
- b. 从 queue 中删除下一个元素后，第一个元素的索引是多少？
- c. 编写表达式，如果 queue 非空返回 `true`，否则返回 `false`。
- d. 编写将 **"programming"** 插入 queue 的语句。此插入操作后最后一个元素的索引是多少？

**20.** 以下代码段输出什么：

```cpp
queueType<int> queue;
int temp = 20;

queue.addQueue(15);
queue.addQueue(8);
queue.addQueue(temp);
queue.addQueue(42);
temp = queue.front();
queue.deleteQueue();
queue.addQueue(temp - 10);
queue.addQueue(16);
queue.addQueue(2 * temp);
queue.deleteQueue();

cout << "Queue elements: ";
while (!queue.isEmptyQueue())
{
    cout << queue.front() << " ";
    queue.deleteQueue();
}
cout << endl;
cout << "temp = " << temp << endl;
```

![](img/b217c421655b51e7494cf3b89bb5432d_1320_0.png)

**21.** 考虑以下语句：

```cpp
linkedStackType<int> stack;
linkedQueueType<int> queue;
int num;
```

假设输入为

```
28 30 15 11 10 -9 21 8 -3 33 17 14
```

编写 C++ 代码按如下方式处理这些数字：如果数字是偶数，则将其压入栈。如果数字是奇数且能被 3 整除，则将其加入队列；否则，如果栈中有元素，则移除栈中的元素，并将该数字的平方压入栈。处理完这些数字后，栈和队列中存储的是什么？

**22.** 以下函数做什么？

```cpp
void mystery(queueType<int>& q)
{
    stackType<int> s;

    while (!q.isEmptyQueue())
    {
        s.push(q.front());
        q.deleteQueue();
    }

    while (!s.isEmptyStack())
    {
        q.addQueue(2 * s.top());
        s.pop();
    }
}
```

**23.** 假设 queue 是 queueType 对象，实现 queue 的数组大小为 65。还假设 queueFront 的值为 35，queueRear 的值为 60。(9)

- a. queue 中有多少个元素？
- b. 向 queue 添加一个元素后，queueFront 和 queueRear 的值分别是多少？
- c. 从 queue 删除一个元素后，queueFront 和 queueRear 的值分别是多少？

**24.** 假设 queue 是 queueType 对象，实现 queue 的数组大小为 65。还假设 queueFront 的值为 63，queueRear 的值为 20。(9)

- a. queue 中有多少个元素？
- b. 向 queue 添加一个元素后，queueFront 和 queueRear 的值分别是多少？
- c. 从 queue 删除两个元素后，queueFront 和 queueRear 的值分别是多少？

**25.** 假设 `queue` 是 **queueType** 对象，实现 queue 的数组大小为 65。还假设 **queueFront** 的值是 25，**queueRear** 的值是 55。(9)

- a. queue 中有多少个元素？
- b. 向 queue 添加一个元素后，**queueFront** 和 **queueRear** 的值分别是多少？
- c. 从 queue 删除一个元素后，**queueFront** 和 **queueRear** 的值分别是多少？

**26.** 假设 `queue` 是 **queueType** 对象，实现 queue 的数组大小为 65。还假设 **queueFront** 的值是 64，**queueRear** 的值是 64。(9)

- a. queue 中有多少个元素？
- b. 向 queue 添加一个元素后，**queueFront** 和 **queueRear** 的值分别是多少？
- c. 从 queue 删除一个元素后，**queueFront** 和 **queueRear** 的值分别是多少？

**27.** 假设 `queue` 实现为带有特殊保留槽的数组，如本章所述。还假设实现 queue 的数组大小为 100。如果 **queueFront** 的值是 50，第一个队列元素的位置是什么？(9)

**28.** 假设 `queue` 实现为带有特殊保留槽的数组，如本章所述。假设实现 queue 的数组大小为 100。还假设 **queueFront** 的值是 74，**queueRear** 的值是 99。(9)

- a. 向 queue 添加一个元素后，**queueFront** 和 **queueRear** 的值分别是多少？
- b. 从 queue 删除一个元素后，**queueFront** 和 **queueRear** 的值分别是多少？被删除的队列元素的位置是什么？

**29.** 考虑以下语句：

```cpp
linkedQueueType<int> queue;
linkedStackType<int> stack;
long long num;
int digit1, digit2;
```

如果输入是 837298651020706，以下代码段输出什么。(4, 10)

```cpp
cin >> num;

num = abs(num);

while (num > 0)
{
    stack.push(num % 10);
    num = num / 10;
}

while (!stack.isEmptyStack())
{
    queue.addQueue(stack.top());
    stack.pop();
}

if (!queue.isEmptyQueue())
{
    digit1 = queue.front();
    queue.deleteQueue();
}

while (!queue.isEmptyQueue())
{
    digit2 = queue.front();
    queue.deleteQueue();
    cout << digit1 - digit2 << " ";
    digit1 = digit2;
}
cout << endl;
```

**30.** 练习 29 中的程序段做什么？(4, 10)

**31.** 编写函数模板 `reverseStack`，它接受一个栈对象作为参数，并使用一个队列对象来反转栈中元素。

**32.** 编写函数模板 `reverseQueue`，它接受一个队列对象作为参数，并使用一个栈对象来反转队列中元素。

**33.** 向 `class queueType`（队列的数组实现）添加操作 `queueCount`，它返回队列中元素个数。编写实现此操作的函数模板定义。

**34.** 绘制 `class linkedStackType` 的 UML 图。(4)

**35.** 绘制 `class queueADT` 的 UML 图。(8)

**36.**
- a. 绘制 `class queueType` 的 UML 图。(9)
- b. 绘制 `class linkedQueueType` 的 UML 图。(10)

