
```cpp
class Network
{
private:
    vector<Node> node;
public:
    void find_nei(); /* 查找邻居并存储在 Node 成员中 */
    void show_topology() const; /* 显示节点和对应的距离 */
    ... // 添加一个构造函数来创建节点
};
```

```cpp
int main() {
    Network *net;
}
```

答案：在 `network.h` 头文件中放置类的声明。

```cpp
#ifndef NETWORK_H
#define NETWORK_H

#include <vector>
using std::vector;

const int MAX_NODES = 10;

class Node {
private:
    int id;
    int x, y;
    vector<int> nei_id; // 存储邻居的标识符
    vector<double> nei_dist; // 存储邻居的距离
public:
    Node(int id, int x, int y);
    void get_coord(int& x, int& y) const;
    void set_nei(int n_id, double dist);
    void show_nei() const;
};

#endif
```

这是代码文件。

```cpp
#include <iostream>
#include <cmath>
#include <cstdlib>
#include <ctime>
#include "network.h"
```

```cpp
Node::Node(int id, int x, int y) /** 我使用了 this 指针来对应成员变量 */
{
    this->id = id;
    this->x = x;
    this->y = y;
}
```

```cpp
void Node::get_coord(int& x, int& y) const
{
    x = this->x;
    y = this->y;
}
```

```cpp
void Node::set_nei(int n_id, double dist)
{
    nei_id.push_back(n_id);
    nei_dist.push_back(dist);
}
```

```cpp
void Node::show_nei() const
{
    for (int i = 0; i < nei_id.size(); i++)
        std::cout << id << "-" << nei_id[i] << ": " << nei_dist[i] << '\n';
}
```

```cpp
Network::Network()
{
    srand(time(NULL));
    for (int i = 0; i < MAX_NODES; i++)
        node.push_back(Node(i, rand() % 1000, rand() % 1000));
}
```

```cpp
void Network::find_nei()
{
    int i, j, x1, x2, y1, y2;
    double dist;

    for (i = 0; i < MAX_NODES; i++) {
        node[i].get_coord(x1, y1);
        for (j = i+1; j < MAX_NODES; j++) {
            node[j].get_coord(x2, y2);
            dist = sqrt(pow(x1-x2, 2) + pow(y1-y2, 2)); /* 应用勾股定理计算距离 */
            if(dist < 200) { // 存储邻居
                node[i].set_nei(j, dist);
                node[j].set_nei(i, dist);
            }
        }
    }
}
```

```cpp
void Network::show_topology() const
{
    for(int i = 0; i < MAX_NODES; i++)
        node[i].show_nei();
}
```

```cpp
int main() {
    Network *net;

    net = new Network();
    net->find_nei();
    net->show_topology();
    delete net;
    return 0;
}
```

# 554 C++ 语言介绍

## 未完成的练习

**U.17.1** 定义 `Date` 类，私有成员为 `day`、`mon` 和 `year`，分别表示日、月、年。编写一个程序读取 `d/m/y` 格式的日期，将值存储在 `Date` 对象的相应成员中，并调用类的适当函数显示它们。不要定义构造函数。

**U.17.2** 定义 `Warehouse` 类，表示一个仓库。该类应包含两个私有成员向量，第一个存储产品代码，第二个存储数量。该类应包含以下函数：

- `void reg(int c, int q);` 如果代码 `c` 未存储，则将其加入 `codes` 向量，并将数量 `q` 加入 `quantities` 向量。
- `void order(int c, int q);` 对应于产品代码 `c` 的订单。该函数应检查代码是否有效以及是否有可用数量，如果是则减去 `q`，否则应显示相关消息。
- `void show(int c);` 检查代码 `c` 是否有效，如果有效则显示相应的数量，否则显示相关消息。
- 默认构造函数。

编写一个程序** 定义 `Book` 类，私有成员为书名、代码和价格。它还应该包含以下公共函数：

- `void review(float grd);` 为书籍评分 `grd`。`review()` 可以对同一本书进行多次调用。最终分数是评分的平均值。
- 一个构造函数，接受参数作为书籍的数据并赋值给相应的成员。

为类添加你认为需要的任何其他函数或成员。

编写一个程序声明五个对象的数组并初始化它们。为了测试类的操作，调用对象的 `review()`。然后，程序读取书籍的代码，如果书籍存在，则显示其分数和价格。如果书籍不存在或未评分，程序应显示相关消息。

**U.17.4** 完成下列类的公共部分，并编写一个类似 C.17.7 的程序，区别在于用户将输入员工数量并动态分配内存创建 `Employee` 对象（即不使用 vector）。假设员工数量小于 100。

