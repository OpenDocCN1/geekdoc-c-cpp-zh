# 292 CHAPTER 10 Algorithm Efficiency

> Note: In general, you should avoid analyzing an algorithm by studying the running-times of a specific implementation. Times are influenced by such factors as programming style, the particular computer, and the data on which the program is run.

Counting an algorithm's operations is a way to assess its efficiency

# 10.2.1 The Execution Time of Algorithms

Previous chapters have informally compared different solutions to a problem by looking at the number of operations that each solution required. For example, Chapter 4 compared array-based and link-based implementations of the ADT bag. An array based bag can access its $i^{th}$ element directly in one step, because the element is stored in $[i-1]$. A link-based bag, however, must traverse a chain of linked nodes until the $i^{th}$ node is reached and therefore require $i$ steps.

An algorithm's efficiency is related to the number of operations it requires. It is usually expressed in terms of the number, $n$, of items the algorithm must process. Counting an algorithm's operations—if possible—is a way to assess its efficiency. Let us consider a few examples:

**Traversal of linked nodes.** As an example of traversing a chain of linked nodes, displaying the data in such a chain. If headPtr points to the first node in the chain, the following C++ code displays:

```
Node<ItemType>* curPtr = headPtr;
while (curPtr != nullptr) {
    cout << curPtr->getItem() << endl;
    n++;
    comparisons++;
    curPtr = curPtr->getNext();
}
```

Displaying the data in a linked chain of $n$ nodes requires proportional to $n$

If we have $n$ nodes, these statements require $n+1$ comparisons, and $n$ write operations. If each assignment, comparison, and write operation, respectively, $a$, $c$, and $w$ time units, the time $(n+1) 	imes (a+c) + n 	imes w$ time units. Thus, the time to write $n$ nodes is proportional to $n$. This conclusion makes sense intuitively: It takes longer to display, or traverse, a chain of 100 nodes than it does a chain of 10 nodes.

> Note: You must traverse a linked chain to access its $i^{th}$ node. The access time is, directly proportional to $i$. On the other hand, you can access items directly, with equal access time for each item.

**The Towers of Hanoi.** Chapter 2 proved recursively the solution to the Towers of Hanoi with $n$ disks requires $2^n-1$ moves. If each move requires the same time $m$, the number of moves grows exponentially. You will soon see, this time requirement increases rapidly as the number of disks increases.

Nested loops. Consider an algorithm that contains nested loops of the following form:

```
for (i = 1; i <= n; i++) {
    for (j = 1; j <= i; j++) {
        for (k = 1; k <= 5; k++) {
            task;
        }
    }
```

Without omitting multiplication operators is common in algebra, we indicate them explicitly to facilitate counting them.