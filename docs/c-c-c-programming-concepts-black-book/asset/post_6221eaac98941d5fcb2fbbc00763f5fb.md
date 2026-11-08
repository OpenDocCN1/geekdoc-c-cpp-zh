
## Listing 24.36: Showing the Code for Radix Sort

Listing 24.36 shows the implementation of radix sort using C:

```c
#include "stdio.h"
#define MAX 100
#define SHOWPASS

void Radix_Sort(int *a, int n)
{
    int i, b[MAX], m = 0, exp = 1;
    for (i = 0; i < n; i++)
    {
        if (a[i] > m)
        {
            m = a[i];
        }
    }

    while (m / exp > 0)
    {
        int box[10] = { 0 };
        for (i = 0; i < n; i++)
            box[a[i] / exp % 10]++;
        for (i = 1; i < 10; i++)
            box[i] += box[i - 1];
        for (i = n - 1; i >= 0; i--)
            b[--box[a[i] / exp % 10]] = a[i];
        for (i = 0; i < n; i++)
            a[i] = b[i];
        exp *= 10;

        #ifdef SHOWPASS
        printf("\n\npass...\n");
        for (i = 0; i < n; i++)
        {
            printf("%d\t", a[i]);
        }
        #endif
    }
}

void main()
{
    int array[MAX];
    int i, n;
    printf("\nenter the number of array elements (n<%d) . . .", MAX);
    scanf("%d", &n);
    printf("\nenter the array elements. . .");
    for (i = 0; i < n; i++)
        scanf("%d", &array[i]);
    Radix_Sort(array, n);
    printf("\n\nthe sorted array is. . .");
    for (i = 0; i < n; i++)
    {
        printf("%d\t", array[i]);
    }
}
```

## Heap Sort

Heap is a property of a binary tree based on the notion of a *complete tree*. A tree is said to be complete iff,

- It is empty.
- All the levels are completely filled, except the last level.
- All the nodes are placed at the leftmost positions.
- The left sub-tree of the tree is complete with height h-1 and contains 2^h - 1 nodes and the right sub-tree is complete with height h-2. A tree is said to be completely full if it is of height H and contains 2^{H+1}-1 nodes.
- The left sub-tree of the tree is complete with height h-1 and its right sub-tree is complete with height h-1 and contains 2^{h-1} nodes.

Therefore, the heap property of a binary tree states that,

- The tree must be a complete tree.
- The key value at the root node must be greater than all its descendants. This rule also applies to all the sub-trees.

In the heap sort, we follow two steps to sort a list of elements. The steps are as follows:

- 1. Construct a binary tree by implementing the heap property. This step continues until all the elements are used to form a binary tree with the heap orientation.
- 2. Remove the largest element from the root node of the tree, replace the root node with the rightmost node in the tree, and then apply the heap orientation on the tree. The largest element is then inserted into a priority queue. This process continues until all the elements are sorted.

Let's consider the following array to understand the heap sort:

{40, 30, 10, 80, 90, 20}

Now, let's apply the two steps as follows:

### 1. Building the Heap

Iteration 1: First, we take the first element of the array, which is 40. Then, we create a tree, where 40 is the only element, as follows:

![](img/43c5f409f9b17790a628c4b4df854b61_893_0.png)

Iteration 2: The next number 30 is placed as the left child of 40 and as 40 > 30, no heap orientation is performed. This is because according to the binary tree logic, the left child node holds a value smaller than its parent node and the right child node holds a value greater than or equal to its parent node in a binary tree. The tree is as follows:

![](img/43c5f409f9b17790a628c4b4df854b61_893_1.png)

Iteration 3: Next, the element 10 is added to the tree and as 10 < 40, the heap orientation is required. The tree is as follows:

![](img/43c5f409f9b17790a628c4b4df854b61_894_0.png)

**Iteration 4:** The next element 80 is added to the tree, as follows:

![](img/43c5f409f9b17790a628c4b4df854b61_894_1.png)

As 30 < 80, 30 and 80 interchange their positions, as follows:

![](img/43c5f409f9b17790a628c4b4df854b61_894_2.png)

Again, as 40 < 80, 80 and 40 interchange their positions and 80 becomes the root node of the tree and is the highest element of the tree so far. Therefore, the tree is as follows:

