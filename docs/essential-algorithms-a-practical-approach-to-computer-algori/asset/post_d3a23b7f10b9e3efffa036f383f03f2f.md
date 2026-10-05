
# Chapter 6 Sorting

| | | |
|---|---|---|
| 0 | 0 | 0 |
| 1 | 1 | 1 |
| 2 | 2 | 2 |
| 7 | 4 | 3 |
| 4 | 5 | 4 |
| 5 | 6 | 5 |
| 6 | 3 | 6 |
| 7 | | 7 |
| 8 | | 8 |
| 9 | | 9 |

**Figure 6-4:** Improvements make bubblesort faster, but it still has O(N²) performance.

After placing 7 after 3, the algorithm continues moving through the array and doesn't find any other items to swap so it knows that 7 and those that follow are in their final positions and don't need to be examined. If some item nearer to the top were larger than 7, the first pass would have swapped it past 7. In the middle image shown in Figure 6-4, the final items are shaded to indicate they don't need to be checked during later passes. The algorithm knows item 7 and the items after it are in their final positions, so it starts its second pass, moving upward through the array at the first item before 7, which swaps with items 6, 5, and 4, this time holding item 3 in a temporary variable until it reaches its final position.

Now item 3 and those that come before it in the array are in their final positions, so they are shaded in the last image in Figure 6-4.

The algorithm makes one final downward pass through the array, starting the pass at value 4 and ending at value 6. No swaps occur during this pass, so the algorithm ends.

These improvements make bubblesort faster. (In one test sorting 10,000 items, bubblesort would take 2.5 seconds without improvements and 0.69 seconds with improvements.) But it still has O(N²) performance, so there's a limit to the size of the list you can sort with bubblesort.

# O(n log N Algorithms

O(n log N) algorithms are much faster than O(N²), at least for larger arrays. If N is 1,000, N log N is less than 1x10⁴, but N² is roughly 100 times as big at 1x1⁶. That difference in speed makes these algorithms more useful in everyday programming, as for large arrays.

# Heapsort

Heapsort uses a data structure called a heap and is a useful technique for storing a complete binary tree in an array.

# Storing Complete Binary Trees in Arrays

A binary tree is a tree where every node is connected to, at most, two children. In a complete tree (binary or otherwise), all the tree's levels are completely filled, except possibly the last level, where all the nodes are pushed to the left.

Figure 6-5 shows a complete binary tree holding 12 nodes. The tree's first three levels are full. The fourth level contains five nodes pushed to the left side of the tree.

![](img/fefa42765c0b410af6705110aea7c0cb_162_0.png)

**Figure 6-5**: In a complete binary tree, every level is full, except possibly the last.

One useful feature of complete binary trees is that you can easily store them in an array using a simple formula. Start by placing the root node at index 0. Then, for any node with index $i$, place its children at indices $2 \times i + 1$ and $2 \times i + 2$. If a node has index $j$, its parent has index $\lfloor(j-1)/2\rfloor$ where $\lfloor\rfloor$ means to truncate the result to the next-smaller integer (round down). For example, $\lfloor 2.9\rfloor$ is 2, and $\lfloor 2\rfloor$ is also 2.

Figure 6-6 shows the tree shown in Figure 6-5 stored in an array, with the entry's indices on top.

| 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 |
|---|---|---|---|---|---|---|---|---|---|---|---|
| 7 | 10 | 4 | 6 | 9 | 2 | 11 | 3 | 5 | 12 | 8 | |

**Figure 6-6**: You can easily store a complete binary tree in an array. For example, the value 6 is at index 4, so its children should be at $2 \times 4 + 1 = 9$ and $2 \times 4 + 2 = 10$. Those items have values 5 and 12. If you look at the tree shown in Figure 6-5, you'll see those are the correct children.

If the index of either child is greater than the largest index in the array, the node doesn't have child in the tree. For example, the value 9 has index 5. Its right child has $2 \times 5 + 2 = 12$, which is beyond the end of the array. If you look at Figure 6-5, you'll see the item with value 9 has no right child.

For an example of calculating a node's parent, the item with value 12 stored at index 10. The index of the parent is $(10 - 1) / 2 = 4$. The value at index 4 is 6. If you look at the tree shown in Figure 6-5, you'll see the node with value 12 has its parent the value 6.

# Defining Heaps

A heap, shown in Figure 6-7, is a complete binary tree where every node holds a value that is at least as large as all of its children. Figure 6-5 is not a heap because, for example, the root node has a value of 7, and its right child has a value of 10, which is greater.

![](img/fefa42765c0b410af6705110aea7c0cb_163_0.png)

**Figure 6-7**: In a heap, the value of every node is at least as large as the values of its children.

You can build a heap node at a time. Start with a tree consisting of a single node. Because it has no children, it satisfies the heap property.

Now suppose you have built a heap and you want to add a new node to it. Add the new node at the end of the tree. There is only one place where you can add this node to keep the complete binary tree—at the bottom level of the tree.

Now compare the new value to the value of its parent. If the new value is larger than the parent, swap them. Because the tree was previously a heap, you know that the parent's value was already larger than its other child (if it has one). By swapping it with a larger value, you know the heap property is preserved at this point.

However, you changed the value of the parent node, so you might break the heap property farther up the tree. Move up to the parent node, and compare its value to the value of its parent, swapping their values if necessary. Continue up the tree, swapping values if necessary, until you reach the root node. At that point the tree is again a heap.

Figure 6-8 shows this process when you add the value 12 to the tree shown in Figure 6-7. Figure 6-9 shows the new heap.

![](img/fefa42765c0b410af6705110aea7c0cb_164_0.png)

![](img/fefa42765c0b410af6705110aea7c0cb_164_1.png)

Storing the heap in an array makes this process particularly easy, because you need to add a new item to the end of the tree, it's already in the position in the array.

The following pseudocode shows the algorithm to turn an array into a heap:

```
MakeHeap(Data: values[])
  // Add each item to the heap one at a time.
  For i = 0 To <length of values> - 1
    // Start at the new item, and work up to the root.
    Integer: index = i
    While (index != 0)
      // Find the parent's index.
      Integer: parent = (index - 1) / 2

      // If child <= parent, we're done, so
      // break out of the While loop.
      If (values[index] <= values[parent]) Then Break

      // Swap the parent and child.
      Data: temp = values[index]
      values[index] = values[parent]
      values[parent] = temp

      // Move to the parent.
      index = parent

    End While
  Next i
End MakeHeap
```

Heaps are useful for creating priority queues because the largest item in the tree is always at the root node. When you need to remove an item from the queue, you use the item at the root.

Unfortunately, that breaks the heap, so it is no longer a tree. Frankly, there's an easy way to fix it: Move the last item in the tree to the root.

Doing so breaks the tree's heap property, but you can fix that using a method similar to the one you used to build the heap. If the new value is smaller than one of its children, swap it with the larger child. That fixes the heap property at this node, but may have broken it at the child's level; move down to that node and repeat the process. Continue swapping the node down into the tree until you find a spot where the heap property is adequately satisfied or you reach the bottom of the tree.
