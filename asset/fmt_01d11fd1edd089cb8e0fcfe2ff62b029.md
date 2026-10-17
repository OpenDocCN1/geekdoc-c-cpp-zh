
### b) 使用双端队列

#### 1. 查询双端队列的状态

`size()` 方法返回双端队列中的元素数量。`max_size()` 方法返回双端队列能容纳的最大元素数量。`empty()` 方法测试双端队列是否为空。

#### 2. 向双端队列添加元素

向双端队列添加元素与向 `vector` 添加元素非常相似。程序员可以通过构造函数、`push_back()`/`insert()`/`swap()` 方法、下标运算符以及赋值运算符添加元素。此外，双端队列提供了额外的 `push_front()` 用于在双端队列的头部添加元素：

```cpp
void push_front(const T& x); //在头部
//插入一个新元素
```

#### 3. 在双端队列中移除元素

`pop_back()`/`pop_front()`/`erase()`/`clear()` 方法可以移除双端队列中的元素。它们的语义与 `vector` 的。此外，双端队列提供了额外的 `pop_front()` 用于移除双端队列的第一个元素：

```cpp
void pop_front(); //移除第一个元素
```

#### 4. 访问元素

访问双端队列元素有很多方法。程序员可以使用 `pop_front()`/`pop_back()`/`front()`/`back()` 等方法访问队列中的元素。也可以使用迭代器遍历队列，并通过下标运算符直接访问元素。

### c) 应用

#### 示例 10.2：使用双端队列存储双精度浮点数。

```cpp
//10_2.cpp
#include <iostream>
#include <deque>                //包含 deque 头文件
#include <algorithm>         //包含 algorithm 头文件
using namespace std;
int main()
{
    deque<double> values;             //定义一个双端队列
    ostream_iterator<double> output(cout, " ");
    values.push_front( 2.2 );         //使用 push_front 在
//头部添加元素
    values.push_front( 3.5 );
    values.push_back( 1.1 );   //使用 push_back 在
//末尾添加元素
    cout << "values contains: ";
    for ( int i = 0; i < values.size(); ++i )
        cout << values[i] << " ";   使用 pop_front 删除第一个
//元素
    values.pop_front();
    cout << "\nAfter pop_front values contains: ";
}
```

结果：
| values contains: 3.5 2.2 1.1 |
| :--- |
| After pop_front values contains: 2.2 1.1 |
| After values[1] = 5.4 values contains: |

### 4. 列表 (Lists)

`list` 是一种用于快速添加/删除元素的顺序容器。它支持拆接（splice），可以将一个列表中的所有元素移动到另一个。`list` 不随机访问，因此某些算法无法在列表上运行。`list` 是双向链表实现的，可以双向遍历。

#### a) 构造函数与析构函数

`list` 有四个构造函数：

```cpp
list(); //创建一个空列表
list(size_type n, const T& v = T()); //创建一个包含 n 个 v 拷贝的列表
list(const list& l); //拷贝构造函数
list(const_iterator first, const_iterator last); //创建一个包含范围拷贝的列表
```

#### b) 使用列表

##### 1. 访问列表

`list` 的接口与 `vector` 有细微差异。由于 `list` 不支持 `capacity()`/下标运算符和 `at()` 方法，其他接口是相同的。

##### 2. 添加元素

`list` 的 `insert()` 方法语义与 `vector` 和队列相同，但 `list` 中的 `insert()` 方法不会影响迭代器。`splice()` 方法也可以将元素添加到列表：

```cpp
void splice(iterator it, list& x);
//注意：it 必须是有效的迭代器，且
void splice(iterator it, list& x, iterator first, iterator last);
//将 [first, last) 中的元素移动到 it 之前。
//如果 it 是 first 或 it == last，此方法不会包含由 it 指向的元素
```

##### 3. 移除元素

`erase()` 方法移除列表中等于 `x` 的元素。`remove()` 的原型如下：

```cpp
void remove(const T& x);
//移除所有等于 x 的元素
```

#### c) 应用

#### 示例 10.3：使用 list 重写示例 9.7。

从键盘读取 10 个整数，创建一个存储这些整数的链表，并按顺序输出数字。然后从键盘读取，删除包含该数字的节点并输出列表中的数据。在退出前清除链表。以下是程序：

