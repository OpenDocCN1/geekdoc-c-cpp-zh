

```cpp
1 /**
2  * Merge rhs into the priority queue.
3  * rhs becomes empty. rhs must be different from this.
4  * Exercise 6.35 needed to make this operation more efficient.
5  */
6 void merge( BinomialQueue & rhs )
7 {
8     if( this == &rhs )     // Avoid aliasing problems
9         return;
10
11     currentSize += rhs.currentSize;
12
13     if( currentSize > capacity( ) )
14     {
15         int oldNumTrees = theTrees.size( );
16         int newNumTrees = max( theTrees.size( ), rhs.theTrees.size( ) ) + 1;
17         theTrees.resize( newNumTrees );
18         for( int i = oldNumTrees; i < newNumTrees; ++i )
19             theTrees[ i ] = nullptr;
20     }
21
22     BinomialNode *carry = nullptr;
23     for( int i = 0, j = 1; j <= currentSize; ++i, j *= 2 )
24     {
25         BinomialNode *t1 = theTrees[ i ];
26         BinomialNode *t2 = i < rhs.theTrees.size( ) ? rhs.theTrees[ i ]
27                                                : nullptr;
28         int whichCase = t1 == nullptr ? 0 : 1;
29         whichCase += t2 == nullptr ? 0 : 2;
30         whichCase += carry == nullptr ? 0 : 4;
31
32         switch( whichCase )
33         {
34             case 0: /* No trees     */
35             case 1: /* Only this    */
36                 break;
37             case 2: /* Only rhs     */
38                 theTrees[ i ] = t2;
39                 rhs.theTrees[ i ] = nullptr;
40                 break;
41             case 4: /* Only carry   */
42                 theTrees[ i ] = carry;
43                 carry = nullptr;
44                 break;
45             case 3: /* this and rhs */
46                 carry = combineTrees( t1, t2 );
47                 theTrees[ i ] = rhs.theTrees[ i ] = nullptr;
48                 break;
49
50             case 5: /* this and carry */
51                 carry = combineTrees( t1, carry );
52                 theTrees[ i ] = nullptr;
53                 break;
54             case 6: /* rhs and carry */
55                 carry = combineTrees( t2, carry );
56                 rhs.theTrees[ i ] = nullptr;
57                 break;
58             case 7: /* All three */
59                 theTrees[ i ] = carry;
60                 carry = combineTrees( t1, t2 );
61                 rhs.theTrees[ i ] = nullptr;
62                 break;
63         }
64
65         for( auto & root : rhs.theTrees )
66             root = nullptr;
67         rhs.currentSize = 0;
68     }
}
```

图 6.55 合并两个优先队列的例程

```cpp
1 /**
2  * Remove the minimum item and place it in minItem.
3  * Throws UnderflowException if empty.
4  */
5 void deleteMin( Comparable & minItem )
6 {
7     if( isEmpty( ) )
8         throw UnderflowException( );
9
10    int minIndex = findMinIndex( );
11    minItem = theTrees[ minIndex ]->element;
12
13    BinomialNode *oldRoot = theTrees[ minIndex ];
14    BinomialNode *deletedTree = oldRoot->leftChild;
15    delete oldRoot;
16
17    // Construct H''
18    BinomialQueue deletedQueue;
19    deletedQueue.theTrees.resize( minIndex + 1 );
20    deletedQueue.currentSize = ( 1 << minIndex ) - 1;
21    for( int j = minIndex - 1; j >= 0; --j )
22    {
23        deletedQueue.theTrees[ j ] = deletedTree;
24        deletedTree = deletedTree->nextSibling;
25        deletedQueue.theTrees[ j ]->nextSibling = nullptr;
26    }
27
28    // Construct H'
29    theTrees[ minIndex ] = nullptr;
30    currentSize -= deletedQueue.currentSize + 1;
31
32    merge( deletedQueue );
33 }
34
35 /**
36 * Find index of tree containing the smallest item in the priority queue.
37 * The priority queue must not be empty.
38 * Return the index of tree containing the smallest item.
39 */
40 int findMinIndex( ) const
41 {
42    int i;
43    int minIndex;
44
45    for( i = 0; theTrees[ i ] == nullptr; ++i )
46    ;
47
48    for( minIndex = i; i < theTrees.size( ); ++i )
49    if( theTrees[ i ] != nullptr &&
50        theTrees[ i ]->element < theTrees[ minIndex ]->element )
51        minIndex = i;
52
53    return minIndex;
54 }
```

图 6.56 二项式队列的 deleteMin

```cpp
#include <iostream>
#include <vector>
#include <queue>
#include <functional>
#include <string>
using namespace std;

// Empty the priority queue and print its contents.
template <typename PriorityQueue>
void dumpContents( const string & msg, PriorityQueue & pq )
{
    cout << msg << ":\t" << endl;
    while( !pq.empty( ) )
        cout << pq.top( ) << endl;
    pq.pop( );
}

// Do some inserts and removes (done in dumpContents).
int main( )
{
    priority_queue<int> maxPQ;
    priority_queue<int,vector<int>,greater<int>> minPQ;

    minPQ.push( 4 ); minPQ.push( 3 ); minPQ.push( 5 );
    maxPQ.push( 4 ); maxPQ.push( 3 ); maxPQ.push( 5 );

    dumpContents( "minPQ", minPQ ); // 3 4 5
    dumpContents( "maxPQ", maxPQ ); // 5 4 3

    return 0;
}
```

