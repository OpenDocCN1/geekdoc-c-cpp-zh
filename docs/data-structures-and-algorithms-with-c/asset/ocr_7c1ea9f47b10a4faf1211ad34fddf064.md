# Example:

Input Data: 15, 30, 10, 5, 25 and 20.
In the first step a max-heap is built from the given data items. The list represented as a complete tree, but not ordered.

![](bbox=[0.1, 0.15, 0.9, 0.32])

Start from the node at N/2 = 6/2 = 3 position, it has one greater child and has to be downwards gradually. Therefore, the 3rd element has to be interchanged with 6th element.

![](bbox=[0.1, 0.38, 0.9, 0.53])

After processing 3rd element:

![](bbox=[0.1, 0.55, 0.9, 0.7])

Now for the 2nd element as its children are smaller, so no downward movement is required. Next the 1st element to be processed, its left child is greater of the children. So, the 1st element has to be down to the left, interchanged with 2nd element. Now the right child of 2nd element is greater and it has to be moved down to the right, interchange with 5th element.

![](bbox=[0.1, 0.78, 0.9, 0.93])