```cpp
//10_3.cpp
#include <iostream>
#include <list>
using namespace std;
int main()
{
    list<int> Link;    创建一个存储整数链表的列表
    int i, key, item;
    for (i=0; i < 10; i++) //在开头插入 10 个整数
    {
        cin>>item;
        Link.push_front(item);
    }
    cout << "List: "; //打印链表
    list<int>::iterator p=Link.begin();
    //迭代器 p 用于遍历列表
    while(p!=Link.end()) {
        cout <<*p << " "; //打印每个元素直到结束
        p++; //指向下一个元素
    }
    cout << endl;
    cout << "Please input an integer to delete: "; //输入一个要删除的整数
    cin >> key;
    Link.remove(key);
    cout << "List: "; //打印列表
    p=Link.begin();
    while(p!=Link.end()) //打印每个元素直到结束
    {
        cout <<*p << " "; //p 指向下一个元素
        p++;
    }
    cout << endl;
}
```

结果：
3 6 5 7 2 4 5 9 10
List: 10 9 5 4 2 7 5 6 3
Please input an integer to delete: 5
List: 10 9 4 2 7 6 3

### 10.2.2 容器适配器 (Adapters of Containers)

容器适配器并不实现存储数据的机制以及迭代器等功能。它们只是基于 STL 提供的容器实现了不同的接口。

#### 1. 栈 (Stacks)

栈是一种访问受限的线性集合。元素只能从栈的一端添加或删除。这些操作分别称为 `push` 和 `pop`。在理论上，栈的元素数量没有限制。在实践中，如果栈超过计算机内存限制，它将溢出；如果尝试弹出空栈，它将下溢。STL 捕获这些异常以防止程序崩溃。

栈是基于特定容器实现的，该容器在声明处指定。以下是使用 `deque` 作为底层存储实现的栈声明示例：

```cpp
stack<int, deque<int>> myStack;
```

栈只实现了栈数据结构的原始操作。`push()`/`pop()` 在栈顶部添加或移除元素；`pop()` 返回栈顶部元素的引用。`empty()` 方法检查栈是否为空。`size()` 方法返回栈中的元素数量。底层存储可以是 `vector`、`list` 或 `deque`，其中 `deque` 是默认实现。请参考相关文档（如 MSDN）。以下是栈的简单示例。

#### 示例 10_4.cpp：初始化一个持有整数的栈。

```cpp
//include <iostream>
#include <stack> //包含栈适配器头文件
using namespace std;
template< class T>
void popElements( T &s );
int main(){
    stack< int > dequeStack; //使用 deque 作为默认容器
    for ( int i = 0; i < 10; ++i ) {
        dequeStack.push( i ); //将整数推入 deque 中作为
//栈的顶部
    }
}
```

# 10.2 STL 中的容器 - 417

```cpp
cout << "Popping fromDequeStack: ";
popElements( intDequeStack ); //弹出栈中的元素
cout << endl;
}
```

```cpp
template< class T>
void popElements( T &s ) //定义一个模板函数
{
    while ( s.empty() ) {
        cout << s.top() << ' '; //获取栈的顶端元素并
        //打印
        s.pop(); //使用 pop 移除顶端元素
    }
}
```

结果：

| Popping from intDequeStack: 9 8 7 6 5 4 3 2 1 0 |

#### 2. 队列 (Queues)

队列适配器为先进先出（FIFO）服务提供了接口，即向容器尾部添加元素（入队）和移除容器第一个元素（出队）。队列基于底层存储实现，通常是列表（`list`）或双队列（`deque`）。默认的底层存储实现是 `deque`。这是一个使用 `deque` 作为底层存储实现的队列声明示例：

```cpp
queue<int, deque<int>> myQueue;
```

`push()` 方法将元素添加到队列的尾部，`pop()` 方法移除队列的第一个元素，而 `front()` 和 `back()` 方法分别返回队列头部和尾部的引用。`empty()` 方法检查队列为空，`size()` 方法返回队列中的元素数量。详细信息请参考 MSDN 等文档。以下是一个使用队列的简单示例。

#### 示例 10.5：初始化一个整数类型的队列。

```cpp
//10_5.cpp
#include <iostream>
#include <queue> //包含队列适配器头文件
using namespace std;
```

```cpp
template< class T>
void popElements( T &s );
```

# 418 10 通用编程与标准模板库 (STL)

```cpp
int main()
{
    queue<int> intDequeQueue; //使用队列作为默认容器
    for (int i = 0; i < 10; ++i ) {
        intDequeQueue.push( i ); //将整数推入 deque 作为
                                //队列的顶端
    }
    cout << "Popping from intDequeQueue: ";
    popElements(intDequeQueue); //弹出队列的顶端元素
                                //并打印
    cout << endl;
}
```

