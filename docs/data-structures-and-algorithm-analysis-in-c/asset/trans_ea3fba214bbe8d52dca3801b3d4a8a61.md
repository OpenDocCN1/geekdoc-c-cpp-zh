

![](img/e449061a0cac9cafaefd979fab665b33_270_0.png)

![](img/e449061a0cac9cafaefd979fab665b33_270_1.png)

请确保不要假设总是有两个子节点，因此这通常涉及额外的测试。在图 6.12 所示的代码中，我们在第 40 行执行了此测试。一个极其棘手的解决方案是始终确保你的算法认为每个节点都有两个子节点。具体做法是在堆结束后的位置放置一个值大于堆中任何元素的哨兵，在每次下滤开始时，当堆大小为偶数时这样做。在尝试此方法之前应三思而后行，如果使用此技术，必须加上醒目的注释。虽然这消除了测试右子节点是否存在的需要，但你无法消除到达底部时进行测试的要求，因为这将需要为每个叶子节点设置哨兵。

此操作的最坏情况运行时间为 O(log N)。平均而言，放置在根节点的元素会下滤到堆的几乎底部（即它来自的层级），因此平均运行时间为 O(log N)。

## 6.3.4 其他堆操作

请注意，虽然查找最小值可以在常数时间内完成，但专为查找最小元素而设计的堆（也称为最小堆）对于查找最大元素毫无帮助。事实上，堆包含的顺序信息非常少，

```cpp
/**
 * Remove the minimum item.
 * Throws UnderflowException if empty.
 */
void deleteMin()
{
    if ( isEmpty( ) )
        throw UnderflowException( );

    array[ 1 ] = std::move( array[ currentSize-- ] );
    percolateDown( 1 );
}
```

```cpp
/**
 * Remove the minimum item and place it in minItem.
 * Throws UnderflowException if empty.
 */
void deleteMin( Comparable &minItem )
{
    if ( isEmpty( ) )
        throw UnderflowException( );

    minItem = std::move( array[ 1 ] );
    array[ 1 ] = std::move( array[ currentSize-- ] );
    percolateDown( 1 );
}
```

```cpp
/**
 * Internal method to percolate down in the heap.
 * hole is the index at which the percolate begins.
 */
void percolateDown( int hole )
{
    int child;
    Comparable tmp = std::move( array[ hole ] );

    for( ; hole * 2 <= currentSize; hole = child )
    {
        child = hole * 2;
        if( child != currentSize && array[ child + 1 ] < array[ child ] )
            ++child;
        if( array[ child ] < tmp )
            array[ hole ] = std::move( array[ child ] );
        else
            break;
    }
    array[ hole ] = std::move( tmp );
}
```

图 6.12 在二叉堆中执行 deleteMin 的方法

![](img/e449061a0cac9cafaefd979fab665b33_272_0.png)

图 6.13 一棵非常大的完全二叉树

因此，除非对整个堆进行线性扫描，否则无法找到任何特定元素。要理解这一点，请考虑图 6.13 中的大型堆结构（未显示元素），我们可以看到，关于最大元素的唯一已知信息是它位于某个叶子节点上。然而，一半的元素都包含在叶子节点中，因此这几乎是无用的信息。出于这个原因，如果知道元素的位置很重要，除了堆之外，还必须使用其他数据结构，例如哈希表。（请记住，模型不允许查看堆内部。）

如果假设每个元素的位置通过其他方法已知，那么几个其他操作将变得廉价。下面的前三个操作都以对数最坏情况时间运行。

### decreaseKey

decreaseKey(p, Δ) 操作将位置 p 处的项目值降低正数量 Δ。由于这可能违反堆序，必须通过上滤来修复。此操作对系统管理员可能很有用：他们可以使自己的程序以最高优先级运行。

### increaseKey

increaseKey(p, Δ) 操作将位置 p 处的项目值增加正数量 Δ。这是通过下滤完成的。许多调度程序会自动降低占用过多 CPU 时间的进程的优先级。

### remove

remove(p) 操作从堆中移除位置 p 处的节点。这是通过先执行 decreaseKey(p, ∞) 然后执行 deleteMin() 来完成的。当进程被用户终止（而不是正常结束）时，必须从优先队列中移除它。

### buildHeap

