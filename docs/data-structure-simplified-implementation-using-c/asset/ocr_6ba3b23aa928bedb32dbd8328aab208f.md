+   - At the end of a link list, or
+   - At the beginning/front of a link list

![](bbox=[0.18, 0.14, 0.87, 0.26])

In the insertion from the end, a new node is placed at the end of an existing link list. For instance, inserting the node with value 20, in the link list already having the node 10 is illustrated below. Here 20, will be placed after 10 and the pointer will be appropriately adjusted. After inserting 20, consider that we have to insert 30 into the existing list. Same is illustrated in the figure 3.3(b). This is known as backward growth of a link list. Since new node is attached at the end.

Simirlarly, we can create a link list that can be forward growing. In forward list, the new node is inserted at the beginning, instead of at the end. Same has been illustrated in the figure 3.4. Consider the case of figure 3.4. In this case, a node with the value of 5 already existed. The new node having value 10 is created; correspondingly it will be inserted at the beginning of the existing link list. Similarly, the new node that has arrived is 20. It will be positioned at the beginning of 10 (refer figure 3.4). This type of growth in a link list is known as forward growing link list.

![](bbox=[0.18, 0.55, 0.87, 0.75])

# B. Display the node

Once the link list is created, irrespective of the forward growing or the backward growing, we would like to view the data that is hold by various node of a link list. To display the node element, we begin from the start i.e. first node and continue to move towards the end node. Next pointer of the last node points to the NULL that can be used to stop the traversal. Logic for the traversal has been depicted in the following program: