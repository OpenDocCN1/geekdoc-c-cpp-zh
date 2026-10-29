

4. (Modify) 修改程序 13.3，使其实例化三个名为 digits1、digits2 和 digits3 的数字栈。将 digits1 初始化为包含数字 9、8、5 和 2，即数字 2589 的逆序。同样，digits2 栈应初始化为包含数字 3、1、5 和 7，即数字 7513 的逆序。计算这两个数的和并将其放入 digits3 栈中。该和应通过从 digits1 和 digits2 中弹出对象并与名为 carry 的变量相加得到，该变量初始化为 0。如果两个弹出对象和 carry 的和不超过 10，则应将该和压入 digits3 栈，并将 carry 设置为 0；否则，carry 应设置为 1，并将和的个位数压入 digits3 栈。

5. (Program) 编写一个 C++ 程序，允许用户在栈对象中输入最多 100 个整数。然后让程序执行以下操作：
a. 将栈的内容反转到第二个整数栈中。
b. 使用另外两个栈，将原始栈中的内容反转。例如，如果原始栈包含整数 1、2、3 和 4，则程序结束时应包含整数 4、3、2 和 1。

6. (Program) 编写一个 C++ 程序，允许用户在栈对象中输入最多 50 个字符。然后让程序对栈内容按递增顺序排序。例如，如果栈的内容最初为 D、E、A 和 B，其最终内容为 A、B、D 和 E。

## 13.4 Queues

队列（读作 "cue"）是一个列表，其中项目被添加到列表的一端，称为顶部，并从列表的另一端移除，称为底部。这种安排确保项目按它们进入列表的精确顺序从列表中移除。这意味着第一个放在列表上的项目是第一个被移除的项目，第二个放在列表上的项目是第二个被移除的项目，以此类推。因此，队列是一个先进先出（FIFO）列表——一个列表，其中第一个添加到列表中的项目是第一个可以被移除的项目。

作为队列的示例，想象一个等待购买职业足球队季票的人的名单。名单上的第一个人应该在第一批票可用时被叫到，第二个应该为第二批可用票被叫到，以此类推。图 13.8 显示了当前在名单上的人名。

![](img/e9bf940282dfb289356f077151cc69dd_617_0.png)

图 13.8 具有其指针的队列

名字以与栈相同的方式添加：随着新名字被添加到列表中，它们被堆叠在现有名字之上。队列与栈的区别在于名字如何从列表中弹出。显然，这个名单上的人期望按他们被列入名单的顺序得到服务——即先进先出。因此，与栈不同，最近添加到列表中的名字并不是第一个被移除的名字。相反，列表上仍然存在的最旧的名字总是第一个被移除的名字。

类似于从栈的另一端弹出。如何实现这些操作取决于用于表示队列的列表。由于你使用 deque 类作为基类，你可以通过使用 deque 类的 push_front() 和 pop_back() 方法轻松创建 push 和 pop 操作（参见表 13.4）。

程序 13.4 显示了使用 deque 类在完整程序的上下文中构造队列，其中名字被推到 deque 的前面并从后面弹出。此过程创建了表征队列的 FIFO 排序。

## Program 13.4

```
#include <iostream>
#include <deque>
#include <string>
#include <cctype>
using namespace std;
int main()
{
    string name;
    deque<string> queue;

    cout << "Enter as many names as you want, one per line" << endl;
    cout << " To stop enter a single x" << endl;

    // push names onto the queue
    while(true)
    {
        cout << "Enter a name (or x to stop): ";
        getline(cin, name);
        if (tolower(name.at(0)) == 'x') break;
        queue.push_front(name);
    }

    cout << "\nThe names in the queue are:\n";

    // pop names from the queue
    while(!queue.empty())
    {
        name = queue.back();  // retrieve the name
        queue.pop_back();     // pop a name from the queue
        cout << name << endl;
    }
    return 0;
}
```

程序 13.4 的一个示例运行产生了以下结果：

