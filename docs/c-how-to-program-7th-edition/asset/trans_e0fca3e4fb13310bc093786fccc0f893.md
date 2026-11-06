

![](img/023f159fdd47d944d48e08843cea732d_991_0.png)

> **性能提示 22.19**
>
> *队列的每种常用操作都实现为内联函数，该函数调用底层容器的相应函数。这避免了第二次函数调用的开销。*

图 22.24 演示了队列适配器类。使用队列必须包含头文件 `<queue>`。

```cpp
1  // Fig. 22.24: Fig22_24.cpp
2  // Standard Library adapter queue test program.
3  #include <iostream>
4  #include <queue> // queue adapter definition
5  using namespace std;
6
7  int main()
8  {
9      queue< double > values; // queue with doubles
10
11     // push elements onto queue values
12     values.push( 3.2 );
13     values.push( 9.8 );
14     values.push( 5.4 );
15
16     cout << "Popping from values: ";
17
18     // pop elements from queue
19     while ( !values.empty() )
20     {
21         cout << values.front() << ' '; // view front element
22         values.pop(); // remove element
23     } // end while
24
25     cout << endl;
26 } // end main
```

Popping from values: 3.2 9.8 5.4

**图 22.24** | 标准库队列适配器类模板。

第 9 行实例化一个存储 double 值的队列。第 12—14 行使用函数 push 向队列添加元素。第 19—23 行的 while 语句使用函数 empty（所有容器均可用）判断队列是否为空（第 19 行）。当队列中还有更多元素时，第 21 行使用队列函数 front 读取（但不删除）队列中的第一个元素以进行输出。第 22 行使用函数 pop（所有适配器类均可用）删除队列中的第一个元素。

### 22.4.3 `priority_queue` 适配器

类 `priority_queue` 提供的功能支持按排序顺序插入底层数据结构，并从底层数据结构的前端删除。`priority_queue` 可以用 STL 序列容器 vector 或 deque 实现。默认情况下，priority_queue 使用 vector 作为底层容器实现。当元素添加到 priority_queue 时，它们按优先级顺序插入，因此最高优先级的元素（即最大值）将是第一个从 priority_queue 中删除的元素。这通常通过将元素排列成一种称为堆的二叉树结构来实现，该结构始终将最大值（即最高优先级元素）保持在数据结构的前端。我们将在 22.5.12 节讨论 STL 的堆算法。默认情况下，元素比较使用比较器函数对象 less<T> 执行，但您可以提供不同的比较器。

priority_queue 有几种常用操作。push 根据 priority_queue 的优先级顺序将元素插入适当位置（实现方式是调用底层容器的函数 push_back，然后使用堆排序重新排列元素）。pop 删除 priority_queue 中最高优先级的元素（实现方式是先移除堆顶元素，然后调用底层容器的函数 pop_back）。top 获取 priority_queue 顶部元素的引用（实现方式是调用底层容器的函数 front）。empty 判断 priority_queue 是否为空（实现方式是调用底层容器的函数 empty）。size 获取 priority_queue 中元素的数量（实现方式是调用底层容器的函数 size）。

> **性能提示 22.20**
>
> *priority_queue 的每种常用操作都实现为内联函数，该函数调用底层容器的相应函数。这避免了第二次函数调用的开销。*

![](img/023f159fdd47d944d48e08843cea732d_992_0.png)

> **性能提示 22.21**
>
> *为获得最佳性能，请使用类 vector 作为 priority_queue 的底层容器。*

![](img/023f159fdd47d944d48e08843cea732d_992_1.png)

图 22.25 演示了 priority_queue 适配器类。要使用类 priority_queue，必须包含头文件 `<queue>`。

```cpp
// Fig. 22.25: Fig22_25.cpp
// Standard Library adapter priority_queue test program.
#include <iostream>
#include <queue> // priority_queue adapter definition
using namespace std;

int main()
{
   priority_queue< double > priorities; // create priority_queue

   // push elements onto priorities
   priorities.push( 3.2 );
   priorities.push( 9.8 );
   priorities.push( 5.4 );

   cout << "Popping from priorities: ";

   // pop element from priority_queue
   while ( !priorities.empty() )
   {
       cout << priorities.top() << ' '; // view top element
       priorities.pop(); // remove top element
   } // end while

   cout << endl;
} // end main
```

