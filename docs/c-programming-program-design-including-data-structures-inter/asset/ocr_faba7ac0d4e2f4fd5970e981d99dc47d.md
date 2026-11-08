We next describe the necessary algorithm to:

+   - Divide the list into two sublists of nearly equal size.
+   - Merge both sublists.
+   - Merge the sorted sublists.

# Divide

Because data is stored in a linked list, we do not know the length of the list. Furthermore, a linked list is not a random access data structure. Therefore, to divide the list into two sublists, we need to find the middle node of the list.

Consider the list in Figure 18-31.

![](bbox=[0.158, 0.366, 0.969, 0.428])

**FIGURE 18-31**  Unsorted linked list

To find the middle of the list, we traverse the list with two pointers—say, middle and current. The pointer middle is initialized to the first node of the list. Because this list has more than two nodes, we initialize current to the third node. (Recall that we sort the list only if it has more than one element because a list of size 1 is already sorted. Also, if the list has only two nodes, we set current to NULL.) Consider the list shown in Figure 18-32.

![](bbox=[0.157, 0.656, 0.969, 0.738])

**FIGURE 18-32**  middle and current before traversing the list

Every time we advance middle by one node, we advance current by one node. After advancing current by one node, if current is not NULL, we again advance current by one node. That is, for the most part, every time middle advances by one node, current advances by two nodes. Eventually, current becomes NULL and middle points to the last node of the first sublist. For example, for the list in Figure 18-32, when current becomes NULL, middle points to the node with info 25 (see Figure 18-33).