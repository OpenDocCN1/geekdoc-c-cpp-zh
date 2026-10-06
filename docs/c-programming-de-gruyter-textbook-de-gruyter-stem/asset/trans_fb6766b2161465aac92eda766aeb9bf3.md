

# 10.2 STL 中的容器

```cpp
A.resize(primecount + 10);
if (i % 2 == 0)
    //大于 2 的偶数不是
    //质数。
    continue;
    //检查 3,5,7,...,i/2 是否是 i 的因子
    int j = 3;
    while (j <= i/2 && i % j != 0)
        j += 2;
    if (j > i/2)
        //如果所有这些数都不是 i 的
            //因子，则 i 是质数
    A[primecount++] = i;
for (i = 0; i < primecount; i++) //打印质数
{
    cout << setw(5) << A[i];
    if ((i+1) % 10 == 0) //每行10个数字
        cout << endl;
}
```

程序的运行如下：

| 输入一个大于等于2 的值作为质数的上限：100 |
| :--- |
| 2 3 5 7 11 13 17 19 23 29 |
| 31 37 41 43 47 53 59 61 67 71 |
| 73 79 83 89 97 |

# 3. 双端队列 (Double Queues)

双端队列是队列数据结构的扩展。可以在双端队列的两端添加或删除元素。可以使用可以使用下标“[]”直接访问元素。

## a) 构造函数与析构函数

双端队列有四个构造函数：

```cpp
deque(); //创建一个空的 deque
deque(size_type n, const T &v = T(0));
//创建一个包含 n 个 v 拷贝的 deque
deque(const deque &x); //拷贝构造函数
deque(const_iterator first, const_iterator last);
//创建一个包含某个范围拷贝的 deque
```

## b) 使用双端队列

### 1. 查询双端队列的状态

`size()` 方法返回双端队列中的元素数量。`max_size()` 方法返回双端队列能容纳的最大元素数量。`empty()` 方法测试双端队列是否为空。

### 2. 向双端队列添加元素

向双端队列添加元素与向 vector 添加元素非常相似。程序员可以通过构造函数、`push_back()`/`insert()`/`swap()` 方法、下标运算符以及赋值运算符添加元素。此外，双端队列提供了额外的 `push_front()` 用于在双端队列的头部添加元素：

```cpp
void push_front(const T& x); //在头部
//插入一个新元素
```

### 3. 在双端队列中移除元素

`pop_back()`/`pop_front()`/`erase()`/`clear()` 方法可以移除双端队列中的元素。它们的语义与 vector 的。此外，双端队列提供了额外的 `pop_front()` 用于移除双端队列的第一个元素：

```cpp
void pop_front(); //移除第一个元素
```

### 4. 访问元素

访问双端队列元素有很多方法。程序员可以使用 `pop_front()`/`pop_back()`/`front()`/`back()` 等方法访问队列中的元素。也可以使用迭代器遍历队列，并通过下标运算符直接访问元素。

## c) 应用

# 示例 10.2：使用双端队列存储双精度浮点数。

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

# 4. 列表 (Lists)
list 是一种用于快速添加/删除元素的顺序容器。它支持拆接（splice），可以将一个列表中的所有元素移动到另一个。list 不随机访问，因此某些算法无法在列表上运行。list 是双向链表实现的，可以双向遍历。

### a) 构造函数与析构函数
list 有四个构造函数：

```cpp
list(); //创建一个空列表
list(size_type n, const T& v = T()); //创建一个包含 n 个 v 拷贝的列表
list(const list& l); //拷贝构造函数
list(const_iterator first, const_iterator last); //创建一个包含范围拷贝的列表
```

### b) 使用列表
### 1. 访问列表
list 的接口与 vector 有细微差异。由于 list 不支持 `capacity()`/下标运算符和 `at()` 方法，其他接口是相同的。

### 2. 添加元素
list 的 `insert()` 方法语义与 vector 和队列相同，但 list 中的 `insert()` 方法不会影响迭代器。`splice()` 方法也可以将元素添加到列表：

```cpp
void splice(iterator it, list& x);
//注意：it 必须是有效的迭代器，且
void splice(iterator it, list& x, iterator first, iterator last);
//将 [first, last) 中的元素移动到 it 之前。
//如果 it 是 first 或 it == last，此方法不会包含由 it 指向的元素
```

### 3. 移除元素
`erase()` 方法移除列表中等于 x 的元素。`remove()` 的原型如下：

```cpp
void remove(const T& x);
//移除所有等于 x 的元素
```

## c) 应用
# 示例 10.3：使用 list 重写示例 9.7。
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

# 10.2.2 容器适配器 (Adapters of Containers)
容器适配器并不实现存储数据的机制以及迭代器等功能。它们只是基于 STL 提供的容器实现了不同的接口。

## 1. 栈 (Stacks)
栈是一种访问受限的线性集合。元素只能从栈的一端添加或删除。这些操作分别称为 push 和 pop。在理论上，栈的元素数量没有限制。在实践中，如果栈超过计算机内存限制，它将溢出；如果尝试弹出空栈，它将下溢。STL 捕获这些异常以防止程序崩溃。

栈是基于特定容器实现的，该容器在声明处指定。以下是使用 deque 作为底层存储实现的栈声明示例：

```cpp
stack<int, deque<int>> myStack;
```

栈只实现了栈数据结构的原始操作。`push()`/`pop()` 在栈顶部添加或移除元素；`pop()` 返回栈顶部元素的引用。`empty()` 方法检查栈是否为空。`size()` 方法返回栈中的元素数量。底层存储可以是 vector、list 或 deque，其中 deque 是默认实现。请参考相关文档（如 MSDN）。以下是栈的简单示例。

# 示例 10_4.cpp：初始化一个持有整数的栈。

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

