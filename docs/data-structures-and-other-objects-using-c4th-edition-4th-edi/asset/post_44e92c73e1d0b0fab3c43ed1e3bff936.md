
## Heap Review (from Section 11.1)

A heap is a binary tree where the entries of the nodes can be compared with the less-than operator of a strict weak ordering. In addition, these two rules are followed:

- 1. The entry contained by a node is never less than the entries of the node's children.
- 2. The tree is a complete binary tree, so that every level except the deepest must contain as many nodes as possible; and at the deepest level, all nodes are as far left as possible (see “Complete binary trees” page 476).

A heap is a complete binary tree, and we have an efficient method for representing a complete binary tree in an array. This representation was first shown in Section 10.2, following these rules:

- Data from the root of the complete binary tree goes in the [0] component of the array.
- Data from the root's children is put in the next two components of the array.
- We continue in this way, placing the four nodes of depth two in the next four components of the array, and so forth. For example, a heap with 10 nodes can be stored in a 10-element array, as shown here:

![](img/7bf56f684fab50d5ff9e94ae2818f3ac_690_0.png)

To be more precise about the location of data in the array, we have these rules:

- 1. The data from the root always appears in the [0] component of the array.
- 2. Suppose that the data for a nonroot node appears in component [i] of the array. Then the data for its parent is always at location [(i-1)/2] (using integer division).
- 3. Suppose that the data for a node appears in component [i] of the array. Then its children (if they exist) always have their data at these locations: Left child at component [2i + 1]; Right child at component [2i + 2].

first, the array is made into a heap

With these facts in mind, we can easily state the general idea that underlies the heapsort algorithm. We start with an array of values to be sorted. The heapsort algorithm treats the array values as if they were values in a complete binary tree using the three rules listed previously. That much is easy since any array of n values represents some complete binary tree with n nodes.

The first step of the heapsort algorithm is to rearrange the values in the array so that the corresponding complete binary tree is a heap. In other words, we rearrange the array so that the corresponding complete binary tree follows the heapsort storage rule: The value contained in a node is never less than an entry from one of the node's children. For example, suppose the array begins with these values:

| 21 | 35 | 22 | 27 | 23 | 45 | 42 | 19 | 4 | 5 |
|---|---|---|---|---|---|---|---|---|---|
| [0] | [1] | [2] | [3] | [4] | [5] | [6] | [7] | [8] | [9] |

This array can be interpreted as representing this complete binary tree:

![](img/7bf56f684fab50d5ff9e94ae2818f3ac_691_0.png)

Of course, this complete binary tree is not a heap—for example, the data in the root's left child (35) is larger than the data in the root (21). So, the first step of the heapsort is to rearrange the array elements so that the corresponding complete binary tree is a heap.

For the 10-element example that we have just seen, the first step of the heapsort might rearrange the array so that the elements are in the following order:

| 45 | 27 | 42 | 21 | 23 | 22 | 35 | 19 | 4 | 5 |
|---|---|---|---|---|---|---|---|---|---|
| [0] | [1] | [2] | [3] | [4] | [5] | [6] | [7] | [8] | [9] |

![](img/7bf56f684fab50d5ff9e94ae2818f3ac_691_1.png)

After the rearrangement of the array elements, the corresponding complete binary tree is a heap, and to aid your visualization, we have drawn the corresponding tree beside the array. But keep in mind that the only place that the numbers are stored is in the array. The tree is just our visualization of how those elements are structured. In a moment, we’ll provide the details of how the rearrangement into a heap occurs, but first let’s look at the rest of the heapsort algorithm.

Recall that the largest value in a heap is stored in the root, and that in our array representation of a complete binary tree, the root node is stored in the first array position. Thus, since the array represents a heap, we know that the largest array element is in the first array position. To get the largest value into the correct array position, we simply interchange the first and the final array elements. After interchanging these two array elements, we know that the largest array element is in the final array position, as shown here:

find the largest element, and move it to the end of the array

| 5 | 27 | 42 | 21 | 23 | 22 | 35 | 19 | 4 | 45 |
|---|---|---|---|---|---|---|---|---|---|
| [0] | [1] | [2] | [3] | [4] | [5] | [6] | [7] | [8] | [9] |