![](img/43c5f409f9b17790a628c4b4df854b61_894_3.png)

**Iteration 5:** The next element 90 is added as the right descendant of the left sub-tree of the tree rooted at 80, as follows:

![](img/43c5f409f9b17790a628c4b4df854b61_894_4.png)

As 40 < 90, 40 and 90 interchange their positions, as follows:

![](img/43c5f409f9b17790a628c4b4df854b61_895_0.png)

Again, as 80 < 90, they interchange their positions making the root node to contain 90, which is the highest element of the tree so far. The tree would look like as follows:

![](img/43c5f409f9b17790a628c4b4df854b61_895_1.png)

**Iteration 6:** The next element added to the tree is 20, which is placed as the left descendant of the right-sub-tree rooted at 90, as follows:

![](img/43c5f409f9b17790a628c4b4df854b61_895_2.png)

As 20 > 10, they exchange their positions, as follows:

![](img/43c5f409f9b17790a628c4b4df854b61_895_3.png)

Therefore, we get the tree implementing the heap at the end of step 1.

- 2. In this step, we remove the root element from the tree, insert it into a priority queue, and replace the root node with the rightmost leaf element in the tree. At the end of the replacement, the sorting technique re-adjusts the tree to maintain the heap property.

**Iteration 1:** From the preceding tree, remove the root node 90, place it in the priority queue, and make the node 10 as the root node, as follows:

![](img/43c5f409f9b17790a628c4b4df854b61_896_0.png)

At this point, as 10 < 80, they interchange their positions, as follows:

![](img/43c5f409f9b17790a628c4b4df854b61_896_1.png)

As 40 > 10, they exchange their positions, as follows:

![](img/43c5f409f9b17790a628c4b4df854b61_896_2.png)

This way, the re-adjustment of the tree is performed that results in a tree with heap.

**Iteration 2:** Remove the root element 80, make the element 10 as the root element, and insert 80 in the priority queue. The resultant tree would be as follows:

![](img/43c5f409f9b17790a628c4b4df854b61_897_0.png)

As 40 > 10, they interchange their positions, as follows:

![](img/43c5f409f9b17790a628c4b4df854b61_897_1.png)

As 30 > 10, they exchange their positions by maintaining the heap property, as follows:

![](img/43c5f409f9b17790a628c4b4df854b61_897_2.png)

**Iteration 3:** Remove the root element 40, make the element 10 as the root element, and insert 40 in the priority queue. The resultant tree would be as follows:

![](img/43c5f409f9b17790a628c4b4df854b61_897_3.png)

As 10 < 30, they exchange their positions establishing the heap property, shown as follows:

![](img/43c5f409f9b17790a628c4b4df854b61_898_0.png)

**Iteration 4:** Remove the root element 30, make the element 20 as the root element, and insert 30 in the priority queue. The resultant tree would be as follows:

![](img/43c5f409f9b17790a628c4b4df854b61_898_1.png)

In this case, re-adjustment is required as the nodes are placed perfectly maintaining the heap property.

**Iteration 5:** Remove the root element 20 and the tree is only left with a single node 10. Insert 20 in the priority queue. At the end, the tree would be as follows:

![](img/43c5f409f9b17790a628c4b4df854b61_898_2.png)

**Iteration 6:** 10 is placed at the first place of the priority queue, shown as follows:

- {10, 20, 30, 40, 80, 90}

In the heap sort algorithm, we will define two procedures: one for building the heap and another for removing the last element and rebuilding the heap. Listing 24.37 shows the algorithm for heap sort:

### Listing 24.37: Showing the Algorithm for Heap Sort

```text
function Heap_Sort(A[n])
begin
    H[n] <- Form_Heap(A[0...n])
    for i <- 0 to i <- n-1
    begin
        A[n-i-1] <- H[1]
        H[1] <- H[n-i-1]
        H[n-i-1] <- Form_Heap(H[0...(n-i)])
    end
end

function Form_Heap(B[0...k])
begin
    for i <- 1 to i <- m-1
    begin
        childIndex <- i
        while(childIndex > 1) do
        begin
            parentIndex <- Floor(i/2)
            if B[parentIndex] < B[childIndex]
            begin
                temp <- B[parentIndex]
```
