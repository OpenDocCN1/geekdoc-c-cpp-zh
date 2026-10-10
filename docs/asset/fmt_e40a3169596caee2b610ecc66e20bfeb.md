
所以，在这种情况下，你有一个循环导致迭代器遍历容器中的每一个元素，并你将其打印出来。

当你打印`vector`的内容时，你会发现元素是顺序排列的，正如预期的那样。

从容器中删除数据也有类似的过程。

这种遍历像`vector`容器的方法非常常见，看到一个从容器开始并迭代到结束的语句并不稀奇。而且因为迭代器通常只为此定义，当你对容器元素进行循环时，将声明语句直接放在循环体内部是常见做法。

迭代器对于指定在容器中插入或删除数据的例程至关重要。

对于`vector`和`deque`这样的容器，插入和删除并不高效；另一种容器在处理插入和删除方面好得多：`list`，以及相关的单向链表（`forward list`）。

但`list`不允许你直接访问中间的某个元素。

`list`的优势在于你可以非常容易地向其中插入。如果你向`vector`插入内容，你可能需要复制大量信息，因为你基本上需要将现有元素向后移动一个位置。

但对于`list`，你只需要获取要添加的新项并更新几个指针。同样，合并两个`list`是一项非常快速的任务，而`deque`则需要复制其中一个`list`。

当你使用`*list*`时，这是一个双向链表。**`forward list`**（单向链表）会给你一个单向链表，并且插入操作发生在迭代器所指的元素之后。

假设你有一个用于制作花生酱果果三明治的`list`。在程序`22_8`中，你包含了`<list>`。`list`是模板化的，你创建了一个名为**`instructions`**的*`list`*类型。你可以使用**`push_back`**和**`push_front`**向`list`的尾或头部添加元素，就像使用`deque`那样。

```cpp
// Program 22_8
// 插入示例
#include <iostream>
#include<string>
#include<list>
using namespace std;
int main() {
list<string> instructions;
instructions.push_back("Get bread");
instructions.push_back("Put jelly");
instructions.push_back("Put two halves together");
list<string>::iterator insert_spot;
insert_spot = instructions.begin(); // 指向第一个元素
insert_spot++; // 指向第二个元素
instructions.insert(insert_spot, "Put peanut butter");
for (auto iter = instructions.begin(); iter != instructions.end(); ++iter)
    cout << *iter << endl;
}
```

1 这非常适合队列（`queue`），因为它具有先入先出（FIFO）属性。

2 向量的序列非常适合向量（`vector`），它可以让你轻松地访问中间的任何一个点。

3 这非常适合列表（`list`），它允许你轻松地在中间的任何位置添加或删除电影。

点击此处返回练习题。

# // 测验

1 在以下每个情况下，使用哪种容器最合适？

2 编写一个程序来记录找你会面的人的顺序。你应该反复询问姓名，或者如果用户输入"`next`"，你就应该打印下一个应该会面的人的名字。该程序的运行示例如下：

- a 你已经处理了收到的电话消息顺序，并想按照它们接收的顺序来处理它们。

```
John
James
next
下一个会面的人是: John
Joseph
next
下一个会面的人是: James
```

- b 你每个月都会收到一张账单，并想要查看任何月的账单。

- c 你正在计划一次公路旅行，并已经列出了沿途的几个站点，但想要能够在路径中添加一个新站点。

- d 你正在聊天，并跳到了新的话题上。你想记录对话，以便在完成一个话题后，可以回到上一个话题——当那个完成后，再回到再上一个，以此此类推。

3 编写一个函数，接收一个整数向量，然后使用迭代器打印每个元素，每个元素占一行。

点击此处查看答案。

# // 测验答案

1 每个情况可能都不止一种合适的类型，但以下是针对给定任务的最自然的容器：

2 这里是实现此类程序的一种方法：

注意，使用队列（`queue`）来记录姓名。循环无限进行，在循环的每次迭代中，你读取一个字符串。如果是"`next`"，就弹出前面的元素（并移除该元素）。否则，你只需将姓名添加到队列中。

- a 队列（`Queue`）。这是 FIFO 排序的一个示例，这也是队列最适合用途。