The dark vertical line in the array separates the “unsorted side” of the array (on the left) from the “sorted side.” Moreover, the unsorted side (on the left) still represents a complete binary tree, which is almost a heap, as shown at the top of the next page.

| 5 | 27 | 42 | 21 | 23 | 22 | 35 | 19 | 4 | 45 |
|---|---|---|---|---|---|---|---|---|---|
| [0] | [1] | [2] | [3] | [4] | [5] | [6] | [7] | [8] | [9] |

![](img/7bf56f684fab50d5ff9e94ae2818f3ac_692_0.png)

When we consider the unsorted side as a complete binary tree, it is only the root that violates the heap storage rule. This root is smaller than its children. So, the next step of the heapsort is to reposition this one out-of-place value in order to restore the heap. In Section 11.1 we discussed this process of restoring the heap by repositioning the out-of-place root. The process, called reheapification downward, begins by comparing the value in the root with the value of each of its children. If one or both children are larger than the root, then the root node’s value is exchanged with the larger of the two children. This moves the troublesome value down one level in the tree. For our example, the out-of-place value (5) is exchanged with its larger child (42), as shown on the next page.

fix the heap

![](img/7bf56f684fab50d5ff9e94ae2818f3ac_693_0.png)

Of course, this “exchange” of values actually occurs within the array that represents the heap, so that the array now looks like this:

| 42 | 27 | 5 | 21 | 23 | 22 | 35 | 19 | 4 | 45 |
|---|---|---|---|---|---|---|---|---|---|
| [0] | [1] | [2] | [3] | [4] | [5] | [6] | [7] | [8] | [9] |

In this example, the 5 is still out of place, so we will once again exchange it with its largest child, resulting in the array (and heap) shown here:

| 42 | 27 | 35 | 21 | 23 | 22 | 5 | 19 | 4 | 45 |
|---|---|---|---|---|---|---|---|---|---|
| [0] | [1] | [2] | [3] | [4] | [5] | [6] | [7] | [8] | [9] |

![](img/7bf56f684fab50d5ff9e94ae2818f3ac_693_1.png)

Keep in mind that only the unsorted side of the array must be maintained as a heap. In general, the reheapification continues until the troublesome value reaches a leaf or it reaches a spot where it is no longer than its children.

When the unsorted side of the array is once again a heap, the heapsort continues by exchanging the largest element in the unsorted side with the rightmost element of the unsorted side. For our example, the 42 is exchanged with the 4, as shown here:

| 4 | 27 | 35 | 21 | 23 | 22 | 5 | 19 | 42 | 45 |
|---|---|---|---|---|---|---|---|---|---|
| [0] | [1] | [2] | [3] | [4] | [5] | [6] | [7] | [8] | [9] |

As you can see, the “sorted side” now has the two largest elements, and the unsorted side is once again almost a heap, as shown here:

![](img/7bf56f684fab50d5ff9e94ae2818f3ac_694_0.png)

Only the root (4) is out of place, and that may be fixed by another reheapification downward. After the reheapification downward, the largest value of the unsorted side will once again reside at location [0], and we can continue to pull out the next largest value.

Here is the pseudocode for the heapsort algorithm we have been describing:

```
// Heapsort for the array called data with n elements
1. Convert the array of n elements into a heap.
2. unsorted = n; // The number of elements in the unsorted side
3. while (unsorted > 1)
{
    // Reduce the unsorted side by one.
    --unsorted;
    Swap data[0] with data[unsorted].
    The unsorted side of the array is now a heap with the root out of place.
    Do a reheapification downward to turn the unsorted side back into
a heap.
}
```

The implementation of this pseudocode is shown in Figure 13.6. In the implementation, we use two functions, make_heap and reheapify_down, which we will discuss next.

## Making the Heap

At the start of the heapsort algorithm, we must rearrange the array elements so that they form a heap. This rearrangement is accomplished by calling a function with the following specification:

```
void make_heap(int data[], size_t n);
// Precondition: data is an array with at least n elements.
// Postcondition: The elements of data have been rearranged so that the
// complete binary tree represented by this array is a heap.
```
