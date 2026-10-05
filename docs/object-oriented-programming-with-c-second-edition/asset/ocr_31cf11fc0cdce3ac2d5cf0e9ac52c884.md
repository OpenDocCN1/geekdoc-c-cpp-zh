# Object-Oriented Programming with C++

that carries the address of the next node in the list. This is how a node is linked to the next node.

FIFO (first-in-first-out) operation. The first node to get is the first to get out.

There are two classes that enable to create linked lists.

Trees, unlike linked lists, stacks and queues, do not have a linear structure. In a tree, each of the nodes may be connected to more than one node.

+   - A node whose objects will be the actual nodes of the single linked list. The class that we have created is SingleLinkedList.

A binary tree is a tree in which each node is linked to a maximum of two nodes. A binary tree is a finite set of elements. It is either empty or partitioned into three disjoint subsets. The first subset contains one element, the root of the tree. The other subsets are binary trees. One of them is considered to be the left-subtree and the other the right-subtree. Either or both of the sub-trees can be empty.

+   - A single list class, each object of which will represent a single list of nodes. The class that we have created is SingleLinkedList.

Binary trees have recursive structures. The entire tree has a root, a left-subtree, and a right-subtree. Both of the sub-trees are binary trees. Both of them have roots and sub-trees.

Each of the SingleLinkedList class will be a node in the linked list. This class has an integer data value, which is supposed to contain the value of the node.

While performing operation on trees, we can exploit this recursive nature of trees and make them recursive. This will make the functions shorter and reduce our programming effort.

Each of the SingleLinkedList class will have a head member, which is a pointer. This pointer is defined to the first node of the linked list. In our program, it will either be point to the first node in the list or will be assigned the NULL value (to indicate that the current list is empty).

There are three ways of traversing a tree—in-order, in-order, and post-order.

Stacks are just like linked lists, also consist of nodes where each node is linked to exactly one other node (with the exception of not connected to any other node). In a stack, we can add a node to the beginning. In a stack, we delete a node only from the top. This operation is called pop. In a stack, we add a node to the beginning. This operation is called push. Stacks are said to have a LIFO (last-in-first-out) structure. The last node to get is the first to get out.

A binary search tree is a special form of binary tree. In a binary search tree, for any given value, the value contained in its left is less than the value contained in the node and the value contained in the node is greater than the value contained in its right child.

Queues are data structures they are very similar to stacks. The difference between the two is in their operations. In a stack, the push operation causes the new node to get added to the beginning. But, in a queue, the push operation causes the new node to get added to the end. Thus, queues are said to have a

If you traverse a binary search tree in in-order (left, root, right), and display the value of each node as you visit, you will end printing the values in ascending order.

In order to create trees, we have two classes 'BSTNode' and 'BST'. The first class helped us in creating the nodes of BSTs while the second class helped us in creating the BSTs.

# Key Terms

data structures
arrays have limitations—fixed size, difficulty in inserting
values
linked lists
linked list node—value and next pointer
SingleLinkedList class
SingleLinkedList class
head pointer
append nodes to single linked lists
prefix nodes to single linked lists

find nodes in linked lists
delete nodes from linked lists
display nodes of linked lists
stacks
push operation
pop operation
LIFO in stacks
queues
FIFO in queues
trees