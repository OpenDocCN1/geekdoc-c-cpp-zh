```
enter your choice
3
2
3
menu
1.push
2.pop
3.display
4.exit
enter your choice
2
the deleted element is 2
menu
1.push
2.pop
3.display
4.exit
enter your choice
4
```

# 6.3.2 LINKED IMPLEMENTATION OF A STACK

To insert an item into the linked stack, insert the new node with that item as the first node in the singly linked list. The Top pointer that was previously pointing to the first element in the list now points to the new node. To delete an item from the linked stack, the node pointing by the top is deleted and Top points to the next node. Figure 6.7 illustrates the operations on the linked stack.

Initially stack is

![](bbox=[0.2, 0.56, 0.75, 0.61])

Insert 40 into the list

![](bbox=[0.15, 0.66, 0.85, 0.72])

(a) Push operation

Delete 40 from the linked stack

![](bbox=[0.2, 0.79, 0.75, 0.85])

(b) Pop operation

Figure 6.7 Linked implementation of a stack