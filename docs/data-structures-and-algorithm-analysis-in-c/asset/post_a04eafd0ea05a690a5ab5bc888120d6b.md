
## 6.3 Binary Heap

The implementation we will use is known as a **binary heap**. Its use is so common for priority queue implementations that, in the context of priority queues, when the word *heap* is used without a qualifier, it is generally assumed to be referring to this implementation of the data structure. In this section, we will refer to binary heaps merely as *heaps*. Like binary search trees, heaps have two properties, namely, a structure property and a heap-order property. As with AVL trees, an operation on a heap can destroy one of the properties, so a heap operation must not terminate until all heap properties are in order. This turns out to be simple to do.

### 6.3.1 Structure Property

A heap is a binary tree that is completely filled, with the possible exception of the bottom level, which is filled from left to right. Such a tree is known as a **complete binary tree**. Figure 6.2 shows an example.

It is easy to show that a complete binary tree of height *h* has between 2^h and 2^(h+1) - 1 nodes. (This implies that the height of a complete binary tree is ⌈log N⌉, which is clearly O(log N).)

An important observation is that because a complete binary tree is so regular, it can be represented in an array and no links is necessary. The array in Figure 6.3 corresponds to the heap in Figure 6.2.

![](img/e449061a0cac9cafaefd979fab665b33_265_0.png)

**Figure 6.2** A complete binary tree

| | A | B | C | D | E | F | G | H | I | J | | | |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 | 12 | 13 |

**Figure 6.3** Array implementation of complete binary tree

```
template <typename Comparable>
class BinaryHeap
{
  public:
    explicit BinaryHeap( int capacity = 100 );
    explicit BinaryHeap( const vector<Comparable> & items );

    bool isEmpty( ) const;
    const Comparable & findMin( ) const;

    void insert( const Comparable & x );
    void insert( Comparable && x );
    void deleteMin( );
    void deleteMin( Comparable & minItem );
    void makeEmpty( );

  private:
    int currentSize; // Number of elements in heap
    vector<Comparable> array; // The heap array

    void buildHeap( );
    void percolateDown( int hole );
};
```

Figure 6.4 Class interface for priority queue

For any element in array position i, the left child is in position 2i, the right child is in the cell after the left child (2i + 1), and the parent is in position ⌊i/2⌋. Thus, not only are links not required, but the operations required to traverse the tree are extremely simple and likely to be very fast on most computers. The only problem with this implementation is that an estimate of the maximum heap size is required in advance, but typically this is not a problem (and we can resize if needed). In Figure 6.3 the limit on the heap size is 13 elements. The array has a position 0; more on this later.

A heap data structure will, then, consist of an array (of Comparable objects) and an integer representing the current heap size. Figure 6.4 shows a priority queue interface.

Throughout this chapter, we shall draw the heaps as trees, with the implication that an actual implementation will use simple arrays.

### 6.3.2 Heap-Order Property

The property that allows operations to be performed quickly is the heap-order property. Since we want to be able to find the minimum quickly, it makes sense that the smallest element should be at the root. If we consider that any subtree should also be a heap, then any node should be smaller than all of its descendants.

![](img/e449061a0cac9cafaefd979fab665b33_267_0.png)

Figure 6.5 Two complete trees (only the left tree is a heap)

Applying this logic, we arrive at the heap-order property. In a heap, for every node X, the key in the parent of X is smaller than (or equal to) the key in X, with the exception of the root (which has no parent).2 In Figure 6.5 the tree on the left is a heap, but the tree on the right is not (the dashed line shows the violation of heap order). By the heap-order property, the minimum element can always be found at the root. Thus, we get the extra operation, findMin, in constant time.

### 6.3.3 Basic Heap Operations

It is easy (both conceptually and practically) to perform the two required operations. All the work involves ensuring that the heap-order property is maintained.

#### insert

To insert an element X into the heap, we create a hole in the next available location, since otherwise, the tree will not be complete. If X can be placed in the hole without violating heap order, then we do so and are done. Otherwise, we slide the element that is in the hole's parent node into the hole, thus bubbling the hole up toward the root. We continue this process until X can be placed in the hole. Figure 6.6 shows that to insert 14, we create a hole in the next available location. Inserting 14 in the hole would violate the heap-order property, so 31 is slid down into the hole. This strategy is continued in Figure 6.7 until the correct location for 14 is found.

This general strategy is known as a percolate up; the new element is percolated up the heap until the correct location is found. Insertion is easily implemented with the code shown in Figure 6.8.

2 Analogously we can declare a (max) heap, which enables us to efficiently find and remove the maximum element by changing the heap-order property. Thus, a priority queue can be used to find either a minimum or a maximum, but this needs to be decided ahead of time.

![](img/e449061a0cac9cafaefd979fab665b33_268_0.png)

![](img/e449061a0cac9cafaefd979fab665b33_268_1.png)

```
1 /**
2  * Insert item x, allowing duplicates.
3  */
4 void insert( const Comparable & x )
5 {
6     if( currentSize == array.size( ) - 1 )
7         array.resize( array.size( ) * 2 );
8
9     // Percolate up
10    int hole = ++currentSize;
11    Comparable copy = x;
12
13    array[ 0 ] = std::move( copy );
14    for( ; x < array[ hole / 2 ]; hole /= 2 )
15        array[ hole ] = std::move( array[ hole / 2 ] );
16    array[ hole ] = std::move( array[ 0 ] );
17 }
```

Figure 6.8 Procedure to insert into a binary heap

We could have implemented the percolation in the insert routine by performing repeated swaps until the correct order was established, but a swap requires three assignment statements. If an element is percolated up d levels, the number of assignments performed by the swaps would be 3d. Our method uses d + 1 assignments.

If the element to be inserted is the new minimum, it will be pushed all the way to the top. At some point, hole will be 1 and we will want to break out of the loop. We could do this with an explicit test, or we can put a copy of the inserted item in position 0 in order to make the loop terminate. We elect to place X into position 0.

The time to do the insertion could be as much as O(log N), if the element to be inserted is the new minimum and is percolated all the way to the root. On average, the percolation terminates early; it has been shown that 2.607 comparisons are required on average to perform an insert, so the average insert moves an element up 1.607 levels.

#### deleteMin

deleteMins are handled in a similar manner as insertions. Finding the minimum is easy; the hard part is removing it. When the minimum is removed, a hole is created at the root. Since the heap now becomes one smaller, it follows that the last element X in the heap must move somewhere in the heap. If X can be placed in the hole, then we are done. This is unlikely, so we slide the smaller of the hole's children into the hole, thus pushing the hole down one level. We repeat this step until X can be placed in the hole. Thus, our action is to place X in its correct spot along a path from the root containing minimum children.

In Figure 6.9 the left figure shows a heap prior to the deleteMin. After 13 is removed, we must now try to place 31 in the heap. The value 31 cannot be placed in the hole, because this would violate heap order. Thus, we place the smaller child (14) in the hole, sliding the hole down one level (see Fig. 6.10). We repeat this again, and since 31 is larger than 19, we place 19 into the hole and create a new hole one level deeper. We then place 26 in the hole and create a new hole on the bottom level since, once again, 31 is too large. Finally, we are able to place 31 in the hole (Fig. 6.11). This general strategy is known as a percolate down. We use the same technique as in the insert routine to avoid the use of swaps in this routine.

A frequent implementation error in heaps occurs when there are an even number of elements in the heap, and the one node that has only one child is encountered. You must

![](img/e449061a0cac9cafaefd979fab665b33_269_0.png)

Figure 6.9 Creation of the hole at the root
