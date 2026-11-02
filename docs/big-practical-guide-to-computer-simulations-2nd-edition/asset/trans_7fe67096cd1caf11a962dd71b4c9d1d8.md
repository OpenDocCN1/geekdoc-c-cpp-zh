
让我们从使用 STL 的一个简单的字符串优先队列开始。请注意，STL 也包含一个用于字符串的 string 类。要在程序中使用 string 类和优先队列的模板类，你必须编写以下代码：

```
#include <queue>
#include <string>
```

下面这段简单的程序片段展示了如何定义和使用字符串优先队列：

```
priority_queue<string> q2;
q2.push("hello"); // fill priority queue
q2.push("you");
q2.push("are");
q2.push("welcome");

while(!q2.empty()) // get events from queue
{
string s;
s = q2.top(); // get "smallest" string
q2.pop(); // remove it
cout << s << endl;
}
```

| 获取源代码 |
|---|
| 目录：libraries |
| 文件：pqueue0.cpp |

在第 1 行，定义了一个优先队列 q2，并自动初始化为空队列。在类名 priority_queue 后面，模板参数写在尖括号 < > 中，这里是指队列元素类型 string。这样，对所有模板都指定了类型和进一步的参数（见下文）。第 2 行声明了一个辅助字符串变量。使用成员函数 push() 将一些字符串放入队列，该函数接收要放入队列的对象作为参数（从技术上讲，它接收对象的引用）。在第 8–13 行，优先队列被读出。这里使用了另外三个成员函数：empty() 测试队列是否为空；top() 返回对队列中当前第一个元素的引用；使用 pop() 可以移除当前第一个元素。为了完整起见，我们注意到成员函数 size() 返回当前存储在队列中的元素数量。

运行该程序时，输出为：

```
you
welcome
hello
are
```

因此，队列按字典序递减的顺序返回这些字符串。对于简单的预定义数据类型，可以为队列指定其他排序准则作为模板参数。我们这里只考虑最一般的情况：排序准则完全由自己定义，对于更复杂对象的优先队列，通常就是这种情况。

假设你想为事件创建一个优先队列。每个事件描述气体模拟中两个原子的碰撞。在事件驱动模拟中（见第 6.7.1 节），事件将按照事件时间递增的顺序一个接一个地处理。因此，每个事件可以用两个参与原子的 ID 和碰撞发生的时间来描述。这里使用以下数据结构：

| 获取源代码 |
|---|
| 目录：libraries |
| 文件：pqueue.cpp |

```
struct event_t
{
    int part1, part2;    // IDs of particles colliding
    double time;         // time of collision
};
```

这里使用了结构体，它是一种默认所有成员都为 public 的类。即使我们为事件定义一个带有数据封装、访问用的成员函数等的类，下面展示的所有内容也同样适用。

对于优先队列，我们必须提供一个用于比较两个事件的函数。为此，不能使用标准的比较运算符，因此我们必须自己提供一个。为了获得最大的灵活性，这个比较函数必须是一个函数对象（也称为仿函数）。它是某个类的对象 obj，该类提供了 operator() 作为成员函数。因此，将该运算符应用于对象，即编写 obj()，就恰好实现了对该函数的调用。与定义普通函数相比，其优势在于函数对象本身也是 C++ 对象。因此，它们可以拥有所有类属性，例如成员数据等。这样，同一个类可以有不同的函数对象，它们的行为不同，因为其内部数据不同。下面的示例为事件提供了比较，应该能清楚地说明如何定义提供函数对象的类：

```
class EventSortCriterion
{
public:
    bool operator() (const event_t &e1, const event_t &e2)
    {
        return(e1.time > e2.time);
    }
};
```

这看起来像一个标准的类定义，这里没有成员数据，其中一个成员函数是 () 运算符。该运算符接收两个参数，并返回一个类型为 bool 的变量，bool 是 C++ 的一种特殊类型。bool 类型可能的取值为 true 和 false，分别等价于 0 和非零值，且与标准 C 兼容。参数前面写有 const，它禁止运算符修改这些值。