Popping from priorities: 9.8 5.4 3.2

**图 22.25** | 标准库 `priority_queue` 适配器类。

第 9 行实例化一个存储 double 值并使用 vector 作为底层数据结构的 priority_queue。第 12—14 行使用函数 push 向 priority_queue 添加元素。第 19—23 行的 while 语句使用函数 empty（所有容器均可用）判断 priority_queue 是否为空（第 19 行）。当还有更多元素时，第 21 行使用 priority_queue 函数 top 获取 priority_queue 中最高优先级的元素以进行输出。第 22 行使用函数 pop（所有适配器类均可用）删除 priority_queue 中最高优先级的元素。

## 22.5 算法

在 STL 出现之前，各供应商的容器类库和算法类库基本上互不兼容。早期的容器库通常使用继承和多态，并伴随虚函数调用的相关开销。早期的库将算法作为类行为构建到容器类中。STL 将算法与容器分离。这使得添加新算法容易得多。使用 STL 时，容器元素通过迭代器访问。接下来的几个小节将演示许多 STL 算法。

> **性能提示 22.22**
>
> *STL 为实现效率而设计。它避免了虚函数调用的开销。*

> **软件工程观察 22.8**
>
> *STL 算法不依赖于其操作容器的实现细节。只要容器（或数组）的迭代器满足算法的要求，STL 算法就可以用于 C 风格、基于指针的数组、STL 容器以及用户定义的数据结构。*

> **软件工程观察 22.9**
>
> *可以在不修改容器类的情况下轻松地向 STL 添加算法。*

```cpp
int main()
{
    const int SIZE = 10;
    int a1[ SIZE ] = { 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 };
    int a2[ SIZE ] = { 1, 2, 3, 4, 1000, 6, 7, 8, 9, 10 };
    vector< int > v1( a1, a1 + SIZE ); // copy of a1
    vector< int > v2( a1, a1 + SIZE ); // copy of a1
    vector< int > v3( a2, a2 + SIZE ); // copy of a2
    ostream_iterator< int > output( cout, " " );

    cout << "Vector v1 contains: ";
    copy( v1.begin(), v1.end(), output );
    cout << "\nVector v2 contains: ";
    copy( v2.begin(), v2.end(), output );
    cout << "\nVector v3 contains: ";
    copy( v3.begin(), v3.end(), output );

    // compare vectors v1 and v2 for equality
    bool result = equal( v1.begin(), v1.end(), v2.begin() );
    cout << "\n\nVector v1 " << ( result ? "is" : "is not" )
         << " equal to vector v2.\n";

    // compare vectors v1 and v3 for equality
    result = equal( v1.begin(), v1.end(), v3.begin() );
    cout << "Vector v1 " << ( result ? "is" : "is not" )
         << " equal to vector v3.\n";

    // location represents pair of vector iterators
    pair< vector< int >::iterator, vector< int >::iterator > location;

    // check for mismatch between v1 and v3
    location = mismatch( v1.begin(), v1.end(), v3.begin() );
    cout << "\nThere is a mismatch between v1 and v3 at location "
         << ( location.first - v1.begin() ) << "\nwhere v1 contains "
         << *location.first << " and v3 contains " << *location.second
         << "\n";

    char c1[ SIZE ] = "HELLO";
    char c2[ SIZE ] = "BYE BYE";

    // perform lexicographical comparison of c1 and c2
    result = lexicographical_compare( c1, c1 + SIZE, c2, c2 + SIZE );
    cout << c1 << ( result ? " is less than " :
         " is greater than or equal to " ) << c2 << endl;
} // end main
```

```text
Vector v1 contains: 1 2 3 4 5 6 7 8 9 10
Vector v2 contains: 1 2 3 4 5 6 7 8 9 10
Vector v3 contains: 1 2 3 4 1000 6 7 8 9 10

Vector v1 is equal to vector v2.
Vector v1 is not equal to vector v3.
```

**图 22.27** | 算法 equal、mismatch 和 lexicographical_compare。（第 2 部分，共 3 部分。）

