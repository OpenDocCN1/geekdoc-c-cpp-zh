
```cpp
#include <iostream>
#include <iomanip>
#include <fstream>
#include "mystack.h"

using namespace std;

void evaluateExpression(ofstack& out, stackType<double>& stack,
    char& ch, bool& isExpOk);
void evaluateOpr(ofstack& out, stackType<double>& stack,
    char& ch, bool& isExpOk);
void discardExp(istream& in, ofstream& out, char& ch);
void printResult(ostream outF, stackType<double>& stack);

int main() {
    bool expressionOk;
    char ch;
    stackType<double> stack;
    ifstream infile;
    ofstream outfile;

    infile.open("RpnData.txt");
    if (!infile) {
        cout << "Cannot open the input file!" << endl;
        return 1;
    }

    outfile.open("RpnOutput.txt");
    outfile << fixed << setprecision(2);

    infile >> ch;
    expressionOk = true;
    stack.initialize();
    
    while (infile >> ch) {
        evaluateExpression(outfile, stack, ch, expressionOk);
        if (!expressionOk) {
            discardExp(infile, outfile, ch);
            expressionOk = true;
        }
    }
    
    if (expressionOk) {
        printResult(outfile, stack);
    }

    infile.close();
    outfile.close();

    return 0;
}
// end main
```

示例运行：

输入文件

```
3 4+ 2*8/=
```

输出

```
7.00
```

# 1162 | 第 19 章：栈与队列

`info` 10。因此，在最初遍历列表移动到最后一个节点时，我们必须保存每个节点的指针。例如，对于图 19–18 中的列表，我们必须保存 `info` 为 5 和 10 的每个节点的指针。在打印 15 后，我们回到 `info` 为 10 的节点；打印 10 后，我们回到 `info` 为 5 的节点。由此推导出，我们必须将每个节点的指针保存在一个栈中，以实现后进先出（Last In First Principle）原则。

由于链表中的节点数量通常未知，我们将使用栈的链表实现。假设栈是一个类型为 `LinkedListType` 的对象，`current` 是一个与指针 `first` 类型相同的指针。考虑以下语句：

```
current = first; //Line 1
while (current != NULL) //Line 2
{
    stack.push(current); //Line 3
    current = current->link; //Line 4
}
```

执行第 1 行的语句后，`current` 指向第一个节点。（参见图 19–19。）

![](img/abc25bb507ebb3eb05460d88ce0e0fde_1202_0.png)

图 19-19 执行语句 `current = first;` 后的列表

由于 `current` 不为 NULL，执行第 3 行和第 4 行的语句。（参见图 19–20。）

![](img/abc25bb507ebb3eb05460d88ce0e0fde_1202_1.png)

图 19-20 执行语句 `stack.push(current);` 和 `current = current->link;` 后的列表和栈

## 消除递归：反向打印链表的非递归算法 | 1163

执行第 4 行的语句后，重新评估第 2 行的循环条件。由于 `current` 不为 NULL，循环条件求值为真，因此执行第 3 行和第 4 行的语句。（参见图 19–21）。

![](img/abc25bb507ebb3eb05460d88ce0e0fde_1203_0.png)

执行第 4 行的语句后，再次评估第 2 行的循环条件。由于 `current` 不为 NULL，循环条件求值为真，因此执行第 3 行和第 4 行的语句。（参见图 19–22）。

![](img/abc25bb507ebb3eb05460d88ce0e0fde_1203_1.png)

执行第 4 行的语句后，再次评估第 2 行的循环条件。由于 `current` 为 NULL，循环条件求值为假，第 2 行的 while 循环终止。从图 19-22 可以看出，链表中每个节点的指针都保存在栈中。栈的顶端元素包含列表中最后一个节点的指针，依此类推。现在让我们执行以下语句：

```
while (!stack.isEmpty()) { //Line 5
    current = stack.top(); //Line 6
    stack.pop(); //Line 7
    cout << current->info << " "; //Line 8
}
```

由于栈不空，第 5 行的循环条件求值为真。因此，执行第 6 行、7 行和 8 行的语句，`current` 指向最后一个节点。第 7 行的语句移除栈的顶端元素。（参见图 19-23。）

![](img/abc25bb507ebb3eb05460d88ce0e0fde_1204_0.png)

图 19-23 执行语句 `current = stack.top();` 和 `stack.pop();` 后的列表和栈

第 8 行的语句输出 `current->info`，其值为 15。接下来，评估第 5 行的循环条件。由于循环条件求值为为真，执行第 6 行、7 行和 8 行的语句。执行第 6 行和第 7 行的语句后，得到图 19–24 的结果。