```cpp
template< class T>
void popElements(T &s ) //定义一个模板函数
{
    while (!s.empty()) {
        cout << s.front() << ' '; //使用 front 获取队列的顶端
                                // 元素并打印
        s.pop(); //使用 pop 移除顶端元素
    }
}
```

结果：

| Popping from intDequeQueue: 0 1 2 3 4 5 6 7 8 9 |

与栈和队列类似，优先级队列（priority queue）是另一种实现高级数据结构的适配器。优先级队列被设计为有序队列，能够从队列中提取出优先级最高的元素。

### 10.3 迭代器 (Iterators)

迭代器是指针的面向对象版本。它们提供了一种统一的机制来遍历容器。指针指向内存位置，程序能够通过指针访问内存位置上的对象。你可以将迭代器看作类型安全的指针——它指向特定类型的对象。

迭代器是桥接算法和容器的常用设计模式。实际算法需要遍历线性集合，通过指针遍历链表或通过数组下标遍历数组。使用适用于线性集合的算法是很好的，这样你就不需要为每种线性集合重复实现多次算法。因此，算法需要一个抽象层来处理“获取下一个元素”或“是否到达末尾？”这类操作。在理论上，指针可以处理这个问题，但会使算法和容器的实现变得更加复杂。对于面向对象的指针，STL 包含了迭代器，以便编写能够适用于所有容器的抽象算法。

#### 10.3.1 迭代器的类型

有五种基本的迭代器：输入迭代器、输出迭代器、前向迭代器、双向迭代器和随机访问迭代器。有两种迭代器适配器：反向迭代器适配器和插入迭代器适配器。

#### 1. 分类

输入迭代器可以从集合中读取数据，输出迭代器可以向集合写入数据。

前向迭代器既是输入迭代器也是输出迭代器，它可以沿着某个方向遍历集合。双向迭代器可以在两个方向遍历集合。随机访问迭代器可以访问集合中的任何位置。

#### 2. 迭代器适配器

迭代器适配器是扩展或调整迭代器功能的适配器。有两种迭代器适配器：

- 反向迭代器适配器反转了递增顺序和递减运算符的功能，使得算法按反序处理元素。所有标准容器都可以配合反向迭代器使用。
- 插入迭代器重载了赋值运算符并转换为插入器，使得算法在其元素上运行时将其插入集合，而不是覆盖元素的值。插入适配器有三种：尾部插入器（back inserters）、头部插入器（front inserters）和通用插入器（general inserters）。尾部插入器在集合末尾添加元素，头部插入器在集合头部添加元素。通用插入器则决定插入位置。

这里有一个迭代器适配器的示例。

#### 示例 10.6：迭代器适配器示例。

```cpp
//10_6.cpp
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;
int main() {
    int A[] = {1, 2, 3, 4, 5};
    const int N = sizeof(A)/sizeof(int);
    vector<int> col1(A,N);
    cout << "List1 contains: ";
    copy(col1.begin(), col1.end(), output);
    vector<int>::iterator pos=col1.begin();
    cout<<"\nThe fist element is: "<<pos;
    vector<int>::reverse_iterator rpos=col1.rbegin();
    cout<<"\nThe last element is: "<<rpos<<endl;
    back_insert_iterator<vector<int>> > iter(col1);
    *iter=66;
    back_inserter(col1)=88;
    copy(col1.begin(), col1.end(), output);
    cout <<endl;
}
```

结果：

| List1 contains: 1 2 3 4 5 |
| The fist element is: 1 |
| The last element is: 5 |
| 1 2 3 4 5 66 88 |

#### 10.3.2 迭代器中的辅助函数

迭代器中有三个辅助函数：`advance()`、`distance()` 和 `iter_swap()`。`advance()` 和 `distance()` 模拟了随机访问迭代器的功能（如移动多个位置和计算距离），通过基础迭代器操作来实现。`iter_swap()` 允许程序员交换两个迭代器指向的值。

- 1. `advance()` 将迭代器位置向前向后移动 `n` 个位置。原型如下：

```cpp
void advance(InputIterator & pos, Dist n);
```

在双向或随机访问迭代器中，`n` 可以为负，以便迭代器后移。

- 2. `distance()` 计算两个迭代器之间的距离：

```cpp
Dist distance(InputIterator pos1, InputIterator pos2);
```