接下来展示如何定义和使用事件优先队列：

```
priority_queue<event_t, vector<event_t>, EventSortCriterion> q;
event_t e; // one event
int i; // loop counter
int num_events = 20;

srand48(1000);
for(i=0; i<num_events; i++) // put events into queue
{
    e.part1 = i;
    e.part2 = i+10;
    e.time = 1000*srand48();
    q.push(e);
}

while(!q.empty()) // get events from queue
{
    e = q.top(); // get smallest event
    q.pop(); // remove it
    cout << "(" << e.part1 << "," << e.part2 << ") at t="
         << e.time << endl;
}
```

最重要的一行是第一行。这里定义了优先队列。与上面字符串队列的例子相比，这里给出了两个额外的模板参数。第二个参数是用于实现队列的数据类型。这里使用了一个 vector，它存储 event_t 类型的元素。请注意，这本身也是一个模板，正如从

这里考虑一个基本示例。该模拟由一些分布在 x-y 平面上的“代理”（agent）组成。每个代理都有一个位置，作为键。此外，与每个代理关联的数据由一些“容量”（capacity）和“交互范围”（interaction range）组成，其确切含义在这里并不重要。这通过以下 agent_t 和 agentkey_t 的两个类型定义来实现：

| 获取源代码 |
|---|
| 目录：libraries |
| 文件：maps.cpp |

```
struct agent_t
{
    int capacity;    // how much an agent can process
    int range;       // interaction range
};
```

```
struct agentkey_t
{
    int x,y;         // position of agent
};
```

由于实现基于搜索树，因此必须提供比较准则。这里，我们假设 x 坐标首先决定顺序。如果两个代理的 x 坐标相同，则接着比较 y 坐标。比较通过相应的函数对象类实现，类似于上面展示的优先队列：

```
class AgentkeySortCriterion
{
public:
    bool operator() (const agentkey_t &k1, const agentkey_t &k2) const
    {
        return( (k1.x < k2.x) || ( (k1.x == k2.x) &&(k1.y < k2.y) ) );
    }
};
```

在 main() 函数中，通过以下方式定义一个映射 m1：

```
typedef map<agentkey_t, agent_t, AgentkeySortCriterion> agentmap_t;
agentmap_t m1;                                           // stores all agents
```

第一个模板参数表示键的类型，第二个参数表示要存储的值对象的类型，而第三个参数是排序准则。如果键定义了 operator<（例如整数键），则第三个参数是可选的。

对于插入和删除元素，可以使用成员函数 insert() 和 erase()。插入操作有点不方便。使用数组表示法会更方便，如下例所示：

```cpp
int num_agents = 20; // number of agents
int sizex=10, sizey=10; // size of system
agentkey_t k1; // one key
agent_t a1; // one agent

for(int i=0; i<num_agents; i++) // distrib. agents
{ // random positions
k1.x = static_cast<int>(floor(sizex*drand48()));
k1.y = static_cast<int>(floor(sizey*drand48()));
a1.capacity = 100;
a1.range = 1 + static_cast<int>(floor(3*drand48()));
m1[k1] = a1;
}
```

使用两个变量 k1 和 a1（第 5-6 行）分别存储键和代理。代理的位置和 range 值随机初始化（第 10-11 行）。请注意，这里使用了 static_cast。这是一个 C++ 运算符，它会执行一些由编译器进行的检查，并防止无意义的类型转换。代理实际上在第 14 行使用数组表示法存储。你可以用同样的方式访问映射元素进行读取，但与数组不同，如果你查找一个键值不存在的元素，该元素会被创建为默认值。

因此，在下面的示例中，我们使用 find() 成员函数来测试是否存在具有特定键的元素。该代码遍历映射中的所有元素。为此，需要一个特殊的对象——迭代器，它类似于映射中的内部指针。有一些预定义的迭代器可以通过公有成员函数访问：begin() 和 end()。前者总是返回一个指向映射当前第一个元素的迭代器，后者返回一个指向最后一个元素之后位置的迭代器。