二叉堆有时是从初始项目集构建的。此构造函数以 N 个项目作为输入并将它们放入堆中。显然，这可以通过 N 次连续插入完成。由于每次插入平均耗时 O(1)，最坏情况耗时 O(log N)，因此该算法的总运行时间平均为 O(N)，最坏情况为 O(N log N)。由于这是一条特殊指令且中间没有其他操作，并且我们已经知道该指令可以在平均线性时间内执行，因此可以合理地期望，通过合理的注意可以保证线性时间界。

一般算法是将 N 个项目以任意顺序放入树中，同时保持结构属性。然后，如果 percolateDown(i) 从节点 i 开始下滤，构造函数可以使用图 6.14 中的 buildHeap 例程来创建一个堆有序树。

图 6.15 中的第一棵树是无序树。图 6.15 到 6.18 中的其余七棵树显示了每次七次下滤的结果。每条虚线对应两次比较：一次用于找到较小的子节点，一次用于将较小的子节点与节点进行比较。请注意，整个算法中只有 10 条虚线（可能有第 11 条——在哪里？），对应 20 次比较。

为了限制 buildHeap 的运行时间，我们必须限制虚线的数量。这可以通过计算堆中所有节点的高度之和来完成，这是虚线的最大数量。我们希望证明这个和是 O(N)。

```cpp
explicit BinaryHeap( const vector<Comparable> & items )
    : array( items.size( ) + 10 ), currentSize{ items.size( ) }
{
    for( int i = 0; i < items.size( ); ++i )
        array[ i + 1 ] = items[ i ];
    buildHeap( );
}

/**
 * Establish heap order property from an arbitrary
 * arrangement of items. Runs in linear time.
 */
void buildHeap( )
{
    for( int i = currentSize / 2; i > 0; --i )
        percolateDown( i );
}
```

图 6.14 buildHeap 和构造函数

![](img/e449061a0cac9cafaefd979fab665b33_274_0.png)

![](img/e449061a0cac9cafaefd979fab665b33_274_1.png)

![](img/e449061a0cac9cafaefd979fab665b33_274_2.png)

**定理 6.1**
对于包含 2^{h+1} - 1 个节点的高度为 h 的完美二叉树，节点高度之和为 2^{h+1} - 1 - (h + 1)。

**证明**
很容易看出，这棵树由高度 h 处的 1 个节点、高度 h - 1 处的 2 个节点、高度 h - 2 处的 2^2 个节点组成，一般来说，高度 h - i 处有 2^i 个节点。所有节点的高度之和为

\( S = \sum_{i=0}^{h} 2^i(h - i) \)
\( = h + 2(h - 1) + 4(h - 2) + 8(h - 3) + 16(h - 4) + \cdots + 2^{h-1}(1) \) (6.1)

两边乘以 2 得到方程

\( 2S = 2h + 4(h - 1) + 8(h - 2) + 16(h - 3) + \cdots + 2^h(1) \) (6.2)

我们减去这两个方程并得到方程 (6.3)。我们发现某些项几乎相互抵消。例如，我们有 \( 2h - 2(h - 1) = 2 \)，\( 4(h - 1) - 4(h - 2) = 4，依此类推。方程 (6.2) 中的最后一项 \( 2^h \) 不出现在方程 (6.1) 中；因此，它出现在方程 (6.3) 中。方程 (6.1) 中的第一项 \( h \) 不出现在方程 (6.2) 中；因此，\( -h \) 出现在方程 (6.3) 中。我们得到

\( S = -h + 2 + 4 + 8 + \cdots + 2^{h-1} + 2^h = (2^{h+1} - 1) - (h + 1) \) (6.3)

这证明了定理。

完全树不是完美二叉树，但我们得到的结果是完全树中节点高度之和的上界。由于完全树的节点数在 \( 2^h \) 到 \( 2^{h+1} \) 之间，该定理表明这个和是 \( O(N) \)，其中 \( N \) 是节点数。

尽管我们得到的结果足以证明 buildHeap 是线性的，但高度之和的上界并不尽可能强。对于具有 \( N = 2^h \) 个节点的完全树，我们得到的上界大约是 \( 2N \)。可以通过归纳法证明高度之和为 \( N - b(N) \)，其中 \( b(N) \) 是 \( N \) 的二进制表示中 1 的个数。

## 6.4 优先队列的应用

我们已经提到过优先队列在操作系统设计中的用法。在第 9 章中，我们将看到如何使用优先队列高效地实现多个图算法。在这里，我们将展示如何使用优先队列来求解两个问题的解决方案。

