+   l) The first node of a tree is the ______ node.
+   m) Each link in a tree node points to a(n) ______ or ______ of that node.
+   n) A tree node that has no children is called a(n) ______ node.
+   o) The three traversal algorithms (covered in this chapter) for a binary tree are _______, _______ and _______.

# 12.2 What are the differences between a linked list and a stack?

# 12.3 What are the differences between a stack and a queue?

# 12.4 Write a statement or set of statements to accomplish each of the following. Assume that all the manipulations occur in main (therefore, no addresses of pointer variables are needed), and assume the following definitions:

```
```c
struct gradeNode {
    char lastName[ 20 ];
    double grade;
    struct gradeNode *nextPtr;
};
typedef struct gradeNode GradeNode;
typedef GradeNode *GradeNodePtr;
```
```

+   a) Create a pointer to the start of the list called startPtr. The list is empty.
+   b) Create a new node of type GradeNode that's pointed to by pointer newPtr of type GradeNodePtr. Assign the string "Jones" to member lastName and the value 91.5 to member grade. Provide any necessary declarations and statements.
+   c) Assume that the list pointed to by startPtr currently consists of 2 nodes—one containing "Jones" and one containing "Smith". The nodes are in alphabetical order. Provide the statements necessary to insert in order nodes containing the following data for lastName and grade:
+   "Adams" 85.0
+   "Thompson" 73.5
+   "Pritchard" 66.5
+   Use pointers previousPtr, currentPtr and newPtr to perform the insertions. State what previousPtr and currentPtr point to before each insertion. Assume that newPtr always points to the new node, and that the new node has already been assigned the data.
+   d) Write a while loop that prints the data in each node of the list. Use pointer currentPtr to move along the list.
+   e) Write a while loop that deletes all the nodes in the list and frees the memory associated with each node. Use pointer currentPtr and pointer tempPtr to walk along the list and free memory, respectively.

# 12.5 (Binary Search Tree Traversals) Provide the in-order, pre-order and post-order traversals of the binary search tree of Fig. 12.22

![](bbox=[0.2, 0.92, 0.9, 0.98])

Fig. 12.22 | A 15-node binary search tree.