
入队、初始化队列、检查队列是否为空，以及检查队列是否已满。

13. 队列可以用数组或链表实现。
14. 不应直接访问队列的中间元素。
15. 队列是数组和链表的受限版本。

## 练习

练习末尾括号中的数字指的是本章开头列出的学习目标。

1. 判断以下陈述为真或假。
    a. 栈是同质元素组成的列表，其中元素的添加和删除只在一端发生。(1)
    b. 栈是一种先进后出的数据结构。(1)
    c. 在栈的数组实现中，`stackTop` 包含栈中栈顶元素的索引。(2)
    d. 在栈的数组实现中，要删除栈顶元素，如果栈非空，操作 `pop` 会将 `stackTop` 的值减 1。(3)
    e. 在栈的数组实现中，操作 `top` 返回栈顶元素的索引。(3)
    f. 在栈的链式实现中，`stackTop` 包含栈中栈顶元素的地址。(4)
    g. 在栈的链式实现中，如果栈已满，操作 `isEmptyStack` 返回 `true`。(4)
    h. 在后缀表达式中，操作数写在运算符之后。(5)
    i. 队列是一种先进先出的数据结构。(7)
    j. 在队列中，新元素添加到队列末尾。(8)
    k. 在队列的数组实现中，操作 `deleteQueue` 将 `count` 减 1，并将 `queueFront` 前进到下一个元素。(9)
    l. 在队列的链式实现中，如果 `queueFront == queueRear`，则队列为空。(10)
    m. 在计算机模拟中，被研究的对象通常表示为操作。(11)
    n. 模拟问题使用栈来解决。(11)

2. 假设 `stack` 是 `stackType<int>` 类型的对象。`stack.stackTop` 和 `stack.stackTop - 1` 之间有什么区别？(3)

3. 假设 `stack` 是 `stackType<double>` 类型的对象，且 `stack.stackTop` 的值为 5。栈顶元素的索引是多少？(3)

4. 假设 `stack` 是 `stackType<string>` 类型的对象，且 `stack.stackTop - 1` 的值为 2。栈中有多少个元素？(3)

5. 考虑以下语句：(3)

下列代码段输出什么：

```
stackType<int> stack;
int num1, num2;

stack.push(12);
stack.push(5);
num1 = stack.top() + 3;
stack.push(num1 + 5);
num2 = stack.top();
stack.push(num1 + num2);
num2 = stack.top();
stack.pop();
stack.push(15);
num1 = stack.top();
stack.pop();
while (!stack.isEmptyStack())
{
    cout << stack.top() << " ";
    stack.pop();
}
cout << endl;
cout << "num1 = " << num1 << endl;
cout << "num2 = " << num2 << endl;
```

6. 考虑以下语句：(3)

假设输入为：

```text
31 47 86 39 62 71 15 63
```

下列代码段输出什么：

```cpp
stackType<int> stack(50);
int num;

cin >> num;

while (cin)
{
    if (!stack.isFullStack())
    {
        if (num % 2 == 0 || num % 3 == 0)
            stack.push(num);
        else if (!stack.isEmptyStack())
        {
            cout << stack.top() << " ";
            stack.pop();
        }
    }
    else
        stack.push(num + 3);
}
```

   c.  ((x - y) + (z - w) / t) * u
   d.  x - y / (z + w) * t / u + (v - s)

11. 写出以下后缀表达式的等价中缀表达式：(5)

    a.  x y + z * w -
    b.  x y * z / w +
    c.  x y z + * w -

12. 下列程序的输出是什么？(3)

```cpp
#include <iostream>
#include <string>
#include "myStack.h"

using namespace std;

template <class type>
void mystery(stackType<type>& s1, stackType<type>& s2,
             stackType<type>& s3);

int main()
{
    stackType<string> stack1;
    stackType<string> stack2;
    stackType<string> newStack;

    string fNames[] = {"Chelsea", "Kirk", "David", "Stephanie",
                       "Bianca", "Katie", "Holly"};
    string lNames[] = {"Jackson", "McCarthy", "Miller", "Pratt",
                       "Holman", "Smith", "Klien"};

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

13. 下列程序的输出是什么？(3)

```cpp
#include <iostream>
#include <cmath>
#include "myStack.h"

using namespace std;

void mystery(stackType<int>& s, stackType<double>& t);

int main()
{
    int list[] = { 1, 2, 3, 4, 5};

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

14. 解释为什么在栈的链式实现中，不需要实现用于判断栈是否已满的操作。(4)

15. 假设 stack 是 `linkedStackType<int>` 类型的对象。语句 `stack.top();` 和 `stack.pop();` 之间有什么区别？(4)

16. 编写函数模板 `printListReverse` 的定义，该函数使用栈按逆序打印链表。假设该函数是第16章设计的类 `linkedListType` 的成员。(6)

17. 编写方法 `second` 的定义，该方法以栈对象为参数并返回栈的第二个元素。原栈保持不变。(3, 4)

18. 考虑以下语句：(8, 9)

```cpp
queueType<int> queue;
int num;
```

下列代码段输出什么：

```cpp
num = 7;
queue.addQueue(6);
queue.addQueue(num);
num = queue.front();
queue.deleteQueue();
queue.addQueue(num + 5);
queue.addQueue(14);
queue.addQueue(num - 2);
queue.addQueue(25);
queue.deleteQueue();

cout << "Queue elements: ";
while (!queue.isEmptyQueue())
{
    cout << queue.front() << " ";
    queue.deleteQueue();
}
cout << endl;
```

19. 考虑以下语句：(4, 10)

```cpp
linkedStackType<int> stack;
linkedQueueType<int> queue;
int num;
```

假设输入为：

48 35 72 88 92 11 10 15 44 52 67 36

下列代码段会输出什么：

```cpp
stack.push(0);
queue.addQueue(0);
cin >> num;

while (cin)
{
    switch (num % 3)
    {
        case 0:
            stack.push(num);
            break;
        case 1:
            queue.addQueue(num);
            break;
        case 2:
            if (!stack.isEmptyStack())
            {
                cout << stack.top() << " ";
                stack.pop();
            }
            else if (!queue.isEmptyQueue())
            {
                cout << queue.front() << " ";
                queue.deleteQueue();
            }
            else
                cout << "Stack and queue are empty." << endl;
            break;
    } //end switch

    cin >> num;
} //end while
cout << endl;
cout << "stack: ";
while (!stack.isEmptyStack())
{
    cout << stack.top() << " ";
    stack.pop();
}

cout << endl;
cout << "queue: ";
while (!queue.isEmptyQueue())
{
    cout << queue.front() << " ";
    queue.deleteQueue();
}
cout << endl;
```

![](img/d0be7fc6d804b63484835c6c8bc67a07_1307_0.png)

20. 以下函数做什么？(3, 9)

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

