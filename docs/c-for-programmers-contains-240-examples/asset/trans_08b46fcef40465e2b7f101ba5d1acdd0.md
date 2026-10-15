

一个使用整数向量作为底层数据结构的整数栈。Line 26 指定了一个使用整数列表作为底层数据结构的整数栈。

函数 pushElements（第 49–56 行）将元素压入每个栈。Line 53 使用函数 push（在每个适配器类中均可用）将一个整数置于栈顶。Line 54 使用栈函数 top 获取栈顶元素以输出。函数 top 不会移除栈顶元素。

函数 popElements（第 59–66 行）将元素从每个栈弹出。Line 63 使用栈函数 top 获取栈顶元素以输出。Line 64 使用函数 pop（在每个适配器类中均可用）移除栈顶元素。函数 pop 不返回任何值。

```
// Fig. 20.23: fig20_23.cpp
// Standard Library adapter stack test program.
#include <iostream>
using std::cout;
using std::endl;

#include <stack> // stack adapter definition
#include <vector> // vector class-template definition
#include <list> // list class-template definition

// pushElements function-template prototype
template< typename T > void pushElements( T &stackRef );

// popElements function-template prototype
template< typename T > void popElements( T &stackRef );

int main()
{
    // stack with default underlying deque
    std::stack< int > intDequeStack;

    // stack with underlying vector
    std::stack< int, std::vector< int > > intVectorStack;

    // stack with underlying list
    std::stack< int, std::list< int > > intListStack;

    // push the values 0-9 onto each stack
    cout << "Pushing onto intDequeStack: ";
    pushElements( intDequeStack );
    cout << "\nPushing onto intVectorStack: ";
    pushElements( intVectorStack );
    cout << "\nPushing onto intListStack: ";
    pushElements( intListStack );
    cout << endl << endl;

    // display and remove elements from each stack
    cout << "Popping from intDequeStack: ";
    popElements( intDequeStack );
```
```
40  cout << "\nPopping from intVectorStack: ";
41  popElements( intVectorStack );
42  cout << "\nPopping from intListStack: ";
43  popElements( intListStack );
44  cout << endl;
45  return 0;
46 } // end main

// push elements onto stack object to which stackRef refers
template< typename T > void pushElements( T &stackRef )
{
  for ( int i = 0; i < 10; i++ )
  {
    stackRef.push( i ); // push element onto stack
    cout << stackRef.top() << ' '; // view (and display) top element
  } // end for
} // end function pushElements

// pop elements from stack object to which stackRef refers
template< typename T > void popElements( T &stackRef )
{
  while ( !stackRef.empty() )
  {
    cout << stackRef.top() << ' '; // view (and display) top element
    stackRef.pop(); // remove top element
  } // end while
} // end function popElements
```

Pushing onto intDequeStack: 0 1 2 3 4 5 6 7 8 9
Pushing onto intVectorStack: 0 1 2 3 4 5 6 7 8 9
Pushing onto intListStack: 0 1 2 3 4 5 6 7 8 9

Popping from intDequeStack: 9 8 7 6 5 4 3 2 1 0
Popping from intVectorStack: 9 8 7 6 5 4 3 2 1 0
Popping from intListStack: 9 8 7 6 5 4 3 2 1 0

Fig. 20.23 | Standard Library stack adapter class. (Part 2 of 2.)

## 20.4.2 queue Adapter

类 queue 允许在底层数据结构的末尾插入，并在前端删除（通常称为先进先出数据结构）。队列可以用 STL 数据结构 list 或 deque 实现。默认情况下，队列使用 deque 实现。常见的队列操作有 push 用于在队列末尾插入元素（通过调用底层容器的 push_back 函数实现），pop 用于移除队列前端的元素（通过调用底层容器的 pop_front 函数实现），front 用于获取队列中第一个元素的引用（通过调用底层容器的 front 函数实现），back 用于获取队列中最后一个元素的引用（通过调用底层容器的 back 函数实现），empty 用于确定队列是否为空（通过调用底层容器的 empty 函数实现）以及 size 用于获取队列中的元素数量（通过调用底层容器的 size 函数实现）。

## Performance Tip 20.18

队列的每个常用操作都实现为一个内联函数，该函数调用底层容器的相应函数。这避免了第二次函数调用的开销。

## Performance Tip 20.19

为了获得最佳性能，请使用类 deque 作为队列的底层容器。

Figure 20.24 演示了 queue 适配器类。要使用 queue，必须包含头文件 <queue>。

Line 11 实例化了一个存储 double 值的队列。Lines 14–16 使用函数 push 向队列添加元素。Lines 21–25 中的 while 语句使用函数 empty（所有容器均可用）来确定队列是否为空（line 21）。只要队列中还有更多元素，line 23 就使用队列函数 front 读取（但不移除）队列中的第一个元素以输出。Line 24 使用函数 pop（所有适配器类均可用）移除队列中的第一个元素。

```
// Fig. 20.24: fig20_24.cpp
// Standard Library adapter queue test program.
#include <iostream>
using std::cout;
using std::endl;

#include <queue> // queue adapter definition

int main()
{
    std::queue< double > values; // queue with doubles

    // push elements onto queue values
    values.push( 3.2 );
    values.push( 9.8 );
    values.push( 5.4 );

    cout << "Popping from values: ";

    // pop elements from queue
    while ( !values.empty() )
    {
        cout << values.front() << ' '; // view front element
        values.pop(); // remove element
    } // end while

    cout << endl;
    return 0;
} // end main
```

Popping from values: 3.2 9.8 5.4

Fig. 20.24 | Standard Library queue adapter class templates.

## 20.4.3 priority_queue Adapter

类 priority_queue 提供在底层数据结构中按排序顺序插入并从底层数据结构前端删除的功能。priority_queue 可以使用 STL 序列容器 vector 或 deque 实现。默认情况下，priority_queue 使用 vector 作为底层容器。当元素添加到 priority_queue 时，它们会按优先级顺序插入，使得最高优先级元素（即最大值的元素）将成为从 priority_queue 中移除的第一个元素。这通常通过一种称为 heapsort 的排序技术实现，该技术始终保持最大值的元素（即最高优先级元素）在数据结构的前端——这种数据结构称为堆。元素的比较默认使用比较函数对象 less<T> 执行，但你可以提供不同的比较器。

有几个常见的 priority_queue 操作。push 根据 priority_queue 的优先级顺序在适当位置插入元素（通过调用底层容器的 push_back 函数，然后使用 heapsort 重新排序元素实现）。pop 移除 priority_queue 的最高优先级元素（通过在移除堆顶元素后调用底层容器的 pop_back 函数实现）。top 获取 priority_queue 顶元素的引用（通过调用底层容器的 front 函数实现）。empty 确定 priority_queue 是否为空（通过调用底层容器的 empty 函数实现）。size 获取 priority_queue 中的元素数量（通过调用底层容器的 size 函数实现）。

## Performance Tip 20.20

priority_queue 的每个常用操作都实现为一个内联函数，该函数调用底层容器的相应函数。这避免了第二次函数调用的开销。

## Performance Tip 20.21

为了获得最佳性能，请使用类 vector 作为 priority_queue 的底层容器。

Figure 20.25 演示了 priority_queue 适配器类。要使用类 priority_queue，必须包含头文件 <queue>。

```
// Fig. 20.25: fig20_25.cpp
// Standard Library adapter priority_queue test program.
#include <iostream>
using std::cout;
using std::endl;

#include <queue> // priority_queue adapter definition

int main()
{
    std::priority_queue< double > priorities; // create priority_queue