图 6.57 演示 STL priority_queue 的例程；注释显示预期的输出顺序

## 6.9 标准库中的优先队列

二叉堆在 STL 中由标准头文件 queue 中的类模板 priority_queue 实现。STL 实现的是最大堆而不是最小堆，因此访问的是最大元素而不是最小元素。关键成员函数如下：

```cpp
void push( const Object & x );
const Object & top( ) const;
void pop( );
bool empty( );
void clear( );
```

push 将 x 添加到优先队列中，top 返回优先队列中的最大元素，pop 从优先队列中删除最大元素。允许重复元素；如果有多个最大元素，则只删除其中一个。

优先队列模板用元素类型、容器类型（几乎总是希望使用存储元素的 vector）和比较器进行实例化；最后两个参数允许使用默认值，默认值生成最大堆。使用 greater 函数对象作为比较器可生成最小堆。

图 6.57 展示了一个测试程序，说明如何将 priority_queue 类模板同时用作默认最大堆和最小堆。

## 小结

在本章中，我们了解了优先队列 ADT 的各种实现和用途。标准二叉堆实现因其简洁和高速而优雅。它不需要链接，只需要常数级的额外空间，却能高效地支持优先队列操作。

我们还考虑了额外的合并操作，并开发了三种实现，每种都有其独特之处。左偏堆是递归力量的绝佳示例。斜堆因缺乏平衡准则而代表了一种非凡的数据结构。我们将在第 11 章对其进行分析，这本身也很有趣。二项式队列展示了如何利用一个简单的想法来实现良好的时间界限。

我们还了解了优先队列的几种用途，从操作系统调度到模拟。我们将在第 7、9 和 10 章中再次看到它们的用途。

## 练习

- 6.1 insert 和 findMin 都能在常数时间内实现吗？

- 6.2 a. 将 10, 12, 1, 14, 6, 5, 8, 15, 3, 9, 7, 4, 11, 13, 和 2 逐个插入最初为空的二叉堆中，显示结果。
- b. 使用线性时间算法构建二叉堆，使用相同的输入，显示结果。

- 6.3 在上一题的堆中执行三次 deleteMin 操作，显示结果。

- 6.4 含 N 个元素的完全二叉树使用数组位置 1 到 N。假设我们尝试使用非完全二叉树的数组表示。确定以下情况数组必须有多大。
- a. 具有两个额外层级的二叉树（即非常轻微不平衡）
- b. 最深节点深度为 2 log N 的二叉树
- c. 最深节点深度为 4 + 1 log N 的二叉树
- d. 最坏情况二叉树

- 6.5 通过将插入项的副本放在位置 0 来重写 BinaryHeap insert 例程。

- 6.6 图 6.13 中的大堆有多少个节点？

- 6.7 a. 证明对于二叉堆，buildHeap 最多进行 2N - 2 次元素间的比较。
- b. 证明八个元素的堆可以通过八次堆元素间的比较来构建。
- ** c. 给出一个在 (13/8)N + O(log N) 次元素比较内构建二叉堆的算法。

- 6.8 关于堆中最大元素，证明以下内容：
- a. 它必须位于某个叶节点上。
- b. 恰好有 [N/2] 个叶节点。
- c. 必须检查每个叶节点才能找到它。

- ** 6.9 证明在大型完全堆中，第 k 小元素的预期深度（可假设 N = 2^k - 1）被 log k 所界定。

- 6.10 * a. 给出一个在二叉堆中查找所有小于某个值 X 的节点的算法。你的算法应在 O(K) 时间内运行，其中 K 是输出的节点数。
- b. 你的算法是否可扩展到本章讨论的其他堆结构？
- * c. 给出一个在二叉堆中查找任意元素 X 的算法，使用的比较次数最多约为 3N/4 次。

- ** 6.11 提出一个在 O(M + log N log log N) 时间内将 M 个节点插入含 N 个元素的二叉堆的算法。证明你的时间界限。

- 6.12 编写一个程序，读取 N 个元素并执行以下操作：
- a. 将它们逐个插入堆中。
- b. 在线性时间内构建堆。
- 比较两种算法在有序、逆序和随机输入上的运行时间。

- 6.13 每次 deleteMin 操作在最坏情况下使用 2 log N 次比较。
- * a. 提出一个方案，使 deleteMin 操作仅使用 log N + log log N + O(1) 次元素间的比较。这不一定意味着更少的数据移动。
- ** b. 扩展部分 (a) 中的方案，使仅执行 log N + log log log N + O(1) 次比较。
- ** c. 这个想法可以推广到何种程度？
- d. 比较次数的节省是否弥补了算法复杂度的增加？

- 6.14 如果 d-堆存储为数组，对于位于位置 i 的条目，其父节点和子节点在哪里？

