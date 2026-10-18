+   2. Suppose that your program contains the type definitions and code given in Self-Test Exercise 1. That code creates a node that contains the string "Sally" and the number 18. What code would you add in order to set the value of the member variable next of this node equal to NULL?

+   3. Suppose that your program contains the type definitions and code given in Self-Test Exercise 1. Assuming that the value of the pointer variable head has not been changed, how can you destroy the dynamic variable pointed to by head and return the memory it uses to the freestore so that it can be reused to create new dynamic variables?

+   4. Given the following structure definition:

```
struct ListNode
{
    string item;
    int count;
    ListNode *link;
};
ListNode *head = new ListNode;
```

write code to assign the string “Wilbur’s brother Orville” to the member item of the node pointed to by head.

# Linked Lists

Lists such as those shown in Display 13.2 are called linked lists. A linked list is a list of nodes in which each node has a member variable that is a pointer that points to the next node in the list. The first node in a linked list is called the head, which is why the pointer variable that points to the first node is named head. Note that the pointer named head is not itself the head of the list but only points to the head of the list. The last node has no special name, but it does have a special property. The last node has NULL as the value of its member pointer variable. To test to see whether a node is the last node, you need only test to see if the pointer variable in the node is equal to NULL.

Our goal in this section is to write some basic functions for manipulating linked lists. For variety, and to simplify the notation, we will use a simpler type of node than that used in Display 13.2. These nodes will contain only an integer and a pointer. The node and pointer type definitions that we will use are as follows:

```
struct Node
{
    int data;
    Node *link;
};
typedef Node* NodePtr;
```