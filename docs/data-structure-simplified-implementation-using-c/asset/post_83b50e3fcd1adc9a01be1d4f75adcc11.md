
## EXERCISE

## A. Short Answer Type Questions

- 1. How to define the queue? Write down the various operations that are permitted in a queue?
- 2. How many ends are used to insert and remove the elements from the queue? How this phenomenon is implemented in the queue?
- 3. What are the major drawbacks of a queue? How these drawbacks are addressed?
- 4. What are the various methods with the help of which we can overcome the drawback of queues?
- 5. Implement the function that counts the number of element in the queue?
- 6. How circular queue is different from the ordinary queue?
- 7. How the circular feature in a circular queue can be implemented in a queue, justify?
- 8. During the insertion of elements in the circular queue, what are major considerations that need to be addressed?
- 9. Write a function to search an element in a circular queue?
- 10. Write a program to reverse the stack elements using queue?
- 11. Write a program to concatenate the element of two queues using operator (+) overloading.
- 12. Write a program to compare the two arrays on the basis of element count, by using operator (>) overloading.
- 13. Write a function to implement the priority while inserting the elements in the queue.
- 14. In a circular queue, how to ensure that once all the elements are dequeue then it is pointing to the Null condition.

## B. Correct the code, if any

- 1. In the given queue, front and rear has been initialized with 0. Insert function of the queue has been given as:

```
void insert (int x)
{

if (rear+1==size)
cout<<"queue overflow"<<endl;
++rear=x;
}
```

- 2. In the circular queue, front and rear has been initialized with -1. Insert function of the queue has been given as:

```
void insert (int x)
{
if (rear+1==size)
cout<<"queue overflow"<<endl;
rear+1=x;
}
```

3. In the circular queue, front and rear has been initialized with -1. Insert function of the queue has been given as:

```
void insert (int x)
{
if (rear+1==front)
cout<<"queue overflow"<<endl;
rear+1=x;
}
```

4. In dynamic queue, front and rear has been initialized with NULL. Correct the following code for enqueue.

```
void enqueue (int x)
{
if (front==rear)
{
front=new qnode;
front->data=x;
front->next=null;
}
else
{
qnode *temp;
temp=new qnode;
temp->data=x;
temp->next=null;
rear->next=temp;
}
}
```

5. In dynamic queue, front and rear has been initialized with NULL. Correct the following code for dequeue.

```
qnode* dequeue ( )
{
if (front==rear)
{
cout<<"queue is empty";
}
else
{
qnode *temp;
temp=front;
rear=rear->next;
}
}
```

6. Is it possible to remove the item from the middle of the queue? True/False

7. In queue, inserting the first element and other element is to be considered in the same manner. True/False

8. What is the reason for using a "circular queue" instead of a regular one?

+   a) The running time of enqueue () is improved
+   b) Reuse empty spaces
+   c) You can traverse all the elements more efficiently
+   d) None of the above

9. One difference between a queue and a stack is:

+   A. Queues require linked lists, but stacks do not.
+   B. Stacks require linked lists, but queues do not.
+   C. Queues use two ends of the structure; stacks use only one.
+   D. Stacks use two ends of the structure, queues use only one.

10. If the characters 'D', 'C', 'B', 'A' are placed in a queue (in that order), and then removed one at a time, in what order will they be removed?

+   A. ABCD
+   B. ABDC
+   C. DCAB
+   D. DCBA

11. Suppose we have a circular array implementation of the queue class, with ten items in the queue stored at data [2] through data [11]. The current capacity is 42. Where does the insert method place the new entry in the array?

+   A. data [1]
+   B. data [2]
+   C. data [11]
+   D. data [12]

12. Consider the implementation of the Queue using a circular array. What goes wrong if we try to keep all the items at the front of a partially-filled array (so that data [0] is always the front)?

+   A. The constructor would require linear time.
+   B. The getFront method would require linear time.
+   C. The insert method would require linear time.
+   D. The isEmpty method would require linear time.

13. In the linked list implementation of the queue class, where does the insert method place the new entry on the linked list?

