3. If the list is not empty, the new node is “linked” into the list by setting firstNode to a new ListNode object and initializing that object with insertItem and firstNode (line 65). When the ListNode constructor (lines 20–24) executes, it sets instance variable data to refer to the insertItem passed as an argument and performs the insertion by setting the nextNode reference of the new node to the ListNode passed as an argument, which previously was the first node.

In Fig. 22.6, part (a) shows a list and a new node during the insertAtFront operation and before the program links the new node into the list. The dotted arrows in part (b) illustrate Step 3 of the insertAtFront operation that enables the node containing 12 to become the new first node in the list.

![](bbox=[0.28, 0.38, 0.78, 0.62])

Fig. 22.6 | Graphical representation of operation insertAtFront.

# List Method insertAtBack

Method insertAtBack (lines 69–75 of Fig. 22.3) places a new node at the back of the list. The steps are:

+   1. Call isEmpty to determine whether the list is empty (line 71).
+   2. If the list is empty, assign to firstNode and lastNode the new ListNode that was initialized with insertItem (line 72). The ListNode constructor at lines 13–16 calls the constructor at lines 20–24 to set instance variable data to refer to the insertItem passed as an argument and to set reference nextNode to null.
+   3. If the list is not empty, line 74 links the new node into the list by assigning to lastNode and lastNode.nextNode the reference to the new ListNode that was initialized with insertItem. ListNode’s constructor (lines 13–16) sets instance variable data to refer to the insertItem passed as an argument and sets reference nextNode to null, because this is the last node in the list.

In Fig. 22.7, part (a) shows a list and a new node during the insertAtBack operation and before linking the new node into the list. The dotted arrows in part (b) illustrate Step 3 of method insertAtBack, which adds the new node to the end of a list that’s not empty.