```cpp
#include<iostream>
#include<queue>
#include<string>
using namespace std;
int main () {
    queue<string> names;
    string s;
    cout << "输入姓名，或输入 \"next\"获取下一个会面的人" << endl;
    while(true) {
        cin >> s;
        if(s=="next") {
            cout << "下一个会面的人: " << names.front() << endl;
            names.pop();
        } else {
            names.push(s);
        }
    }
}
```

- b 向量（`Vector`）。向量适合在末尾添加新项以及随机访问——直接访问中间的任何项。

3 这里是实现此功能的一种方法：

- c 列表（`List`）。列表按顺序保留项目，但方便从中间添加（或删除）。在实际操作中，向量也可以良好工作，除非话题列表变得非常长。

```cpp
void print_elements(vector<int> v) {
    vector<int>::iterator i;
    for(i=v.begin(); i!=v.end(); i++) {
        cout << *i << endl;
    }
}
```

- d 栈（`Stack`）。这里的想法是对话会继续，如果有新话题，就将其加入栈中。如果话题结束了，就从栈中弹出，并回到上一个话题。

注意，你为向量声明了一个迭代器。然后，你从向量的`begin(i)`循环到`end(i)`，每次递增迭代器。你通过对指针解引用输出向量的元素。不过，还有其他方法可以实现相同的目标。

![](img/bdf1aaea7e08f6cbf15b0a740771ecdc_267_0.png)

# 23 C++ 关联容器与算法

本节课程内容：

- 容器
- 程序 23_1
- 程序 23_2
- 程序 23_3
- 程序 23_4
- 程序 23_5
- 程序 23_6

标准模板库（STL）提供了多种数据结构和算法，你可以用它们在 C++ 中编写强大且高效的代码。你之前见过一组单元容器和容器适配器，你可以用它们单独持有元素。但还有一些容器——被称为关联容器（associative containers），它们将 2 种或更多类型的关联在一起。STL 中还有算法，它们为处理数据提供了一套更强大的标准工具集。

- 模板函数
- 程序 23_8
- 程序 23_11
- 程序 23_12

- 测验
- 测验答案

## 容器

## / 对 (PAIRS) /

关联容器中最简单的是对（`pair`）。很多时候你想要一个非常简单的结构，将 2 个东西组合在一起。例如，你可能在跟踪人员，并希望一个人有一个年龄和一个名字。`pair`提供了一种将 2 个项组合成结构的简单快速的方法。

`pair`接收两个模板类型：第一个项的类型和第二个项的类型。当模板需要 2 种或更多类型时，在括号内用逗号分隔。

声明一个年龄和名字的对

```cpp
// 程序 23_1
// 对 的示例
#include <iostream>
using namespace std;
int main() {
    pair<int, string> p;
    p.first = 45;
    p.second = "John";
    cout << p.second << " years old." << endl;
}
```

所以，在程序 23_2 中，你可以通过编写`pair<int, string>`创建一个仅由整数和字符串对组成的新类型。这允许你声明该类型的变量。

```cpp
// 程序 23_2
// 使用 pair 为类型创建一个新名字
#include<iostream>
#include<string>
using namespace std;
pair<int, string> person;
int main() {
    person = make_pair(45, "John");
    cout << person.second << " years old." << endl;
}
```

你也可以通过组合特定类型创建你自己的类，这样做相比`pair`的一个优势是该类会给你一个指示。虽然这让你有一个更具描述性的名称，但访问成员变量仍然是（类似的）。`pair`提供了一种将 2 个项组合成结构的简单快速方法。

一个元组的对

```cpp
// 程序 23_3
// Tuple 示例
#include <iostream>
#include <string>
#include <tuple>
using namespace std;
int main() {
    tuple<int, string> t(45, "John");
    cout << get<0>(t) << " " << get<1>(t) << " years old." << endl;
}
```

```cpp
// 程序 23_4
// 使用 make_tuple
#include <iostream>
#include <string>
#include <tuple>
using namespace std;
int main() {
    tuple<int, string> t = make_tuple(45, "John");
    cout << get<0>(t) << " " << get<1>(t) << " years old." << endl;
}
```

```cpp
// 程序 23_5
// 使用 get 获取元素
#include <iostream>
#include <string>
#include <tuple>
using namespace std;
int main() {
    tuple<int, string> t(45, "John");
    int age = get<0>(t);
    string name = get<1>(t);
    cout << name << " is " << age << " years old." << endl;
}
```