+   A. At the head
+   B. At the tail
+   C. After all other entries those are greater than the new entry.
+   D. After all other entries those are smaller than the new entry.

14. In the circular array version of the Queue class, which operations require linear time for their worst-case behavior?

+   A. getFront
+   B. insert when the capacity has not yet been reached
+   C. isEmpty
+   D. None of these operations require linear time.

15. In the linked-list version of the Queue class, which operations require linear time for their worst-case behavior?

+   A. getFront
+   B. insert
+   C. isEmpty
+   D. None of these operations require linear time.

16. If data is a circular array of CAPACITY elements, and rear is an index into that array, what is the formula for the index after rear?
A. (rear % 1) + CAPACITY
B. rear % (1 + CAPACITY)
C. (rear + 1) % CAPACITY
D. rear + (1 % CAPACITY)

17. I have implemented the queue with a circular array, keeping track of front, rear, and Many Items (the number of items in the array). Suppose front is zero, and rear is one less than the current capacity. What can you tell me about many Items?
A. manyItems must be zero.
B. manyItems must be equal to the current capacity.
C. count could be zero or the capacity, but no other values could occur.
D. None of the above.

18. I have implemented the queue with a linked list, keeping track of a front node and a rear node with two reference variables. Which of these reference variables will change during an insertion into a NONEMPTY queue?
A. Neither changes
B. Only front changes.
C. Only rear changes.
D. Both change.

19. Priority Queues suppose getFront is called on a priority queue that has exactly two entries with equal priority. How is the return value of getFront selected?
A. One is chosen at random.
B. The one which was inserted first.
C. The one which was inserted most recently.
D. This can never happen (violates the precondition)

## Tree

## Chapter Objective

- Defining tree and its terminology
- Defining Binary search tree (BST)
- Creation of the BST using recursive and non-recursive method
- Traversal of a BST using recursive and non-recursive method
- Deletion a node from a BST
- Constructing the BST based on traversal series
- Searching the element in a BST
- Description of various methods to determine the height of a BST
- To determine the mirror of a tree.

### 7.1 TREE

Data structure can grow in linear or non-linear fashion, accordingly data structure can be categorized into two as mentioned hereunder:

- Linear.
- Non-linear.

![](img/9b7c80a1312a664ae505ba138aa3306b_197_0.png)

Various topics discussed earlier in the book including Stacks, Queue, Link list would fall under the category of linear data structure. In linear data structure, items are arranged one after the other. During, accessing of item, traversal takes place by visiting all the nodes previously placed. Complexity, of linear data structure is O(n). Correspondingly, performance is the major bottleneck in linear data structure. To improve the performance, a new data structure known as tree is devised. Tree is an example of non-linear data structure. In non-linear data structure, data are arranged in parent-child relationship. Same has been

![](img/9b7c80a1312a664ae505ba138aa3306b_198_0.png)

demonstrated in the following figure.

Tree categorization is determined by the maximum number of child that any parent can accommodate at any point in time. However, a node may have less number of nodes than the maximum number of a node that it can accommodate. Trees are further defined based on their degree. For instance tree with degree ‘2’ is termed as binary, tree of degree ‘3’ is termed ternary, whereas the tree of degree ‘n’ is termed as n-ary tree. For this chapter, we have considered the binary tree only.

### 7.2 BASIC TERMINOLOGY

At any point in time, a tree may hold a number of nodes, which are arranged in parent and child relationship. The node from where tree originates that node is termed as root. Node after the root node is child of another node, this will continue till we do not reach at the leaf node. Each node is acting as child of other node (except the root node). Therefore, tree can be defined as non linear data structure, organized in parent child relationship. Each node is again acting as a tree.

Before discussing the tree, it is worth discussing some of the terms that will be frequently used throughout our discussion.

Siblings: Children of same parent are known as siblings. In the tree, illustrated in the figure 7.3, the two nodes with the values 5 and 40 are siblings, since both of them are children of the same parent i.e. node 20.

Non-terminal node: Nodes in a tree with at least one child are known as non-terminal node. It can also be defined as all the nodes other than the terminal nodes are termed as non-
