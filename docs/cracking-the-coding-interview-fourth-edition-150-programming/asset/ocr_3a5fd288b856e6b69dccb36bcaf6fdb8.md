# Solutions to Chapter 4 | Trees and Graphs

4.3 Given a sorted (increasing order) array, write an algorithm to create a binary tree with minimal height.
pg 54

# SOLUTION

We will try to create a binary tree such that for each node, the number of nodes in the left subtree and the right subtree are equal, if possible.

Algorithm:

+   1. Insert into the tree the middle element of the array.
2. Insert (into the left subtree) the left subarray elements
3. Insert (into the right subtree) the right subarray elements
4. Recurse

```
1 public static TreeNode addTree(int arr[], int start, int end{
2   if (end < start) {
3     return null;
4   }
5   int mid = (start + end) / 2;
6   TreeNode n = new TreeNode(arr[mid]);
7   n.left = addTree(arr, start, mid - 1);
8   n.right = addTree(arr, mid + 1, end);
9   return n;
10 }
11 
12 public static TreeNode createMinimalBST(int array[]) {
13   return addTree(array, 0, array.length - 1);
14 }
```