```cpp
// 程序 23_6
// 修改 tuple
#include <iostream>
#include <string>
#include <tuple>
using namespace std;
int main() {
    tuple<int, string> t(45, "John");
    get<0>(t) = 50;
    get<1>(t) = "Jane";
    cout << get<1>(t) << " " << get<0>(t) << " years old." << endl;
}
```

## 元组 (TUPLES)

元组（`tuple`）是`pair`的扩展，允许你将任意数量的元素组合在一起。`pair`只能包含 2 个元素，而`tuple`可以包含 3 个更多。

```cpp
// 程序 23_7
// Tuple 示例
#include <iostream>
#include <string>
#include <tuple>
using namespace std;
int main() {
    tuple<int, string, double> t(45, "John", 95.5);
    cout << get<0>(t) << " " << get<1>(t) << " " << get<2>(t) << endl;
}
```

`get`函数用于访问元组中的元素。它需要一个编译时常量作为索引参数，索引从 0 开始。

`tie`用于用于将元组中的值解包到变量中。

```cpp
// 程序 23_8
// 使用 tie
#include <iostream>
#include <string>
#include <tuple>
using namespace std;
int main() {
    tuple<int, string, double> t(45, "John", 95.5);
    int age;
    string name;
    double score;
    tie(age, name, score) = t;
    cout << name << " " << age << " " << score << endl;
}
```

`make_tuple`可以推导出元组的类型。

```cpp
// 程序 23_9
// 使用 make_tuple
#include <iostream>
#include <string>
#include <tuple>
using namespace std;
int main() {
    auto t = make_tuple(45, "John", 95.5);
    t = make_tuple(45, "John", 95.5);
    cout << get<0>(t) << " " << get<1>(t) << " " << get<2>(t) << endl;
}
```

元组是不可变的，除非你重新赋值。

```cpp
// 程序 23_10
// 元组不可变
#include <iostream>
#include <string>
#include <tuple>
using namespace std;
int main() {
    tuple<int, string, double> t(45, "John", 95.5);
    // get<0>(t) = 50; // 错误
    t = make_tuple(50, "Jane", 98.0);
    cout << get<0>(t) << " " << get<1>(t) << " " << get<2>(t) << endl;
}
```

结构化绑定（structured bindings）是 C++17 引入的，可以解包元组。

```cpp
// 程序 23_11
// 结构化绑定
#include <iostream>
#include <string>
#include <tuple>
using namespace std;
int main() {
    tuple<int, string, double> t(45, "John", 95.5);
    auto& [age, name, score] = t;
    cout << age << " " << name << " " << score << endl;
}
```

```cpp
// 程序 23_12
// 结构化绑定修改
#include <iostream>
#include <string>
#include <tuple>
using namespace std;
int main() {
    tuple<int, string, double> t(45, "John", 95.5);
    auto& [age, name, score] = t;
    age = 50;
    name = "Jane";
    score = 98.0;
    cout << get<0>(t) << " " << get<1>(t) << " " << get<2>(t) << endl;
}
```

- 测验
- 测验答案

成对（Pairs）在使用优先级队列（priority queues）时非常常见，因为你通常需要 2 个信息：一个用于确定优先级的值以及与该值关联的实际对象。

假设你想有一个优先级队列，按照年龄从大到小的顺序将人们放入其中。这时你可以关联一个对，第一个元素是年龄，第二个元素是人。最大的年龄将始终排在第一。

在编写代码时，你可以使用以下操作：
- `push`向优先级队列添加元素。
- `pop`移除顶端元素。
- `size`获取优先级队列的大小。
- `empty`返回优先级队列是否为空。

考虑程序 23_5。优先级队列包含在`<queue>`库中，因此你包含`<queue>`来创建一个包含整数和字符串的`pair`类型。整数将是年龄，字符串将是名字。

当你声明一个`pair`的`priority_queue`时，对的第一个元素是年龄，我们最高优先级的元素将是最大的年龄。优先级队列命名为`pq`。

```
// 程序 23_5
// 优先级队列示例
#include <iostream>
#include <string>
#include <queue>
using namespace std;
int main() {
    priority_queue<pair<int, string>> pq;
    pq.push(make_pair(16, "Jack"));