```cpp
class Employee
{
private:
    char *name; /* 每个对象的 name 成员应按需要分配内存 */
    float sal;
};
int main()
{
    Employee *empl; /* 此指针应根据用户输入的员工数量分配内存 */
};
```

**U.17.5** 定义 `Fraction` 类，私有成员为分数的分子和分母。添加公共函数 `add()`、`sub()`、`mul()` 和 `div()` 以允许两个分数的加、减、乘、除，以及你认为用于类的任何其他函数。运算结果应以分数的形式显示。参见以下代码示例：

```cpp
int main() {
    Fraction a(4, 9), b(2, 9), c;
    c = a.add(b);
    c.show(); /* 在每次运算中，程序应简化结果，如果可以简化的话。例如，程序应显示 2/3 而 6/9。提示：你需要找到最大公约数来进行此类简化。 */
};
```

**U.17.6** 定义 `Movie` 类，私有成员为电影标题（例如 `title`），公共成员为类型为 `Info` 的成员（包含电影信息）、一个存储演员名称的向量对象（例如 `v_act`）以及一个存储 `Review` 元素的向量对象（例如 `v_rev`）。定义 `Info` 类，私有成员为电影年份、导演名称、评审员名称以及评审员评分。程序应显示一个菜单以提供以下选择：

- 1. 添加电影。对于每部新电影，程序应该创建一个 `Movie` 对象。程序应该读取并将存储在 `title` 成员中的电影标题、存储在 `v_act` 中的演员名称以及存储在 `Info` 成员中的电影信息。每个 `Movie` 对象应该存储在此类元素的向量中。
- 2. 添加评价。程序应该读取要评价的电影名称，然后读取评价信息，并将其保存到相应 `Movie` 对象的 `v_rev` 成员中。
- 3. 搜索演员。程序应该读取演员名称，并检查该（s）演员是否参与过电影。对于每一部参与的电影，程序应该显示其标题、医疗信息（例如，存储在 `Info` 字段中）以及评价信息（例如，存储在 `v_rev` 的 `Review` 数据中），如果有的话。
- 4. 程序终止。

每个类允许包含的函数仅限于构造函数和一个用于显示其成员变量值的函数（例如 `show()`）。

# 运算符重载 18

在第 16 章中，我们学习了只要函数的签名（signature）不同，我们就可以定义多个同名的函数。C++ 的主要目标之一是让程序员定义的类型表现得像基本类型。在本章中，我们将看到 C++ 如何实现这一目标，也就是说，我们将看到如何将函数重载的概念扩展到运算符上，以便用户定义的类型（如类）能够表现得像基本类型。

# 运算符重载

就像函数可以被重载一样，运算符也可以被重载并执行不同的任务。事实上，你已经遇到过运算符重载的示例。例如，当 `*` 运算符应用于数字时，产生它们的乘积；当应用于指针时，它产生所存储的值。编译器通过检查参数的名称和类型来确定如何使用该运算符。

C++ 允许我们将运算符的概念扩展到用户定义的类型。例如，我们可以重载 `+` 运算符来将两个我们自定义类的对象相加。事实上，我们在第 10 章中看到，可以使用 `+` 运算符来加两个字符串对象，或者使用 `<` 和 `==` 运算符进行比较。事实上，`string` 类重载了这些以及许多运算符。这种执行操作的自然方式揭示了运算符重载的美感。如果应用起来，它可以简化编程任务，并生成易读、易编写的代码。要重载运算符，使用 `operator` 关键字进行声明，如下所示：

```
return_type operatorop (parameters)
```

函数的名称是 `operatorop`。`op` 也可以接受任何 C++ 运算符（例如 `+`、`-`、`*` 等），但有些例外。像任何普通函数一样，它有函数体、返回类型并可以接受参数。参数的数量与运算符参数的数量相同。也就是说，二进制运算符的重载函数接受两个参数，而一元运算符的接受一个。正如我们所说，运算符重载通常应用于以更自然方式操作的类。例如，以下程序定义了 `Rect` 类，该类包含一个重载 `+` 运算符的函数：

```cpp
#include <iostream> // 示例 1

class Rect
{
private:
    float length;
    float height;
public:
    Rect(float l = 0, float h = 0); // 带有默认值的构造函数
    operator+(const Rect& r) const;
    float area() const;
    void show() const;
};
```

```cpp
Rect::Rect(float l, float h)
{
    length = l;
    height = h;
}
```

```cpp
Rect::operator+(const Rect& r) const
{
    Rect tmp;
    tmp.length = length + r.length;
    tmp.height = height + r.height;
    return tmp;
}
```

```cpp
float Rect::area() const
{
    return length;
}
```