![](img/abc25bb507ebb3eb05460d88ce0e0fde_1204_1.png)

图 19-24 执行语句 `current = stack.top();` 和 `stack.pop();` 后的列表和栈

第 8 行的语句输出 `current->info`，其值为 10。接下来，评估第 5 行的循环条件。由于循环条件求值为真，执行第 6 行、7 行和 8 行的语句。执行第 6 行和第 7 行的语句后，得到图 19–25。

![](img/abc25bb507ebb3eb05460d88ce0e0fde_1205_0.png)

**图 19-25** 执行语句 `current = stack.top();` 和 `stack.pop();` 后的列表和栈

第 8 行的语句输出 `current->info`，其值为 5。接下来，评估第 5 行的循环条件。由于循环条件求值为真，执行第 6 行、7 行和 8 行的语句。执行第 6 行和第 7 行的语句后，循环条件求值为假，while 循环终止。

# 队列

队列是一种数据结构，元素从一端（称为尾部 `rear`）添加，从另一端（称为前端 `front`）删除；一种先进先出（FIFO）数据结构。与栈一样，队列可以存储在数组或链结构中。我们将考虑两种实现方式。由于元素从一端添加从另一端删除，我们需要两个指针来跟踪队列的头部和尾部，称为 `queueFront` 和 `queueRear`。

# 队列操作

从队列的定义可以看出两个关键操作是添加（add）和删除（delete）。因为不能从空队列删除元素，也不能向满队列添加元素，我们需要两个操作来成功实现 `addQueue` 和 `deleteQueue`：`isEmptyQueue`（检查队列是否为空）和 `isFullQueue`（检查队列是否满）。我们还需要一个操作 `initializeQueue` 将队列初始化为空状态。此外，为了获取队列的第一个和最后一个元素，我们包含了如下列表所示的 **front** 和 **back** 操作。队列的一些操作包括：

- `initializeQueue`: 将队列初始化为空状态。
- `isEmptyQueue`: 确定队列是否为空。如果队列为空，返回 `true`，否则返回 `false`。
- `isFullQueue`: 确定队列是否满。如果队列已满，返回 `true`，否则返回 `false`。
- **front**: 返回前端，即队列的第一个元素。该操作的输入为队列。执行此操作之前，队列必须存在且为空。
- **back**: 返回队列的最后一个元素。该操作的输入为队列。执行此操作之前，队列必须存在且为空。
- `addQueue`: 在队列尾部添加新元素。该操作的输入为队列和新元素。执行此操作之前，队列必须存在且未满。
- `deleteQueue`: 从队列中删除前端元素。该操作的输入为队列。执行此操作之前，队列必须存在且为空。

队列 | 1167

以下抽象类 `queueADT` 定义了这些操作作为一种抽象数据类型（ADT）。

```cpp
template <class Type>
class queueADT {
public:
    virtual bool isEmptyQueue() const = 0;
    // 用于判断队列是否为空的函数。
    // 后置条件：如果队列为空则返回 true，
    // 否则返回 false。

    virtual bool isFullQueue() const = 0;
    // 用于判断队列是否满队的函数。
    // 后置条件：如果队列满则返回 true，
    // 否则返回 false。

    virtual void initializeQueue() const = 0;
    // 将队列初始化为空状态的函数。
    // 后置条件：队列变为空。
    virtual Type front() const = 0;
    // 返回队列中第一个元素的函数。
    // 前置条件：队列存在且不空。
    // 后置条件：如果队列为空，程序
    // 将终止；否则返回队列的
    // 第一个元素。

    virtual Type back() const = 0;
    // 返回队列最后一个元素的函数。
    // 前置条件：队列存在且不空。
    // 后置条件：如果队列为空，程序
    // 将终止；否则返回队列的
    // 最后一个元素。

    virtual void addQueue(const Type& queueElement) = 0;
    // 将 queueElement 添加到队列的函数。
    // 前置条件：队列存在且未满。
    // 后置条件：队列发生变化且 queueElement
    // 已添加到队列中。

    virtual void deleteQueue() = 0;
    // 移除队列中第一个元素的函数。
    // 前置条件：队列存在且不空。
    // 后置条件：队列发生变化且第一个
    // 元素已从队列中移除。

};
```

我们留了一个练习题让你绘制 `queueADT` 类的 UML 图。

1168 | 第 19 章：栈与队列

# 使用数组实现队列

在给出用于实现队列作为 ADT 的类定义之前，我们需要决定实现队列需要多少成员变量。当然，我们需要一个数组来存储队列元素，需要变量 `queueFront` 和 `queueRear` 来跟踪队列的第一个和最后一个元素，以及一个变量 `maxSize` 来指定队列的最大容量。因此，我们至少需要四个成员变量。