```
Enter as many names as you want, one per line
  To stop enter a single x
Enter a name (or x to stop): Jane Jones
Enter a name (or x to stop): Bill Smith
Enter a name (or x to stop): Jim Robinson
Enter a name (or x to stop): x

The names in the queue are:
Jane Jones
Bill Smith
Jim Robinson
```

## EXERCISES 13.4

+ 1. **(Review)** 指出队列、栈或两者都不适用于以下各项任务，并说明原因或原因不成立：
+ a. 等待在餐厅就座的顾客名单
+ b. 等待批改的学生试卷组
+ c. 按字母顺序列出姓名和电话号码的地址簿
+ d. 在医生办公室等待检查的病人

+ 2. **(Practice)** 输入并运行程序 13.4。

+ 3. **(Modify)** 修改程序 13.4，使其使用整数队列而不是字符串队列。

+ 4. **(Program)** 编写一个 C++ 程序，允许用户在队列中输入最多 20 个字符。然后让程序对队列内容按递增顺序排序。例如，如果队列的内容最初为 D、E、A 和 B，其最终内容为 A、B、D 和 E。

+ 5. **(Program)** 编写一个队列程序，接受一个对象，该对象由整数 ID 号和双精度时薪组成。

+ 6. **(Modify)** 向程序 13.4 添加一个菜单方法，让用户选择将名字添加到队列中、从队列中删除名字，或在不删除任何对象的情况下列出队列的内容。

+ 7. **(Program)** 一群人已到达公交车站，并按此顺序排队：
  
  1. Chaplin	4. Laurel	7. Oliver	10. Garland
  2. West	5. Smith	8. Hardy	11. Wayne
  3. Taylor	6. Grisby	9. Burton	12. Stewart
  
  从输入文件读取名字到队列中，并显示乘客上车顺序。

### 13.5 Common Programming Errors

与使用 STL 的 list 和 deque 类相关的两个常见编程错误是：

+ 1. 将从不同类实例化的对象插入到同一个列表中
+ 2. 在使用 STL 类方法和算法时尝试使用索引而不是迭代器

当程序员尝试构建自己的列表时，与链表、栈和队列相关的五个最常见的编程错误如下：

+ 1. 在构建非 STL 列表时未检查 new 操作符提供的指针。如果此操作符返回 NULL 值，用户应被通知分配未发生，并且必须相应地更改正常的程序操作。你不能假设对 new 的所有调用都会成功分配请求的内存空间。
+ 2. 在向动态创建的栈和队列添加或删除记录时未正确更新所有相关指针地址。除非在更新所有地址时极其小心，否则这些动态数据结构会迅速损坏。
+ 3. 在空间不再需要时忘记释放先前分配的内存空间。此错误通常仅在大型应用程序程序中成为问题，该程序预期连续运行，并且可以根据用户需求进行多次分配空间请求。
+ 4. 在处理栈时未保留栈顶指针的完整性，在处理队列时未保留入队和出队指针的完整性。由于这些指针定位其数据结构中的起始位置，如果起始地址不正确，整个列表将被丢失。
+ 5. 在向栈或队列插入和删除记录时未正确更新内部记录指针。在这些列表中的内部指针包含错误地址后，几乎不可能定位并重新建立丢失的对象集。

### 13.6 Chapter Summary

+ 1. 一个对象允许在公共变量名下存储数据项。这些对象然后可以一起存储在列表中。
+ 2. 链表是对象的列表，其中每个对象包含一个指针变量，用于定位列表中的下一个对象。每个链表必须有一个指针来定位列表中的第一个对象。最后一个对象的指针变量设置为 NULL 以指示列表的结束。
+ 3. 链表可以通过使用 STL 的 list 类自动构造。
+ 4. 栈是一个列表，由只能从列表顶部添加和移除的对象组成。此对象是 LIFO（后进先出）列表，这意味着最后添加到列表中的对象是第一个被移除的对象。栈可以用 STL 的 deque 类实现。
+ 5. 队列是一个列表，由对象添加到列表顶部并从列表底部移除的对象组成。此对象是 FIFO（先进先出）列表，这意味着对象按它们被添加的顺序移除。队列可以用 STL 的 deque 类实现。