```cpp
void Rect::show() const
{
    std::cout << "L:" << length << " H:" << height << '\n';
}
```

```cpp
int main()
{
    Rect r1(10, 20), r2(30, 40), r3;
    r3 = r1+r2; // 等同于 r3 = r1.operator+(r2)
    r3.show();
    return 0;
}
```

在讨论运算符重载之前，让我们先回答这个问题。由于 `length` 和 `height` 成员是私有的，当在 `operator+` 函数中访问这些成员时（例如 `r1.length?`），编译不会失败。答案是，当编译器遇到 `r1+r2` 语句时，它会检查操作数的类型并意识到必须调用 `operator+` 函数。具体来说，`r1+r2` 语句被实现为 `r1.operator+(r2)`，因此调用了 `r1` 对象的 `operator+` 函数并传入参数 `r2`。通常，当在类中声明二进制运算符的重载时，左侧（例如 `r1`）是调用它的对象，而右操作数（例如 `r2`）则作为参数传递给函数。注意，如果没有声明运算符函数，编译器将为非法操作显示错误信息，因为对象不能相加。或者，也可以显式地调用该函数并写下 `r1.operator+(r2)`。自然地，运算符的使用比显式调用更易读、易写。该函数返回一个维度与两个对象对应维度的新对象。

此程序证明了与类相关的 C++ 运算符在应用于类的对象时可以具有特殊行为。例如，对象可以像基本类型一样参与普通表达式（例如 `r1+r2`）。传统方法是以通常的方式定义相应的函数。例如，与其重载 `+` 运算符，不如我们定义 `add()` 函数：

```cpp
Rect add(const Rect& r1, const Rect& r2)
{
    Rect tmp;
    tmp.length = r1.length + r2.length;
    tmp.height = r1.height + r2.height;
    return tmp;
}
```

```cpp
int main()
{
    r3 = add(r1, r2);
}
```

运算符重载的用处是让类以更自然的方式操作。这种方法简化了编程任务，并生成易读、易写的代码。运算符重载的优势是让类操作看起来更自然（例如 `r1+r2`），这对于开发者来说更优雅。

## 562 C++ 简介

注意，在重载函数中，至少有一个操作数的类型必须是用户定义的类型，例如类。你不能定义所有操作数都是基本类型的重载函数。例如，你不能定义一个带有两个 `char*` 或 `int` 参数的 `==` 运算符重载函数。

在上一个程序中，重载的 `>` 运算符接收一个参数 `Rect (e, r)`，如果调用函数的面积大于 `r` 则返回 `true`，否则返回 `false`。使用 `area()` 函数计算面积。修改 `main()` 来测试函数的操作。

```cpp
bool Rect::operator>(const Rect& r) /* 在类中添加了声明。 */
{
    if(area() > r.area())
        return true;
    else
        return false;
}
```

```cpp
int main()
{
    Rect r1(10, 20), r2(30, 40);

    if(r1 > r2)
        std::cout << "Bigger\n";
    else
        std::cout << "Not bigger\n";
    return 0;
}
```

表达式 `r1 > r2` 被翻译为 `r1.operator>(r2)`，因此调用了 `r1` 的 `operator>` 函数并传入 `r2` 作为参数。也就是说，尽管这看起来很奇怪，表达式 `r1+r2` 或 `r1 > r2` 并没有执行数学运算，而是调用运算符函数。由于函数返回 `false`，程序显示 `Not bigger`。

## 包含指针的类

现在让我们来看包含指针对象的拷贝情况。请密切注意，以下程序有什么问题？

```cpp
#include <iostream> // 示例 18.2
#include <cstring>
```

```cpp
class T{
  private:
    char *s;
public:
    T(const char str[]);
    ~T();
    void show() const {std::cout << s << '\n' }
};
```

## 18 • 运算符重载 563

```cpp
T::T(const char str[])
{
    s = new char[strlen(str)+1];
    strcpy(s, str);
}
```

```cpp
T::~T()
{
    delete[] s;
}
```

```cpp
int main()
{
    T t1("Peter"), t2("Mike");
    t2 = t1;
    t2.show();
    return 0;
}
```

语句 `t2 = t1;` 导致程序运行过程中出现问题。让我们看看为什么。拷贝操作使得 `t2.s` 指针指向与 `t1.s` 相同的内存。为 `t2.s` 留的内存没有被释放。当程序结束时，会调用 `t2` 的析构函数，它释放了 `t2.s` 指向的内存。由于 `t2.s` 和 `t1` 指向同一内存，`t1` 的析构函数会再次尝试释放该内存。众所周知，删除已经释放的内存是未定义的（例如，它可能会导致程序崩溃）。