在编写实现队列操作的算法之前，我们需要决定如何使用 `queueFront` 和 `queueRear` 来访问队列元素。`queueFront` 和 `queueRear` 如何指示队列为空或全满？假设 `queueFront` 给出队列第一个元素的索引，而 `queueRear` 给出队列最后一个元素的索引。要向队列中添加元素，我们首先将 `queueRear` 移动到下一个位置，然后将元素添加到 `queueRear` 指向的位置。要从队列中删除元素，我们首先获取 `queueFront` 指向的元素，然后将 `queueFront` 移动到队列的下一个元素。因此，在每次 `deleteQueue` 操作后 `queueFront` 发生变化，在每次 `add` 操作后 `queueRear` 发生变化。

让我们看看在 `deleteQueue` 操作后 `queueFront` 变化以及在 `addQueue` 操作后 `queueRear` 变化会发生什么。假设持有队列元素的数组大小为 100。

初始状态下，队列为空。执行操作后：

```cpp
addQueue (Queue, 'A');
```

数组如图 19-26 所示。

![](img/abc25bb507ebb3eb05460d88ce0e0fde_1208_0.png)

**图 19-26** 第一次 `addQueue` 操作后的队列

再执行两次 `addQueue` 操作后：

```cpp
addQueue (Queue, 'B');
addQueue (Queue, 'C');
```

数组如图 19-27 所示。

| [0] | [1] | [2] | [3] | | [97] | [98] | [99] |

|---|---|---|---|---|---|---|---|

| A | B | C | | ...... | | | |

| | | | queueFront | 0 | | | |

| | | | queueRear | 2 | | | |

图 19-27 连续执行两次 addQueue 操作后的队列

现在考虑 `deleteQueue` 操作：

```cpp
deleteQueue();
```

在执行此操作后，包含队列的数组如图 19-28 所示。

| [0] | [1] | [2] | [3] | | [97] | [98] | [99] |

|---|---|---|---|---|---|---|---|

| A | B | C | | ...... | | | |

| | | | queueFront | | | | |

| | | | queueRear | | | | |

图 19-28 deleteQueue 操作后的队列

这种设计可行吗？假设 A 代表向队列中添加（即 `addQueue`）元素，D 代表从队列中删除（即 `deleteQueue`）元素。考虑以下操作序列：

AAADADADADADADADA...

这一系列操作最终会使索引 `queueRear` 指向最后一个位置，给人一种队列已满的印象。然而，队列只有三个元素，而数组的前部是空的（见图 29）。

| [0] | [1] | [2] | [3] | | [97] | [98] | [99] |

|---|---|---|---|---|---|---|---|

| A | B | C | | ...... | | | |

| | | | queueFront | | | | |

| | | | queueRear | | | | |

图 19-29 操作序列 AAADADAD 后的队列

解决这个问题的一种方案是，当队列溢出到尾（即 `queueRear` 指向最后一个位置）时，我们可以检查 `queueFront` 的值。如果 `queueFront` 的值指示数组头部有空间，那么我们将所有元素移动到第一个位置。这种方案在队列较小时是可行的。

另一种方案是假设数组是环形的——即第一个位置跟随最后一个位置。让我们考虑图 19-30 所示的队列。

![](img/abc25bb507ebb3eb05460d88ce0e0fde_1210_0.png)

| [0] | [1] | [2] | [3] | | [97] | [98] | [99] |

|---|---|---|---|---|---|---|---|

| A | B | C | | ...... | | | |

| | | | queueFront | | | | |

| | | | queueRear | | | | |

| [0] | [1] | [2] | [3] | | [97] | [98] | [99] |

|---|---|---|---|---|---|---|---|

| A | B | C | | ...... | | | |

| | | | queueFront | | | | |

| | | | queueRear | | | | |

图 19-30 使用形数组的队列

在这种设计中，`queueFront` 指的是第一个元素之前的数组位置索引，而不是元素本身的索引。在这种情况下，假设 `queueRear` 仍然指示队列中最后一个元素的索引，当 `queueFront == queueRear` 时队列为空。在该方案中，索引 `queueFront` 指向的槽（即第一个元素之前的槽）被预留。当下一个可用空间是 `queueFront` 指向的预留槽时，队列变满。最后，由于 `queueFront` 指向的数组位置为空，如果数组大小为 100，则队列中可以存储 99 个元素（见图 19-34）。

![](img/abc25bb507ebb3eb05460d88ce0efde_1211_0.png)

图 19-34 带有预留槽存储队列元素的数组
