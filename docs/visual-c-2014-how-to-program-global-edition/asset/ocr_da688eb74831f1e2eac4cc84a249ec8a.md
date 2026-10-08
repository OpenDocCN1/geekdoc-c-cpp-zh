# 19.4 Linked Lists 823

| True removed
The list is: 34567 hello

hello removed
The list is: 34567

34567 removed
Empty list |

**Fig. 19.5** Testing class List. (Part 3 of 3.)

# Method InsertAtFront
 the next few pages, we discuss each of the methods of class List in detail. Method InsertAtFront (Fig. 19.4, lines 49–59) places a new node at the front of the list. The method consists of three steps:

+   1. Call IsEmpty to determine whether the list is empty (line 51).
2. If the list is empty, set firstNode and lastNode to refer to a new ListNode initialized with insertItem (line 53). The ListNode constructor at line 18 calls the ListNode constructor at lines 22–26, which sets property Data to refer to the object passed as the first argument and sets the Next property’s reference to null.
3. If the list is not empty, the new node is “linked” into the list by setting firstNode to refer to a new ListNode initialized with insertItem and firstNode (line 57). When the ListNode constructor (lines 22–26) executes, it sets property Data to refer to the object passed as the first argument and performs the insertion by setting the Next reference to the ListNode passed as the second argument.

In Fig. 19.6, part (a) shows a list and a new node during the InsertAtFront operation before the new node is linked into the list. The dashed lines and arrows in part (b) illustrate Step 3 of the InsertAtFront operation, which enables the node containing 12 to become the new list front.

![](bbox=[0.318, 0.663, 0.679, 0.903])

**Fig. 19.6** InsertAtFront operation.