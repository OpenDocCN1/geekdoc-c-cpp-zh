

一个新链表的头节点，其中包含原始两个链表中的所有节点。这个更长链表中的节点同样按值从小到大排序。请注意，你的函数既不会创建也不会销毁任何节点。当函数调用结束时，两个指针变量参数的值应为 NULL。

### 3. 设计并实现一个类，其对象表示多项式。

多项式

$a_n x^n + a_{n-1} x^{n-1} + \dots + a_0$

将实现为一个链表。每个节点包含一个 int 值表示 x 的幂次，以及一个 int 值表示对应的系数。类的操作应包括加、减、乘以及多项式求值。重载运算符 +、- 和 * 分别用于加、减和乘。

多项式求值实现为一个成员函数，其参数类型为 int。该求值成员函数返回将参数代入 x 并执行相应运算后得到的值。包含四个构造函数：一个默认构造函数、一个拷贝构造函数、一个带单个 int 类型参数的构造函数（生成仅包含一个常数项且等于构造参数的多项式），以及一个带两个 int 类型参数的构造函数（生成单项式多项式，其系数和指数由这两个参数给出）。（在上面的记号中，单参数构造函数生成的多项式是仅由 $a_0$ 组成的简单形式。双参数构造函数生成的多项式是稍微复杂一点的形式 $a_n x^n$。）包含一个合适的析构函数。包含输入和输出多项式的成员函数。

当用户输入一个多项式时，用户输入以下形式：

$a_n x^n + a_{n-1} x^{n-1} + \dots + a_0$

但是，如果某项的系数 $a_i$ 为零，用户可以省略该项 $a_i x^i$。例如，多项式

$3x^4 + 7x^2 + 5$

可以输入为

3x^4 + 7x^2 + 5

也可以输入为

3x^4 + 0x^3 + 7x^2 + 0x^1 + 5

以及可能还有一个额外的指针。

对于链表节点，你需要以下结构体（位于列表类外部）：

```
struct node
{
    double item;
    node *next;
};
```

增量开发对于任何规模的项目都至关重要，本项目也不例外。先编写 List 类的定义，但暂不实现任何成员。将此类的定义放在文件 list.h 中。然后在一个包含 int main(){} 的文件中 #include "list.h"。编译你的文件。这样可以发现语法错误和许多拼写错误，如果你在未进行此检查的情况下尝试实现成员，这些错误会造成极大的麻烦。然后，你应该一次实现并编译一个成员，直到在 main 函数中有足够的代码来编写测试代码。

### 6. 在一个古老的国度里，美丽的公主伊芙有许多追求者。

她决定采用以下程序来确定她将嫁给哪位追求者。首先，所有追求者将排成一队，并分配编号。第一位追求者编号为 1，第二位为 2，依此类推，直到最后一位追求者编号为 n。她从第一位追求者开始，沿着队伍数三位追求者（因为她名字中有三个字母），第三位追求者将被淘汰，不能赢得她的芳心，并从队伍中移除。然后伊芙继续，再数三位追求者，并淘汰每第三位追求者。当她数到队尾时，她会从头继续数。

例如，如果有六位追求者，那么淘汰过程如下进行：

- 123456      初始追求者列表，从 1 开始计数
- 12456       追求者 3 被淘汰，从 4 开始继续计数
- 1245        追求者 6 被淘汰，从 1 开始继续计数
- 125         追求者 4 被淘汰，从 5 开始继续计数
- 15          追求者 2 被淘汰，从 5 开始继续计数
- 1           追求者 5 被淘汰，1 是幸运的获胜者

编写一个程序，创建一个循环链表节点，以确定如果有 n 位追求者时，你应该站在哪个位置才能娶到公主。循环链表是一种链表，其中列表中最后一个节点的链接字段指向列表的头节点。你的程序应通过删除与淘汰过程中每一步被淘汰的追求者相对应的节点来模拟该过程。考虑你可能需要删除列表中“头”节点的情况。

![](img/88b1f375f11336dbd9dac8b1675d0698_819_0.png)

### 7. 重做（或首次完成）第 9 章的编程项目 5。

但是，不要使用动态数组来存储每个计算机站点的用户 ID 列表，而是使用链表。这些列表的节点应包含站点编号以及登录该站点的用户的用户 ID。如果没有人登录某个计算机站点，则该计算机站点在链表中不应存在任何条目。

### 8. 修改或重写 Queue 类（显示 13.21 至 13.23），以模拟车辆管理局（DMV）柜台的客户到达情况。

当客户到达时，他们会被分配一个票号，从 1 开始，每来一位新客户就递增。当客服人员空闲时，下一个票号的客户被叫到。这种系统形成了一个按票号排序的 FIFO 客户队列。编写一个程序，实现该队列并模拟客户进入和离开队列。进入队列的输入应该是票号以及该票号进入队列时的时间戳。当一个客服人员处理下一个客户时，票及其对应的时间戳被移除。你的程序应保存最后三位客户在队列中等待的时长。每次从队列中移除一个票号时，更新这些时间，并输出最后三位客户的平均值，作为下一位客户被处理所需时间的估计。如果队列中没有人，输出该队列为空。

下面给出了基于计算机时钟计算时间戳的代码。在大多数 C++ 实现中，time(NULL) 函数返回自 1970 年 1 月 1 日以来的秒数：

```
#include <ctime>
...
int main()
{
    long seconds;
    seconds = static_cast<long>(time(NULL));
    cout << "Seconds since 1/1/1970: " << seconds << endl;
    return 0;
}
```

示例执行如下所示：

```
The line is empty.
Enter '1' to simulate a customer's arrival, '2' to help the next customer, or '3' to quit.
1
Customer 1 entered the queue at time 100000044.
Enter '1' to simulate a customer's arrival, '2' to help the next customer, or '3' to quit.
1
Customer 2 entered the queue at time 100000049.
Enter '1' to simulate a customer's arrival, '2' to help the next customer, or '3' to quit.
1
Customer 3 entered the queue at time 100000055.
Enter '1' to simulate a customer's arrival, '2' to help the next customer, or '3' to quit.
2
Customer 1 is being helped at time 100000069. Wait time = 25 seconds.
The estimated wait time for customer 2 is 25 seconds.
Enter '1' to simulate a customer's arrival, '2' to help the next customer, or '3' to quit.
2
Customer 2 is being helped at time 100000076. Wait time = 27 seconds.
The estimated wait time for customer 3 is 26 seconds.
Enter '1' to simulate a customer's arrival, '2' to help the next customer, or '3' to quit.
1
Customer 4 entered the queue at time 100000080.
Enter '1' to simulate a customer's arrival, '2' to help the next customer, or '3' to quit.
2
Customer 3 is being helped at time 100000099. Wait time = 44 seconds.
The estimated wait time for customer 4 is 32 seconds.
```

### 9. 下图被称为图。

圆圈称为节点，线条称为边。一条边连接两个节点。你可以将图解释为一个由房间和通道组成的迷宫。节点可以看作房间，边将一个房间连接到另一个房间。请注意，图中的每个节点最多有四条边。

![](img/88b1f375f11336dbd9dac8b1675d0698_821_0.png)

